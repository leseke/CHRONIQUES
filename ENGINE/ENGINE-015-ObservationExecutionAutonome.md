# ENGINE-015 — Observation de l'exécution autonome

> Version : 1.2
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004E v1.2, GDB-004F v1.2, ACT-002-H, ENGINE-006, ENGINE-010 à ENGINE-014
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 233 / 233 tests réussis

---

# 1. Objectif

Créer une frontière d'observation entre un Intent autonome et l'Action réellement exécutée afin que de futurs systèmes d'apprentissage, notamment les Habitudes, puissent distinguer :

```text
Intent sélectionné
↓
Action réellement exécutée
↓
Outcome succès / échec
↓
World après Effects
```

ENGINE-015 n'implémente aucune Habitude ou Ambition concrète.

---

# 2. Problème architectural

`AutonomousActionSystem` remet l'Intent à :

```csharp
public interface IAutonomousIntentExecutor
{
    void Execute(Intent intent, World world);
}
```

Cette abstraction reste correcte pour ENGINE-010, mais son `void` masque l'`ActionInstance` et son `Outcome`.

GDB-004E exige pourtant de distinguer activation, exécution et réussite avant de pouvoir former ou renforcer une Habitude.

La source d'Intent ne peut pas résoudre ce problème en mutant le World : ENGINE-010 lui interdit d'être une seconde couche d'Effects.

---

# 3. Décision validée

ENGINE-015 **ne modifie pas** `IAutonomousIntentExecutor`.

Il ajoute un adaptateur concret vers `PipelineRunner` capable de notifier des observateurs avant et après l'exécution.

Restent inchangés :

- `IAutonomousIntentExecutor` ;
- `AutonomousActionSystem` ;
- `PipelineRunner` ;
- ACT `Intent`.

Aucune métadonnée de source n'est ajoutée à l'Intent.

---

# 4. IAutonomousIntentExecutionObserver

```csharp
public interface IAutonomousIntentExecutionObserver
{
    void BeforeExecution(
        Intent intent,
        Entity actor,
        World world,
        Tick currentTick);

    void AfterExecution(
        Intent intent,
        Entity actor,
        ActionInstance action,
        World world,
        Tick requestedAt);

    void ExecutionAborted(
        Intent intent,
        Entity actor,
        World world,
        Tick requestedAt,
        Exception error);
}
```

## BeforeExecution

Appelé avant `PipelineRunner.Execute`.

Cette phase permet de capturer le contexte pré-Effects et ne constitue pas une seconde source d'Action ou d'Effects.

## AfterExecution

Appelé uniquement si `PipelineRunner.Execute` retourne une `ActionInstance`.

À cet instant :

- l'Action est `Archived` ;
- son `Outcome` est défini ;
- les Effects d'une réussite ont déjà été appliqués ;
- un échec métier normal reste observable via `OutcomeForme.Echec`.

Un futur système autorisé peut alors mettre à jour ses propres données d'apprentissage, sans réappliquer ni modifier rétroactivement les Effects de l'Action terminée.

## ExecutionAborted

Appelé lorsque le pipeline lève une exception au lieu de retourner une Action.

L'observateur peut nettoyer son contexte temporaire, puis l'exception originale est relancée.

---

# 5. PipelineAutonomousIntentExecutor

Le nouvel adaptateur implémente toujours `IAutonomousIntentExecutor`.

```text
Execute(Intent, World)
↓
résoudre l'Actor
↓
capturer requestedAt = World.CurrentTick
↓
BeforeExecution des observers
↓
PipelineRunner.Execute
├── exception → ExecutionAborted → rethrow
└── ActionInstance retournée
    ↓
    AfterExecution
```

Les observateurs sont appelés dans leur ordre d'enregistrement.

---

# 6. Implémentation validée

Fichiers ajoutés dans `CHRONIQUES-ENGINE` :

