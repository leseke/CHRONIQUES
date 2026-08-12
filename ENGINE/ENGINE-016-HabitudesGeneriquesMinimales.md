# ENGINE-016 — Habitudes génériques minimales

> Version : 1.2
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004D v1.3, GDB-004E v1.2, ACT-002-H, ENGINE-010, ENGINE-015
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 260 / 260 tests réussis

---

# 1. Objectif

Implémenter le premier framework générique d'Habitudes sans inventer une Habitude métier concrète.

Le moteur sait désormais :

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

Le framework permet également l'érosion déterministe d'une Habitude inactive.

---

# 2. Frontière métier

ENGINE-016 n'introduit aucun comportement concret tel que :

- « se reposer tous les soirs » ;
- « aller travailler le matin » ;
- « manger à heure fixe » ;
- « rendre visite à un proche » ;
- « pratiquer un loisir ».

Ces exemples exigent chacun une règle GDB concrète avant d'être fournis comme configuration de production.

Les tests ENGINE-016 utilisent uniquement des règles factices déterministes afin de valider le framework, sans donner à ces règles un statut canonique.

---

# 3. Données persistantes

Le moteur ajoute :

```csharp
public sealed class HabitComponent : IComponent
{
    public List<HabitState> Habits { get; set; } = new();
    public List<HabitFormationTrace> FormationTraces { get; set; } = new();
}
```

Une Habitude formée :

```csharp
public sealed record HabitState(
    string HabitTypeId,
    string IntentObjective,
    string FormationSignature,
    double Force,
    Tick? LastActivatedAt,
    Tick CreatedAt);
```

Une trace de formation :

```csharp
public sealed class HabitFormationTrace
{
    public string HabitTypeId { get; set; }
    public string IntentObjective { get; set; }
    public string FormationSignature { get; set; }
    public List<Tick> ObservedAt { get; set; }
}
```

`LastActivatedAt = null` signifie que l'Habitude vient d'être formée mais n'a pas encore elle-même produit d'Intent.

Le Component reste de la donnée pure.

---

# 4. Identité d'une Habitude

Le premier lot identifie une Habitude par :

```text
HabitTypeId
+
IntentObjective
+
FormationSignature
```

Deux observations de ce même triplet alimentent la même séquence de formation.

Une Habitude déjà formée empêche la création d'un doublon de même identité.

---

# 5. Règle concrète injectée

Chaque type concret d'Habitude doit fournir :

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

`ObserveFormation` fournit la Signature déterministe ou `null` si l'Intent observé n'appartient pas à ce type.

Une candidate dont `HabitTypeId` ne correspond pas à la règle qui l'a produite est ignorée.

`IsTriggered` évalue le Déclencheur concret.

`IsIntentTreatable` empêche tout faux Intent.

Aucune implémentation métier `IHabitRule` n'est fournie par défaut.

---

# 6. Formation

Les paramètres sont résolus par type :

```csharp
public sealed record HabitFormationParameters(
    int RequiredRepetitions,
    long WindowTicks,
    double InitialForce);
```

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

Cette frontière pourra intégrer plus tard un mapping Trait/Habitude explicitement autorisé par GDB-004D.

Une observation appartient à la fenêtre lorsque :

```text
currentTick - observedTick < WindowTicks
```

Les observations plus anciennes sont retirées avant comptage.

Contraintes validées du premier lot :

- `RequiredRepetitions > 0` ;
- `WindowTicks > 0` ;
- `InitialForce` finie et strictement comprise entre 0 et 100.

Lorsque le seuil est atteint, l'Habitude est créée puis la trace correspondante supprimée.

La formation compte les Intents dont le pipeline retourne une `ActionInstance` terminée, y compris un `OutcomeForme.Echec`.

Une exception technique du pipeline ne valide aucune observation de formation.

---

# 7. Registre runtime de sélection

ACT `Intent` reste indépendant de sa source.

`HabitSelectionRegistry` relie temporairement :

- Acteur ;
- identité de l'Habitude ;
- Tick de sélection.

Le registre n'est pas persisté et ne modifie jamais le World.

