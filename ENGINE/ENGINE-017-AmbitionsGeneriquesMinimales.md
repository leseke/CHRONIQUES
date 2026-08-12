# ENGINE-017 — Ambitions génériques minimales

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004D v1.3, GDB-004F v1.2, ACT-002-H, ENGINE-010, ENGINE-016

---

# 1. Objectif

Implémenter le premier framework générique d'Ambitions sans inventer un Type d'Ambition métier concret.

Le moteur doit pouvoir :

```text
règle concrète d'Ambition injectée
↓
conditions de création satisfaites
↓
Ambition persistante
↓
évaluation déterministe de l'Objectif
↓
Progrès mis à jour
↓
Ambition candidate
↓
arbitrage Intensité → Progrès → ancienneté
↓
Intent
↓
ACT
```

Le framework doit également représenter l'accomplissement et l'abandon sans inventer leur logique métier.

---

# 2. Frontière métier

ENGINE-017 ne crée aucun Type concret tel que :

- devenir riche ;
- obtenir un logement ;
- atteindre une Compétence donnée ;
- améliorer une Relation ;
- posséder un stock ;
- réussir une carrière.

Les tests peuvent utiliser des règles factices déterministes afin de valider le framework.

La présence d'un exemple dans GDB-004F ne suffit jamais à créer un Type concret en production.

---

# 3. AmbitionComponent

Le moteur ajoute une donnée persistante :

```csharp
public sealed class AmbitionComponent : IComponent
{
    public List<AmbitionState> Ambitions { get; set; } = new();
}
```

Une Ambition persistante est représentée par :

```csharp
public sealed record AmbitionState(
    string AmbitionTypeId,
    string InstanceKey,
    string ObjectivePayload,
    string IntentObjective,
    double Intensity,
    double Progress,
    bool IsAbandoned,
    Tick CreatedAt);
```

`AmbitionComponent` reste de la donnée pure.

---

# 4. Type, instance et Objectif

`AmbitionTypeId` identifie la règle concrète qui sait interpréter l'Ambition.

`InstanceKey` identifie de façon stable une instance d'Ambition au sein d'un habitant.

L'identité technique du premier lot est :

```text
AmbitionTypeId
+
InstanceKey
```

`ObjectivePayload` est une donnée opaque persistée. ENGINE-017 ne l'interprète jamais et ne déduit jamais un Type à partir de ce payload.

La règle concrète du Type est seule responsable de produire et lire ce payload.

Cette frontière permet à de futurs Types de représenter leurs données propres sans introduire un modèle universel de logement, relation, compétence ou stock dans ENGINE.

---

# 5. AmbitionCreationCandidate

Une règle concrète peut proposer :

```csharp
public sealed record AmbitionCreationCandidate(
    string AmbitionTypeId,
    string InstanceKey,
    string ObjectivePayload,
    string IntentObjective,
    double InitialIntensity);
```

Contraintes du framework :

- `AmbitionTypeId`, `InstanceKey` et `IntentObjective` non vides ;
- le `AmbitionTypeId` retourné doit correspondre à la règle qui produit la candidate ;
- `InitialIntensity` doit être finie et strictement supérieure à 0, au maximum 100 ;
- une instance déjà présente avec le même couple `AmbitionTypeId + InstanceKey` n'est jamais dupliquée.

Le payload peut être vide uniquement si la règle concrète déclare qu'aucune donnée supplémentaire n'est nécessaire ; le moteur ne lui attribue aucune sémantique.

---

# 6. IAmbitionRule

Chaque Type concret doit fournir une règle injectée :

```csharp
public interface IAmbitionRule
{
    string AmbitionTypeId { get; }

    IReadOnlyList<AmbitionCreationCandidate> FindCreationCandidates(
        Entity actor,
        World world,
        Tick currentTick);

    AmbitionEvaluation Evaluate(
        AmbitionState ambition,
        Entity actor,
        World world,
        Tick currentTick);

    bool IsIntentTreatable(
        AmbitionState ambition,
        Entity actor,
        World world,
        Tick currentTick);
}
```

Le framework ne fournit aucune implémentation métier `IAmbitionRule` par défaut.

`FindCreationCandidates` matérialise les conditions de création du Type.

`Evaluate` interprète l'Objectif et calcule son Progrès.

`IsIntentTreatable` interdit la production d'un faux Intent lorsqu'aucune réponse ACT réellement traitable n'est disponible.

---

# 7. AmbitionEvaluation

Le résultat d'évaluation générique est :

```csharp
public sealed record AmbitionEvaluation(
    double Progress,
    bool ShouldAbandon);
```

Le framework impose :

- `Progress` fini ;
- Clamp `[0,100]` ;
- `ShouldAbandon` déterministe pour un même World/Objectif/Type/configuration.

`Progress = 100` signifie Ambition accomplie.

`ShouldAbandon = true` marque l'Ambition comme abandonnée.

Accomplissement et abandon rendent l'Ambition non candidate mais ne suppriment pas automatiquement sa trace persistante dans ce lot.

---

# 8. AmbitionEvolutionSystem

`AmbitionEvolutionSystem` reçoit la collection ordonnée des `IAmbitionRule`.

Pour chaque habitant et Tick :

1. demander à chaque règle ses candidates de création ;
2. valider et ajouter les nouvelles instances non dupliquées ;
3. évaluer chaque Ambition existante dont la règle est disponible ;
4. mettre à jour `Progress` ;
5. appliquer `IsAbandoned = true` lorsque la règle le demande.

Les nouvelles Ambitions sont évaluées dès le Tick de leur création afin que leur Progrès reflète immédiatement le World courant.

