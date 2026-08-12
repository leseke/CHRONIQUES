# ENGINE-018 — Personnalité générique minimale

> Version : 1.2
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004D v1.3, ENGINE-003, ENGINE-004, ENGINE-016, ENGINE-017
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 330 / 330 tests réussis

---

# 1. Objectif

Implémenter le premier framework générique de Personnalité sans inventer de Trait métier concret ni de mapping Trait/Habitude ou Trait/Ambition.

```text
règle de Trait injectée
↓
création déterministe
↓
Valeur + Poids de référence persistants
↓
Inflexion identifiable ?
├── oui → déplacement + trace causale
└── non → convergence bornée vers la référence
```

La Personnalité reste en amont de GDB-004A et ne produit jamais directement d'Intent.

---

# 2. Frontière métier

Aucun Trait concret n'est fourni par défaut.

ENGINE-018 ne déduit jamais qu'un événement est traumatique, heureux, formateur ou suffisamment profond pour modifier durablement une personnalité.

Les tests utilisent uniquement des Traits factices déterministes.

---

# 3. Données persistantes

```csharp
public sealed class PersonalityComponent : IComponent
{
    public List<PersonalityTraitState> Traits { get; set; } = new();
    public List<PersonalityInflexionTrace> Inflexions { get; set; } = new();
}
```

```csharp
public sealed record PersonalityTraitState(
    string Name,
    double Value,
    double ReferenceWeight,
    Tick CreatedAt);
```

Le Nom est l'identité du Trait au sein d'un habitant. Deux dispositions opposées restent donc deux Traits distincts.

Valeur et Poids de référence sont finis et bornés dans `[0,100]`.

---

# 4. Formation minimale

Une règle peut proposer :

```csharp
public sealed record PersonalityTraitCreationCandidate(
    string TraitName,
    double InitialValue,
    double ReferenceWeight);
```

Contraintes :

- `TraitName` non vide ;
- correspondance exacte avec la règle productrice ;
- valeurs finies dans `[0,100]` ;
- aucune duplication d'un même Nom.

Le Trait nouvellement créé conserve exactement son état initial pendant son Tick de création. La stabilisation ne commence qu'à un Tick ultérieur.

Aucun `PersonalityComponent` vide n'est créé lorsqu'aucune règle ne fournit réellement de Trait.

---

# 5. Règle concrète

```csharp
public interface IPersonalityTraitRule
{
    string TraitName { get; }

    PersonalityTraitCreationCandidate? FindCreationCandidate(
        Entity actor,
        World world,
        Tick currentTick);

    PersonalityInflexion? FindInflexion(
        PersonalityTraitState trait,
        Entity actor,
        World world,
        Tick currentTick);
}
```

Aucune implémentation métier n'est fournie en production.

ENGINE-018 ne scanne pas automatiquement `World.Events`. Une règle concrète est seule responsable d'identifier une cause pertinente à partir des données qu'une autorité lui permet de lire.

---

# 6. Stabilisation

```csharp
public interface IPersonalityStabilizationParameterResolver
{
    double ResolveMaxConvergencePerTick(
        string traitName,
        Entity actor,
        World world,
        Tick currentTick);
}
```

La vitesse résolue doit être finie et strictement positive lorsqu'une convergence est nécessaire.

Sans Inflexion applicable :

```text
distance = ReferenceWeight - Value

mouvement = min(abs(distance), MaxConvergencePerTick)

Value += signe(distance) × mouvement
```

La Valeur ne dépasse jamais le Poids de référence pendant une stabilisation normale.

Aucun bruit aléatoire implicite n'est ajouté.

---

# 7. Inflexions

```csharp
public enum PersonalityInflexionKind
{
    Light,
    Deep,
}
```

```csharp
public sealed record PersonalityInflexion(
    string CauseId,
    PersonalityInflexionKind Kind,
    double ValueDelta,
    double? NewReferenceWeight = null);
```

`CauseId` est opaque mais stable.

## Légère

- cause non vide ;
- delta fini et non nul ;
- aucun nouveau Poids de référence ;
- déplacement réel de Valeur obligatoire après Clamp ;
- référence inchangée.

## Profonde

- mêmes exigences de cause et déplacement ;
- nouveau Poids présent, fini et dans `[0,100]` ;
- nouveau Poids différent de l'ancien ;
- la nouvelle référence devient durable.

Une Inflexion appliquée remplace la stabilisation normale pour ce Trait pendant le Tick courant.

---

# 8. Trace causale persistante

```csharp
public sealed record PersonalityInflexionTrace(
    string TraitName,
    string CauseId,
    PersonalityInflexionKind Kind,
    double ValueDelta,
    double PreviousReferenceWeight,
    double NewReferenceWeight,
    Tick AppliedAt);
```

`ValueDelta` enregistre le déplacement réellement appliqué après Clamp, pas seulement le delta demandé par la règle.

Une même paire :

```text
TraitName + CauseId
```

n'est appliquée qu'une seule fois.

Une cause déjà consommée n'empêche pas la stabilisation de reprendre au Tick suivant.

Les traces persistées sont validées : cause et Trait non vides, valeurs finies, référence inchangée pour une Inflexion légère et modifiée pour une Inflexion profonde.

---

# 9. PersonalityEvolutionSystem