Il est consommé par `HabitLearningObserver` après exécution ou abandon technique.

---

# 8. HabitIntentSource

`HabitIntentSource` implémente `IAutonomousIntentSource`.

Elle :

1. lit `HabitComponent` ;
2. ignore `Force <= 0` ;
3. exige une `IHabitRule` correspondante ;
4. exige un Déclencheur vrai ;
5. exige un Intent actuellement traitable ;
6. trie par Force décroissante ;
7. départage une égalité par `CreatedAt` le plus ancien ;
8. enregistre la sélection runtime ;
9. produit exactement un Intent.

La source ne modifie jamais le World ni `LastActivatedAt`.

La `Priorite` technique de l'Intent reste neutre ; l'ordre inter-familles appartient à GDB-004A et `CompositeAutonomousIntentSource`.

---

# 9. HabitLearningObserver

`HabitLearningObserver` implémente `IAutonomousIntentExecutionObserver` d'ENGINE-015.

## BeforeExecution

Les candidates de formation sont capturées en mémoire runtime sur le World pré-Effects.

Aucune donnée persistante n'est créée lorsqu'aucune candidate et aucune sélection d'Habitude n'existent.

## AfterExecution

Les candidates capturées sont ajoutées aux traces de formation, y compris pour un échec métier normal.

Si l'Intent provenait d'une Habitude :

- `LastActivatedAt` reçoit toujours le Tick de sélection ;
- `Reussite` et `ReussitePartielle` peuvent renforcer la Force ;
- `Echec` et `Interruption` ne renforcent pas.

## ExecutionAborted

Une exception technique :

- ne forme pas ;
- ne renforce pas ;
- conserve cependant l'activation si l'Habitude avait déjà été sélectionnée et avait produit son Intent ;
- nettoie les données runtime temporaires.

Cette distinction respecte GDB-004E : activation et réussite sont deux faits différents.

---

# 10. Politique de Force

La forme numérique du renforcement et de l'érosion reste injectée :

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

Le framework :

- exige une valeur finie ;
- applique un Clamp `[0,100]` ;
- interdit à `Reinforce` de diminuer la Force ;
- interdit à `Erode` de l'augmenter.

Aucune formule par défaut n'est imposée.

---

# 11. HabitEvolutionSystem

`HabitEvolutionSystem` reçoit :

```csharp
long InactivityThresholdTicks
IHabitStrengthPolicy
```

La référence d'inactivité est :

```text
LastActivatedAt
si présent

sinon
CreatedAt
```

L'érosion devient applicable lorsque :

```text
currentTick - référence > InactivityThresholdTicks
```

Une Force ramenée à 0 supprime l'Habitude.

Le System n'avance jamais le Tick.

---

# 12. Persistance

`HabitComponent` est ajouté à `EntitySnapshot` comme champ optionnel.

Sans `HabitComponent`, le champ `Habits` est omis du JSON afin de préserver la forme historique des sauvegardes.

Sont persistés :

- Habitudes formées ;
- Force ;
- Ticks de création/activation ;
- traces de formation et leurs Ticks.

Ne sont pas persistés :

- `IHabitRule` ;
- politiques ;
- resolver de paramètres ;
- `HabitSelectionRegistry`.

---

# 13. Composition autonome

Aucun changement de `CompositeAutonomousIntentSource` n'est requis.

La composition compatible devient :

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

ENGINE-016 n'implémente pas encore les Ambitions.

---

# 14. Implémentation validée

Fichiers ajoutés :

```text
Components/
└── HabitComponent.cs

Autonomy/
├── IHabitRule.cs
├── IHabitFormationParameterResolver.cs
├── IHabitStrengthPolicy.cs
├── HabitSelectionRegistry.cs
├── HabitIntentSource.cs
├── HabitLearningObserver.cs
└── HabitEvolutionSystem.cs
```

Fichiers étendus :

```text
Persistence/WorldSnapshot.cs
Persistence/WorldRepository.cs
```

Aucun Pattern ou Verbe ACT n'est ajouté.

---

# 15. Non-objectifs

ENGINE-016 ne définit pas :

