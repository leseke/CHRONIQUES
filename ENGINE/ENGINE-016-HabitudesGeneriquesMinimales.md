# ENGINE-016 — Habitudes génériques minimales

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004D v1.3, GDB-004E v1.2, ACT-002-H, ENGINE-010, ENGINE-015

---

# 1. Objectif

Implémenter le premier framework générique d'Habitudes sans inventer une Habitude métier concrète.

Le moteur doit pouvoir :

```text
Intent réellement exécuté dans un contexte déterministe
↓
observation de formation
↓
répétitions suffisantes dans une fenêtre configurée
↓
Habitude persistante
↓
Déclencheur concret satisfait
↓
Intent produit par l'Habitude
↓
exécution normale via ACT
↓
activation tracée
+
renforcement uniquement après réussite
```

Le framework doit également permettre l'érosion déterministe d'une Habitude inactive.

---

# 2. Frontière métier

ENGINE-016 n'introduit aucun comportement concret tel que :

- « se reposer tous les soirs » ;
- « aller travailler le matin » ;
- « manger à heure fixe » ;
- « rendre visite à un proche » ;
- « pratiquer un loisir ».

Ces exemples exigent chacun une règle GDB concrète avant d'être fournis comme configuration de production.

Les tests ENGINE-016 peuvent utiliser des règles factices déterministes afin de valider le framework, sans donner à ces règles un statut canonique.

---

# 3. HabitComponent

Le moteur introduit une donnée persistante :

```csharp
public sealed class HabitComponent : IComponent
{
    public List<HabitState> Habits { get; set; } = new();
    public List<HabitFormationTrace> FormationTraces { get; set; } = new();
}
```

Une Habitude formée est représentée par :

```csharp
public sealed record HabitState(
    string HabitTypeId,
    string IntentObjective,
    string FormationSignature,
    double Force,
    Tick? LastActivatedAt,
    Tick CreatedAt);
```

Une trace de formation conserve :

```csharp
public sealed class HabitFormationTrace
{
    public string HabitTypeId { get; set; }
    public string IntentObjective { get; set; }
    public string FormationSignature { get; set; }
    public List<Tick> ObservedAt { get; set; }
}
```

`LastActivatedAt = null` signifie qu'une Habitude vient d'être formée mais n'a pas encore elle-même été sélectionnée comme source d'Intent.

`HabitComponent` reste de la donnée pure et ne décide rien.

---

# 4. Identité d'une Habitude

Dans ce premier lot, une Habitude est identifiée au sein d'un habitant par le triplet :

```text
HabitTypeId
+
IntentObjective
+
FormationSignature
```

Deux traces ayant ce même triplet appartiennent à la même séquence de formation.

Une fois l'Habitude formée, le moteur ne crée pas de doublon du même triplet.

---

# 5. IHabitRule

Chaque type concret d'Habitude doit fournir une règle injectée :

```csharp
public interface IHabitRule
{
    string HabitTypeId { get; }

    HabitFormationCandidate? ObserveFormation(
        Intent intent,
        Entity actor,
        World world,
        Tick currentTick);

    bool IsTriggered(
        HabitState habit,
        Entity actor,
        World world,
        Tick currentTick);

    bool IsIntentTreatable(
        HabitState habit,
        Entity actor,
        World world,
        Tick currentTick);
}
```

`ObserveFormation` fournit la Signature de formation déterministe exigée par GDB-004E ou retourne `null` lorsque l'Intent observé n'appartient pas à ce type d'Habitude.

`IsTriggered` évalue uniquement le Déclencheur concret.

`IsIntentTreatable` empêche une Habitude de produire un faux Intent lorsqu'aucun Plan réellement exécutable n'est disponible.

Le framework ne fournit aucune règle `IHabitRule` de production par défaut.

---

# 6. Formation

La configuration de formation est fournie par type :

```csharp
public sealed record HabitFormationParameters(
    int RequiredRepetitions,
    long WindowTicks,
    double InitialForce);
```

Le moteur injecte un resolver :