```text
Simulation/Chroniques.Simulation/Autonomy/
├── IAutonomousIntentExecutionObserver.cs
└── PipelineAutonomousIntentExecutor.cs
```

Aucun fichier historique d'ENGINE-010/012/013/014 n'a été modifié pour introduire cette capacité.

---

# 7. Invariants validés

- Aucun changement de `IAutonomousIntentExecutor`.
- Aucun changement de `AutonomousActionSystem`.
- Aucun changement de `PipelineRunner`.
- Aucun changement d'ACT `Intent`.
- Un Actor absent du World est rejeté avant toute observation.
- `BeforeExecution` voit le World avant les Effects.
- `AfterExecution` voit l'Action archivée et le World après les Effects.
- `OutcomeForme.Echec` déclenche `AfterExecution`, pas `ExecutionAborted`.
- Une exception du pipeline déclenche `ExecutionAborted`, puis est relancée.
- L'ordre des observateurs est déterministe.
- ENGINE-015 ne crée aucune Habitude, Ambition, règle de formation ou comportement concret.

---

# 8. Pourquoi cette brique précède les Habitudes

GDB-004E v1.2 distingue :

```text
Intent produit
≠
Action exécutée avec succès
```

La formation et le renforcement futurs peuvent désormais lire le résultat réel sans :

- faire muter le World par une source d'Intent ;
- encoder l'identité d'une Habitude dans ACT `Intent` ;
- déduire le succès depuis un Event métier particulier ;
- dupliquer `PipelineRunner`.

---

# 9. Non-objectifs

ENGINE-015 ne définit pas :

- `HabitComponent` ;
- formation ou érosion d'Habitudes ;
- Déclencheur ou Signature de formation concret ;
- `AmbitionComponent` ;
- progression d'Ambition ;
- personnalité ;
- nouveau Pattern ou Verbe ACT ;
- nouveau comportement autonome.

---

# 10. Validation QA

Le fichier ajouté est :

```text
Tests/Chroniques.Simulation.Tests/
└── Engine015AutonomousExecutionObservationTests.cs
```

Il contient **9 nouveaux tests** vérifiant :

1. exécution normale sans observateur ;
2. Actor absent rejeté avant observation ;
3. `BeforeExecution` avant application des Effects ;
4. `AfterExecution` après archivage et Effects ;
5. échec métier normal observé par `AfterExecution` ;
6. ordre déterministe de plusieurs observateurs ;
7. exception du pipeline → `ExecutionAborted` ;
8. exception originale relancée et aucun `AfterExecution` ;
9. intégration `AutonomousActionSystem → PipelineAutonomousIntentExecutor → PipelineRunner` sans Tick supplémentaire.

Base précédente :

```text
224 / 224
```

Validation locale confirmée :

```text
dotnet build
→ succès

dotnet test
→ 233 / 233 tests réussis
→ 0 échec
```

Les 224 tests historiques restent donc verts et les 9 tests ENGINE-015 sont validés.

---

# 11. Critère de validation

Le critère est satisfait : le moteur démontre qu'un système futur peut observer le contexte pré-exécution et l'Outcome post-exécution sans modifier les contrats historiques d'autonomie ou d'ACT.

ENGINE-015 est **Validée / Maturité 4**.

---

# HISTORIQUE

## Version 1.2

- ENGINE-015 passe à **Validée / Maturité 4** ;
- validation locale confirmée à **233 / 233 tests réussis** ;
- les 224 tests historiques restent verts ;
- observation pré-Effects, post-Effects, échec métier, exception et déterminisme confirmés ;
- aucun contrat historique modifié.

## Version 1.1

- synchronisation avec l'implémentation candidate ;
- deux nouvelles briques techniques enregistrées ;
- 9 tests ajoutés ;
- total attendu fixé à **233 / 233**.

## Version 1.0

- création d'ENGINE-015 ;
- ajout du contrat d'observation avant/après/abandon ;
- maintien intégral des contrats historiques.

---

Fin du document