- Habitude concrète de repos, travail, alimentation ou loisir ;
- Trait de personnalité concret ;
- mapping Trait/Habitude concret ;
- perturbation par événement significatif ;
- Ambition ;
- fairness inter-familles ;
- nouveau Pattern ou Verbe ACT ;
- score cognitif global.

---

# 16. Invariants validés

- Aucune Habitude concrète n'est créée sans règle injectée.
- Une règle absente ne produit aucun faux Intent.
- La source d'Intent ne mute jamais le World.
- L'Intent ne contient aucune métadonnée d'Habitude.
- La Force compare uniquement des Habitudes.
- L'arbitrage interne suit Force puis ancienneté.
- Formation, activation et renforcement sont distincts.
- Un échec métier peut compter pour formation et activation, jamais pour renforcement.
- Une exception technique ne forme ni ne renforce, mais ne nie pas une activation déjà survenue.
- Renforcement ne diminue jamais la Force.
- Érosion ne l'augmente jamais.
- Toute Force reste dans `[0,100]`.
- Une Force à 0 supprime l'Habitude lors de l'évolution.
- Aucun nouveau Verbe ACT n'est créé.

---

# 17. Validation QA

Deux fichiers de tests couvrent ENGINE-016 :

```text
Engine016HabitTests.cs
→ 24 tests

Engine016HabitInvariantTests.cs
→ 3 tests
```

Soit **27 nouveaux tests**.

Ils couvrent notamment :

1. round-trip de persistance des Habitudes/traces ;
2. omission JSON sans HabitComponent ;
3. absence de faux Intent sans Component/règle/Déclencheur/traitabilité ;
4. Force nulle non candidate ;
5. sélection Force puis ancienneté ;
6. absence de mutation de LastActivatedAt par la source ;
7. formation au seuil de répétitions ;
8. séparation de signatures ;
9. éviction des observations hors fenêtre ;
10. absence de doublon ;
11. échec métier compté comme observation terminée ;
12. exception technique non comptée pour la formation ;
13. activation sur échec métier ;
14. renforcement sur réussite + clamp 100 ;
15. activation conservée sur abort technique ;
16. érosion seulement après seuil ;
17. suppression à Force 0 ;
18. CreatedAt utilisé avant première activation ;
19. absence de HabitComponent vide ;
20. rejet d'un renforcement décroissant ;
21. rejet d'une érosion croissante ;
22. scénario complet `répétition → formation → HabitIntentSource → Action`.

Base précédente :

```text
233 / 233
```

Validation locale confirmée :

```text
dotnet build
→ succès

dotnet test
→ 260 / 260 tests réussis
→ 0 échec
```

Les 233 tests historiques restent donc verts et les 27 tests ENGINE-016 sont validés.

---

# 18. Critère de validation

Le critère est satisfait : le moteur démontre, avec uniquement des règles factices de test, la persistance, la formation déterministe, la sélection, l'activation, le renforcement, l'érosion et la réutilisation d'une Habitude via ACT sans introduire une Habitude métier canonique ni un nouveau Verbe.

ENGINE-016 est **Validée / Maturité 4**.

---

# HISTORIQUE

## Version 1.2

- ENGINE-016 passe à **Validée / Maturité 4** ;
- validation locale confirmée à **260 / 260 tests réussis** ;
- les 233 tests historiques restent verts ;
- 27 tests ENGINE-016 validés ;
- persistance, formation, arbitrage, activation, renforcement, érosion et scénario bout-en-bout confirmés ;
- aucune Habitude métier canonique ni nouveau Pattern/Verbe ACT introduits.

## Version 1.1

- synchronisation avec l'implémentation candidate ;
- persistance HabitComponent ajoutée ;
- formation, sélection, activation, renforcement et érosion implémentés ;
- activation conservée après abandon technique ;
- monotonie du renforcement et de l'érosion verrouillée ;
- 27 tests ajoutés ;
- total attendu fixé à **260 / 260**.

## Version 1.0

- création d'ENGINE-016 ;
- premier framework générique d'Habitudes ;
- aucun comportement d'Habitude canonique introduit.

---

Fin du document