Une Ambition persistée dont la règle n'est plus enregistrée reste présente mais n'est ni évaluée ni rendue candidate.

Le System n'avance jamais le Tick lui-même.

---

# 9. Intensité

`Intensity` reste bornée entre 0 et 100 et sert à l'arbitrage interne entre Ambitions.

Dans ENGINE-017 :

- la création fournit une Intensité initiale ;
- une Intensité à 0 n'est jamais candidate ;
- aucune formule universelle de renforcement ou d'affaiblissement n'est introduite ;
- aucun Trait de personnalité n'est interprété par le framework.

Les futures variations d'Intensité devront provenir d'une règle concrète identifiable conforme à GDB-004D/F.

ENGINE-017 ne transforme donc pas un Tick ordinaire en cause silencieuse d'évolution psychologique.

---

# 10. AmbitionIntentSource

`AmbitionIntentSource` implémente `IAutonomousIntentSource`.

Une Ambition est candidate si :

```text
règle disponible
+
Intensity > 0
+
Progress < 100
+
IsAbandoned = false
+
Intent traitable
→ candidate
```

L'arbitrage suit strictement GDB-004F :

1. Intensité la plus élevée ;
2. Progrès le plus élevé ;
3. `CreatedAt` le plus ancien.

Si plusieurs Ambitions restent totalement égales après ces trois critères, l'ordre persistant dans `AmbitionComponent.Ambitions` sert uniquement de stabilité technique.

La source :

- retourne au maximum un Intent ;
- utilise `IntentObjective` ;
- ne modifie jamais le World ;
- n'ajoute aucune métadonnée d'Ambition à ACT `Intent` ;
- utilise une Priorité technique neutre, l'ordre inter-familles restant porté par GDB-004A.

---

# 11. Composition autonome

Aucun changement de `CompositeAutonomousIntentSource` n'est requis.

La composition complète devient :

```text
NeedsIntentSource
↓ sinon
VoluntaryFoodTransferIntentSource
↓ sinon
ProductiveActivityIntentSource
↓ sinon
HabitIntentSource
↓ sinon
AmbitionIntentSource
↓ sinon
aucun Intent
```

Une Ambition d'Intensité élevée ne peut donc pas dépasser une famille placée plus haut.

---

# 12. Persistance

`AmbitionComponent` est ajouté à `EntitySnapshot` comme champ optionnel.

Sans `AmbitionComponent`, le champ est omis du JSON afin de préserver la forme historique des sauvegardes.

Sont persistés :

- Type ;
- InstanceKey ;
- ObjectivePayload ;
- IntentObjective ;
- Intensité ;
- Progrès ;
- état d'abandon ;
- Tick de création.

Les règles `IAmbitionRule` restent des services runtime et ne sont jamais sérialisées.

---

# 13. Personnalité

ENGINE-017 ne crée aucun `PersonalityComponent` et n'applique aucun mapping Trait/Ambition.

La frontière est néanmoins compatible avec GDB-004D : une future règle concrète pourra calculer l'Intensité initiale ou une évolution explicitement autorisée à partir d'un mapping déterministe.

Aucun coefficient psychologique universel n'est introduit ici.

---

# 14. Non-objectifs

ENGINE-017 ne définit pas :

- Type concret d'Ambition ;
- Ambition de carrière, richesse, logement ou relation ;
- formule universelle de Progrès ;
- évolution universelle d'Intensité ;
- PersonalityComponent ;
- mapping Trait/Ambition concret ;
- Opportunité PNJ ;
- fairness inter-familles ;
- nouveau Pattern ou Verbe ACT ;
- plan multi-étapes spécifique aux Ambitions.

---

# 15. Invariants

- Aucun Type concret n'est créé sans règle injectée.
- Le moteur générique n'interprète jamais `ObjectivePayload`.
- Une instance est identifiée par `AmbitionTypeId + InstanceKey`.
- Une instance existante n'est jamais dupliquée.
- Progrès et Intensité restent bornés entre 0 et 100.
- Une Ambition accomplie ou abandonnée ne produit aucun Intent.
- Une règle absente ne produit aucun faux Intent.
- Une Ambition non traitable ne bloque pas les autres candidates.
- L'arbitrage suit Intensité → Progrès → ancienneté.
- Intensité ne compare que des Ambitions.
- La source d'Intent ne mute jamais le World.
- ACT `Intent` ne porte aucune métadonnée d'Ambition.
- Aucun Type métier, Trait, Opportunité PNJ ou nouveau Verbe n'est inventé.

---

# 16. Critère de validation

ENGINE-017 pourra passer Validée / Maturité 4 lorsque, avec uniquement des règles factices déterministes, le moteur démontrera :

- création d'une Ambition par règle injectée ;
- absence de création sans règle/candidate valide ;
- absence de doublon ;
- persistance complète ;
- évaluation déterministe du Progrès ;
- accomplissement à Progrès 100 ;
- abandon explicite ;
- sélection Intensité → Progrès → ancienneté ;
- absence de faux Intent si règle ou traitabilité manque ;
- absence de mutation du World par la source ;
- intégration dans la dernière famille de `CompositeAutonomousIntentSource` ;
- aucun Type concret ni nouveau Verbe ACT introduit.

Base validée avant ce lot :

```text
260 / 260
```

---

# HISTORIQUE

## Version 1.0

- création d'ENGINE-017 ;
- premier framework générique d'Ambitions ;
- Objectif porté par payload opaque interprété uniquement par la règle concrète ;
- création, évaluation, accomplissement, abandon et sélection spécifiés ;
- évolution universelle d'Intensité explicitement différée.

---

Fin du document
