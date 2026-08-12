# ENGINE-017 — Ambitions génériques minimales

> Version : 1.1
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004D v1.3, GDB-004F v1.2, ACT-002-H, ENGINE-010, ENGINE-016
> Implémentation candidate : `CHRONIQUES-ENGINE`

---

# 1. Objectif

Implémenter le premier framework générique d'Ambitions sans inventer un Type d'Ambition métier concret.

```text
règle concrète injectée
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
Intensité → Progrès → ancienneté
↓
Intent
↓
ACT
```

ENGINE-017 représente également accomplissement et abandon sans inventer leur logique métier.

---

# 2. Frontière métier

Aucun Type concret n'est fourni par défaut.

Ne sont notamment pas créés : ambition de richesse, logement, Compétence, Relation, stock ou carrière.

Les tests utilisent uniquement des règles factices déterministes.

---

# 3. Données persistantes

```csharp
public sealed class AmbitionComponent : IComponent
{
    public List<AmbitionState> Ambitions { get; set; } = new();
}
```

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

Le Component reste de la donnée pure.

---

# 4. Identité et Objectif

Une instance est identifiée par :

```text
AmbitionTypeId + InstanceKey
```

`ObjectivePayload` est persisté mais reste totalement opaque pour ENGINE-017. Seule la règle associée au `AmbitionTypeId` sait le produire et l'interpréter.

Le moteur ne déduit jamais un Type d'Ambition depuis un texte ou un payload.

---

# 5. Création

Une règle peut produire :

```csharp
public sealed record AmbitionCreationCandidate(
    string AmbitionTypeId,
    string InstanceKey,
    string ObjectivePayload,
    string IntentObjective,
    double InitialIntensity);
```

Contraintes :

- Type, InstanceKey et IntentObjective non vides ;
- ObjectivePayload non null ;
- le Type retourné correspond à la règle productrice ;
- `InitialIntensity` finie dans `]0,100]` ;
- aucune duplication du couple `AmbitionTypeId + InstanceKey`.

---

# 6. IAmbitionRule

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

Aucune implémentation métier n'est fournie en production.

---

# 7. Évaluation

```csharp
public sealed record AmbitionEvaluation(
    double Progress,
    bool ShouldAbandon);
```

Le Progrès doit être fini puis est Clamp dans `[0,100]`.

`Progress = 100` signifie accomplissement.

`ShouldAbandon = true` marque explicitement l'Ambition comme abandonnée.

Accomplissement et abandon rendent l'Ambition non candidate mais conservent sa trace persistante.

---

# 8. AmbitionEvolutionSystem

Pour chaque habitant et Tick :

1. interroger les règles dans leur ordre d'enregistrement ;
2. créer les candidates valides non dupliquées ;
3. évaluer immédiatement les Ambitions disposant encore de leur règle ;
4. mettre à jour Progrès et état d'abandon ;
5. supprimer une Ambition dont `Intensity <= 0`, conformément à GDB-004F.

Une Ambition dont la règle n'est plus enregistrée reste persistée mais n'est pas évaluée.

Le System n'avance jamais le Tick.

---

# 9. Intensité

L'Intensité est persistée, bornée `[0,100]` et utilisée uniquement pour départager les Ambitions.

ENGINE-017 ne définit aucune formule universelle de renforcement/affaiblissement.

Les variations futures devront provenir d'une cause et d'une règle concrètes conformes à GDB-004D/F.

---

# 10. AmbitionIntentSource

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

Arbitrage :

1. Intensité la plus élevée ;
2. Progrès le plus élevé ;
3. `CreatedAt` le plus ancien ;
4. à égalité totale, ordre persistant du Component comme stabilité technique uniquement.

La source retourne au maximum un Intent, ne mute jamais le World et n'ajoute aucune métadonnée d'Ambition à ACT `Intent`.

---

# 11. Composition autonome

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

Aucun changement de `CompositeAutonomousIntentSource` n'est requis.

---

# 12. Persistance

`AmbitionComponent` est ajouté à `EntitySnapshot` comme champ optionnel.

Sans Ambition, le champ est omis du JSON.

Sont persistés : Type, InstanceKey, ObjectivePayload, IntentObjective, Intensité, Progrès, abandon et Tick de création.

Les règles restent runtime et ne sont jamais sérialisées.

---

# 13. Personnalité

ENGINE-017 n'introduit aucun `PersonalityComponent` ni mapping Trait/Ambition.

La structure reste compatible avec une future modulation déterministe explicitement autorisée.

---

# 14. Implémentation candidate

Fichiers ajoutés :

```text
Components/AmbitionComponent.cs
Autonomy/IAmbitionRule.cs
Autonomy/AmbitionEvolutionSystem.cs
Autonomy/AmbitionIntentSource.cs
```

Fichiers étendus :

```text
Persistence/WorldSnapshot.cs
Persistence/WorldRepository.cs
```

Aucun Pattern ou Verbe ACT n'est ajouté.

---

# 15. Non-objectifs

ENGINE-017 ne définit pas :

- Type concret d'Ambition ;
- formule universelle de Progrès ;
- évolution universelle d'Intensité ;
- PersonalityComponent ;
- mapping Trait/Ambition ;
- Opportunité PNJ ;
- fairness inter-familles ;
- nouveau Pattern ou Verbe ACT.

---

# 16. Invariants

- Aucun Type concret sans règle injectée.
- `ObjectivePayload` reste opaque.
- Identité = `AmbitionTypeId + InstanceKey`.
- Pas de doublon.
- Progrès et Intensité dans `[0,100]`.
- Intensité 0 supprimée par l'évolution.
- Accomplissement et abandon interdisent l'Intent.
- Règle absente = aucun faux Intent.
- Ambition non traitable = ignorée sans bloquer les autres.
- Arbitrage Intensité → Progrès → ancienneté.
- La source ne mute jamais le World.
- Aucun Type métier, Trait, Opportunité PNJ ou nouveau Verbe inventé.

---

# 17. QA candidate

Deux fichiers sont ajoutés :

```text
Engine017AmbitionTests.cs
→ 25 tests

Engine017AmbitionInvariantTests.cs
→ 6 tests
```

Soit **31 nouveaux tests**.

Ils couvrent notamment : persistance, omission JSON, création, évaluation immédiate, absence de doublon, règle absente, Clamp du Progrès, accomplissement, abandon, suppression à Intensité 0, sélection, traitabilité, stabilité des égalités, absence de mutation par la source, ordre du composite et intégration complète `Tick → création → Ambition → Intent → Action`.

Base validée :

```text
260 / 260
```

Total attendu avant validation locale :

```text
291 / 291
```

---

# 18. Critère de validation

ENGINE-017 pourra passer Validée / Maturité 4 lorsque le build réussit, que les 260 tests historiques restent verts et que les 31 tests candidats valident le framework sans introduire de Type concret ni nouveau Verbe ACT.

---

# HISTORIQUE

## Version 1.1

- synchronisation avec l'implémentation candidate ;
- AmbitionComponent, règle générique, évolution, source d'Intent et persistance enregistrés ;
- suppression à Intensité 0 alignée sur GDB-004F ;
- 31 tests ajoutés ;
- total attendu fixé à **291 / 291**.

## Version 1.0

- création d'ENGINE-017 ;
- premier framework générique d'Ambitions ;
- Objectif porté par payload opaque ;
- évolution universelle d'Intensité explicitement différée.

---

Fin du document
