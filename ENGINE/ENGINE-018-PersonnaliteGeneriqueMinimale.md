# ENGINE-018 — Personnalité générique minimale

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004D v1.3, ENGINE-003, ENGINE-004, ENGINE-016, ENGINE-017

---

# 1. Objectif

Implémenter le premier framework générique de Personnalité sans inventer de Trait métier concret ni de mapping Trait/Habitude ou Trait/Ambition.

Le moteur doit pouvoir représenter et faire évoluer :

```text
règle de Trait injectée
↓
création déterministe du Trait
↓
Valeur + Poids de référence persistants
↓
absence d'Inflexion
→ convergence bornée vers le Poids de référence

ou

cause identifiable
↓
Inflexion légère / profonde
↓
Valeur déplacée
+
Poids de référence conservé ou remplacé
↓
trace persistante de la cause
```

La Personnalité reste en amont de l'arbitrage autonome et ne produit jamais directement d'Intent.

---

# 2. Frontière métier

ENGINE-018 ne crée aucun Trait concret tel que :

- courage ;
- générosité ;
- ambition ;
- prudence ;
- sociabilité ;
- agressivité.

Il ne déduit pas non plus qu'un événement est traumatique, heureux, formateur ou suffisamment profond pour modifier une personnalité.

Ces décisions appartiennent aux règles concrètes autorisées par GDB.

Les tests utilisent uniquement des règles factices déterministes.

---

# 3. PersonalityComponent

Le moteur ajoute une donnée persistante :

```csharp
public sealed class PersonalityComponent : IComponent
{
    public List<PersonalityTraitState> Traits { get; set; } = new();
    public List<PersonalityInflexionTrace> Inflexions { get; set; } = new();
}
```

Un Trait est représenté par :

```csharp
public sealed record PersonalityTraitState(
    string Name,
    double Value,
    double ReferenceWeight,
    Tick CreatedAt);
```

Le Component reste de la donnée pure.

Le Nom est l'identité du Trait au sein d'un habitant. Deux dispositions opposées sont donc deux Noms distincts conformément à GDB-004D.

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
- le nom retourné correspond à la règle productrice ;
- `InitialValue` et `ReferenceWeight` sont finis et compris dans `[0,100]` ;
- un Trait de même Nom n'est jamais dupliqué.

Le premier lot représente la phase de formation par un état initial pouvant être éloigné du Poids de référence. La stabilisation ultérieure fait converger la Valeur vers cette référence.

Aucun Trait n'est créé si aucune règle n'en fournit un.

---

# 5. IPersonalityTraitRule

Chaque Trait concret doit être fourni par une règle injectée :

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

Le framework ne fournit aucune implémentation métier par défaut.

`FindInflexion` retourne `null` lorsqu'aucune cause identifiable ne justifie de déplacement à ce Tick.

ENGINE-018 ne scanne pas automatiquement `World.Events` et ne confond pas Mémoire du Monde et causalité de simulation. Une règle concrète peut utiliser les données autorisées par son propre contrat.

---

# 6. Stabilisation

La vitesse de convergence reste paramétrable :

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

Le résultat doit être fini et strictement positif.

En l'absence d'Inflexion applicable :

```text
distance = ReferenceWeight - Value

variation appliquée
= signe(distance) × min(abs(distance), MaxConvergencePerTick)
```

La Valeur ne dépasse donc jamais la référence pendant une convergence normale.

Le résultat est Clamp dans `[0,100]`.

Aucun bruit aléatoire implicite n'est ajouté.

---

# 7. Inflexions

Le framework distingue :

```csharp
public enum PersonalityInflexionKind
{
    Light,
    Deep,
}
```

Une règle peut produire :

```csharp
public sealed record PersonalityInflexion(
    string CauseId,
    PersonalityInflexionKind Kind,
    double ValueDelta,
    double? NewReferenceWeight = null);
```

`CauseId` est un identifiant opaque mais stable de la cause reconnue par la règle. ENGINE-018 ne lui attribue aucune sémantique narrative.

Contraintes :

## Inflexion légère

- `CauseId` non vide ;
- `ValueDelta` fini et non nul ;
- `NewReferenceWeight` doit être absent ;
- la Valeur est déplacée puis bornée `[0,100]` ;
- le Poids de référence reste inchangé.

## Inflexion profonde

- `CauseId` non vide ;
- `ValueDelta` fini et non nul ;
- `NewReferenceWeight` présent, fini, dans `[0,100]` ;
- le nouveau Poids doit différer de l'ancien ;
- la Valeur est déplacée puis bornée `[0,100]` ;
- le nouveau Poids devient permanent.

Lorsqu'une Inflexion est appliquée, aucune convergence supplémentaire n'est appliquée au même Trait pendant ce Tick. La convergence reprend aux Ticks suivants si aucune nouvelle Inflexion n'est applicable.