```csharp
public interface IHabitFormationParameterResolver
{
    HabitFormationParameters Resolve(
        string habitTypeId,
        Entity actor,
        World world,
        Tick currentTick);
}
```

Cette frontière permet ultérieurement à GDB-004D de modifier le seuil de répétitions via un mapping Trait/Habitude concret sans introduire de coefficient implicite dans ENGINE-016.

Une observation appartient à la fenêtre courante lorsque :

```text
currentTick - observedTick < WindowTicks
```

Les observations plus anciennes sont retirées avant comptage.

Lorsque le nombre d'observations du même triplet atteint `RequiredRepetitions`, une Habitude est créée avec `InitialForce`, bornée par contrat dans `[0,100]`, puis la trace correspondante est retirée.

La formation compte les Intents ayant traversé le pipeline jusqu'à une `ActionInstance` terminée, indépendamment de son Outcome métier. Une exception technique du pipeline ne constitue pas une observation de formation validée.

Cette distinction est technique : un `OutcomeForme.Echec` est un résultat simulé valide ; une exception est une exécution avortée.

---

# 7. HabitSelectionRegistry

ACT `Intent` reste indépendant de sa source. ENGINE-016 n'ajoute donc aucun identifiant d'Habitude dans `Intent`.

Un registre runtime non persistant relie temporairement la sélection d'une Habitude à l'exécution qui suit :

```csharp
public sealed class HabitSelectionRegistry
```

Il enregistre au minimum :

- Acteur ;
- triplet d'identité de l'Habitude ;
- Tick de sélection.

Il ne modifie pas le World.

Le registre est consommé par l'observer d'apprentissage et nettoyé après exécution ou abandon technique.

---

# 8. HabitIntentSource

`HabitIntentSource` implémente `IAutonomousIntentSource`.

Il :

1. lit `HabitComponent` ;
2. ignore toute Habitude dont `Force <= 0` ;
3. retrouve la règle correspondant à `HabitTypeId` ;
4. exige `IsTriggered == true` ;
5. exige `IsIntentTreatable == true` ;
6. départage les candidates par Force décroissante ;
7. en cas d'égalité, choisit `CreatedAt` le plus ancien ;
8. enregistre la sélection dans `HabitSelectionRegistry` ;
9. retourne exactement un `Intent` portant `IntentObjective`.

La source ne modifie jamais `HabitComponent` ni aucune autre donnée du World.

La `Priorite` technique de l'Intent reste neutre dans ce lot : l'ordre entre familles est déjà assuré par `CompositeAutonomousIntentSource` conformément à GDB-004A.

---

# 9. HabitLearningObserver

`HabitLearningObserver` implémente `IAutonomousIntentExecutionObserver`.

## BeforeExecution

Il capture en mémoire runtime les `HabitFormationCandidate` retournés par les règles pour le contexte pré-Effects.

Il ne modifie pas encore le World.

## AfterExecution

Il réalise deux opérations indépendantes.

### Formation

Les candidates capturées sont ajoutées aux traces de formation, même si l'Outcome métier est `Echec`, car l'Action a été réellement terminée et observée.

### Activation / renforcement

Si `HabitSelectionRegistry` indique que l'Intent provenait d'une Habitude :

- `LastActivatedAt` reçoit le Tick de sélection, quel que soit l'Outcome métier ;
- si `OutcomeForme` n'est pas `Echec`, la Force est renforcée via la politique injectée ;
- si l'Outcome est `Echec`, la Force n'est pas renforcée.

## ExecutionAborted

Les captures temporaires et la sélection runtime sont nettoyées.

Aucune observation de formation ni renforcement n'est commis pour une exécution techniquement avortée.

---

# 10. IHabitStrengthPolicy

La forme exacte du renforcement et de l'érosion reste paramétrable conformément à GDB-004E.

ENGINE-016 introduit :

```csharp
public interface IHabitStrengthPolicy
{
    double Reinforce(
        HabitState habit,
        Entity actor,
        World world,
        Tick currentTick);

    double Erode(
        HabitState habit,
        Entity actor,
        World world,
        Tick currentTick);
}
```