Le System reçoit :

- une collection ordonnée de `IPersonalityTraitRule` ;
- un `IPersonalityStabilizationParameterResolver`.

Pour chaque Entity :

1. demander les candidats de création ;
2. valider puis ajouter les Traits absents ;
3. préserver exactement les Traits créés pendant ce Tick ;
4. valider l'état persistant existant ;
5. pour chaque Trait disposant de sa règle, rechercher une Inflexion ;
6. appliquer une nouvelle cause au maximum une fois ;
7. sinon stabiliser vers le Poids de référence ;
8. laisser inchangé un Trait dont la règle n'est plus enregistrée.

Deux règles portant le même `TraitName` sont rejetées.

Le System n'avance jamais le Tick et ne publie aucun Event implicite.

---

# 10. Persistance

`PersonalityComponent` est ajouté à `EntitySnapshot` comme champ optionnel et pris en charge par `WorldRepository`.

Sans PersonalityComponent :

```text
champ Personality absent du JSON
```

Sont persistés : Traits, Valeurs, Poids de référence, Ticks de création et historique causal des Inflexions.

Les règles et resolvers restent runtime.

---

# 11. Frontière avec Habitudes et Ambitions

ENGINE-018 ne modifie aucun contrat d'ENGINE-016/017.

Aucun mapping n'est introduit.

```text
Trait + Type d'Habitude explicitement mappés
→ future modulation possible du seuil de formation

Trait + Type d'Ambition explicitement mappés
→ future modulation possible de l'Intensité
```

Ces extensions exigent leurs propres règles concrètes et restent hors du lot.

---

# 12. Implémentation validée

Fichiers ajoutés :

```text
Components/PersonalityComponent.cs
Autonomy/IPersonalityTraitRule.cs
Autonomy/IPersonalityStabilizationParameterResolver.cs
Autonomy/PersonalityEvolutionSystem.cs
```

Fichiers étendus :

```text
Persistence/WorldSnapshot.cs
Persistence/WorldRepository.cs
```

Aucun Pattern, Verbe ou Intent supplémentaire n'est créé.

---

# 13. Invariants

- aucun Trait concret sans règle injectée ;
- identité d'un Trait = Nom ;
- Valeur et Poids dans `[0,100]` ;
- création sans doublon ;
- pas de stabilisation au Tick de création ;
- convergence déterministe sans dépassement ;
- Inflexion toujours causée ;
- même cause appliquée une seule fois au même Trait ;
- légère : référence inchangée ;
- profonde : référence modifiée ;
- déplacement réel obligatoire ;
- aucune lecture automatique de `World.Events` ;
- aucune modification implicite d'Habitude ou d'Ambition ;
- aucune source d'Intent ;
- aucun Event implicite ;
- aucun avancement du Tick.

---

# 14. QA validée

```text
Engine018PersonalityTests.cs
→ 22 tests comportementaux

Engine018PersonalityInvariantTests.cs
→ 17 tests d'invariants
```

Soit **39 nouveaux tests**.

Ils couvrent notamment :

- round-trip de persistance ;
- omission JSON sans personnalité ;
- absence de Component vide ;
- création exacte et absence de stabilisation immédiate ;
- absence de doublon ;
- Trait sans règle conservé ;
- convergence montante/descendante sans dépassement ;
- Inflexion légère ;
- Inflexion profonde ;
- Clamp et delta réellement appliqué ;
- idempotence d'une cause ;
- causes distinctes ;
- Traits distincts et évolution indépendante ;
- Scheduler ;
- absence d'Event implicite ;
- absence de modulation Habitudes/Ambitions ;
- déterminisme ;
- rejet des règles, paramètres, états et Inflexions invalides.

Base précédente :

```text
291 / 291
```

Validation locale confirmée :

```text
dotnet build
→ succès

dotnet test
→ 330 / 330 tests réussis
→ 0 échec
```

---

# 15. Critère de validation

Les critères sont satisfaits :

- le build réussit ;
- les 291 tests historiques restent verts ;
- les 39 nouveaux tests sont verts ;
- la persistance est confirmée ;
- formation, stabilisation et Inflexions sont déterministes ;
- aucune règle de Trait métier ni mapping cognitif n'est introduit.

ENGINE-018 est donc **Validée / Maturité 4**.

---

# HISTORIQUE

## Version 1.2

- ENGINE-018 passe à **Validée / Maturité 4** ;
- validation locale enregistrée à **330 / 330 tests réussis** ;
- les 291 tests historiques restent verts ;
- persistance, formation, stabilisation, Inflexions légères/profondes et causalité idempotente confirmées ;
- aucun Trait concret, mapping Trait/Habitude, mapping Trait/Ambition ou nouveau Verbe ACT introduit.

## Version 1.1

- synchronisation avec l'implémentation candidate ;
- persistance PersonalityComponent ajoutée ;
- création, stabilisation et Inflexions implémentées ;
- causalité persistante et idempotente verrouillée ;
- absence de stabilisation au Tick de création explicitée ;
- 39 tests ajoutés ;
- total attendu fixé à **330 / 330**.

## Version 1.0

- création d'ENGINE-018 ;
- premier framework générique de Personnalité ;
- mappings Habitudes/Ambitions explicitement différés.

---

Fin du document