---

# 8. Traçabilité des Inflexions

Chaque Inflexion appliquée ajoute :

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

La trace rend la cause identifiable après sauvegarde/rechargement.

Pour une Inflexion légère :

```text
PreviousReferenceWeight == NewReferenceWeight
```

Pour une Inflexion profonde, les deux valeurs diffèrent.

Une même paire `TraitName + CauseId` n'est appliquée qu'une fois. Si la règle repropose la même cause à un Tick ultérieur, le framework l'ignore.

---

# 9. PersonalityEvolutionSystem

`PersonalityEvolutionSystem` reçoit :

- une collection ordonnée de `IPersonalityTraitRule` ;
- un `IPersonalityStabilizationParameterResolver`.

Pour chaque habitant et Tick :

1. demander à chaque règle un candidat de création ;
2. créer uniquement les Traits valides et absents ;
3. ne créer `PersonalityComponent` que si au moins un Trait est réellement créé ;
4. pour chaque Trait dont la règle existe, chercher une Inflexion ;
5. appliquer au maximum une Inflexion au Trait pour ce passage ;
6. sinon appliquer la convergence vers le Poids de référence ;
7. ne jamais avancer le Tick lui-même.

Deux règles portant le même `TraitName` sont rejetées à la construction du System.

Un Trait persisté dont la règle n'est plus enregistrée reste présent mais n'évolue pas.

---

# 10. Persistance

`PersonalityComponent` est ajouté à `EntitySnapshot` comme champ optionnel.

Sans PersonalityComponent, le champ est omis du JSON.

Sont persistés :

- Nom du Trait ;
- Valeur ;
- Poids de référence ;
- Tick de création ;
- historique des Inflexions et leurs causes.

Les règles et resolvers restent runtime et ne sont jamais sérialisés.

---

# 11. Frontière avec Habitudes et Ambitions

ENGINE-018 ne modifie pas :

- `HabitIntentSource` ;
- `HabitLearningObserver` ;
- `IHabitFormationParameterResolver` ;
- `AmbitionEvolutionSystem` ;
- `AmbitionIntentSource` ;
- ACT `Intent`.

Aucun mapping n'est créé.

Les futures modulations autorisées par GDB-004D devront être introduites par des règles concrètes distinctes :

```text
Trait + Type d'Habitude explicitement mappés
→ éventuelle modulation du seuil de formation

Trait + Type d'Ambition explicitement mappés
→ éventuelle modulation de l'Intensité
```

Ces deux extensions sont hors ENGINE-018.

---

# 12. Non-objectifs

ENGINE-018 ne définit pas :

- catalogue de Traits ;
- états émotionnels ;
- score psychologique global ;
- personnalité comme source d'Intent ;
- mapping Trait/Habitude ;
- mapping Trait/Ambition ;
- influence directe sur besoin, transfert ou production ;
- significativité narrative automatique ;
- aléatoire implicite ;
- nouveau Pattern ou Verbe ACT.

---

# 13. Invariants

- Un Trait possède Nom, Valeur et Poids de référence.
- Valeur et Poids restent dans `[0,100]`.
- Aucun Trait concret n'existe sans règle injectée.
- Une règle ne peut créer qu'un Trait portant son propre Nom.
- Une Inflexion exige une cause non vide.
- Une même cause ne s'applique qu'une fois au même Trait.
- Une Inflexion légère ne modifie jamais le Poids de référence.
- Une Inflexion profonde modifie le Poids de référence.
- Sans Inflexion, la Valeur converge sans dépasser sa référence.
- La personnalité ne produit jamais d'Intent.
- Aucun mapping cognitif n'est implicite.
- Le System ne lit pas automatiquement `World.Events` pour inventer des causes.
- Le System n'avance jamais le Tick.

---

# 14. Critère de validation

ENGINE-018 pourra passer Validée / Maturité 4 lorsque, avec uniquement des règles factices déterministes, le moteur démontrera :

- création contrôlée de Traits ;
- absence de doublons ;
- persistance complète ;
- convergence vers le Poids de référence dans les deux directions ;
- absence de dépassement ;
- Inflexion légère avec référence inchangée ;
- Inflexion profonde avec nouvelle référence durable ;
- cause persistée et non réappliquée ;
- rejet des données invalides ;
- Trait sans règle conservé mais non évolué ;
- intégration Scheduler ;
- absence totale de production d'Intent ou de modulation implicite d'Habitudes/Ambitions.

Base validée avant ce lot :

```text
291 / 291
```

---

# HISTORIQUE

## Version 1.0

- création d'ENGINE-018 ;
- premier framework générique de Personnalité ;
- modèle Traits / Valeur / Poids de référence ;
- stabilisation déterministe ;
- Inflexions légères/profondes avec cause persistante ;
- mappings Habitudes/Ambitions explicitement différés.

---

Fin du document