Chaque méthode retourne la nouvelle Force souhaitée.

Le framework applique ensuite un Clamp `[0,100]`.

Aucune formule de renforcement ou d'érosion par défaut n'est imposée par ENGINE-016.

---

# 11. HabitEvolutionSystem

`HabitEvolutionSystem` applique l'érosion.

Il reçoit :

```csharp
long InactivityThresholdTicks
IHabitStrengthPolicy
```

Une Habitude dont `LastActivatedAt` est `null` utilise `CreatedAt` comme point de départ de l'inactivité.

L'érosion devient applicable lorsque :

```text
currentTick - référenceInactivité > InactivityThresholdTicks
```

Lorsque la Force obtenue atteint `0`, l'Habitude est retirée.

Le System n'avance jamais le Tick lui-même.

---

# 12. Persistance

`HabitComponent`, ses Habitudes et ses traces de formation sont ajoutés à `EntitySnapshot` comme champ optionnel.

Lorsque l'Entity ne possède pas `HabitComponent`, le champ est omis du JSON afin de préserver la forme historique des sauvegardes.

Les règles `IHabitRule`, les politiques et le `HabitSelectionRegistry` sont des services runtime et ne sont jamais sérialisés.

---

# 13. Composition autonome

ENGINE-016 ne modifie pas `CompositeAutonomousIntentSource`.

La composition attendue devient :

```text
NeedsIntentSource
↓ sinon
VoluntaryFoodTransferIntentSource
↓ sinon
ProductiveActivityIntentSource
↓ sinon
HabitIntentSource
↓ sinon
future AmbitionIntentSource
```

ENGINE-016 n'implémente pas encore la dernière source.

---

# 14. Non-objectifs

ENGINE-016 ne définit pas :

- Habitude concrète de repos, travail, alimentation ou loisir ;
- Trait de personnalité concret ;
- mapping Trait/Habitude concret ;
- perturbation par événement significatif ;
- Ambition ;
- fairness inter-familles ;
- nouveau Pattern ou Verbe ACT ;
- score cognitif global.

La perturbation significative reste différée jusqu'à ce qu'un besoin concret l'exige.

---

# 15. Invariants

- Aucune Habitude concrète n'est créée sans `IHabitRule` injectée.
- Une règle absente ne produit aucun faux Intent.
- La source d'Intent ne mute jamais le World.
- L'Intent ne contient aucune métadonnée d'Habitude.
- La Force ne compare que des Habitudes candidates.
- L'arbitrage interne suit Force puis ancienneté.
- Formation, activation et renforcement sont trois faits distincts.
- Un échec métier peut compter pour la formation et l'activation mais jamais pour le renforcement.
- Une exception technique ne forme ni ne renforce.
- Les règles de dynamique de Force sont injectées.
- Toute Force est bornée entre 0 et 100.
- Une Force à 0 supprime l'Habitude lors de l'évolution.
- Le framework ne crée aucun nouveau Verbe ACT.

---

# 16. Critère de validation

ENGINE-016 pourra passer Validée / Maturité 4 lorsque le moteur démontrera, avec uniquement des règles factices de test :

- persistance des Habitudes et traces ;
- formation déterministe par répétition/signature/fenêtre ;
- absence de doublons ;
- sélection Force puis ancienneté ;
- absence de faux Intent si Déclencheur/règle/traitabilité échoue ;
- absence de mutation du World par la source ;
- activation distincte du renforcement ;
- renforcement seulement après réussite ;
- érosion et suppression à Force 0 ;
- intégration `formation → Habitude → Intent → Action` sans nouveau Verbe.

Base validée avant ce lot :

```text
233 / 233
```

---

# HISTORIQUE

## Version 1.0

- création d'ENGINE-016 ;
- premier framework générique d'Habitudes ;
- séparation explicite entre règle concrète, données persistantes et services runtime ;
- formation, activation, renforcement et érosion spécifiés ;
- aucun comportement d'Habitude canonique introduit.

---

Fin du document
