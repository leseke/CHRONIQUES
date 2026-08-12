# ENGINE-015 — Observation de l'exécution autonome

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : GDB-004A v1.3, GDB-004E v1.2, GDB-004F v1.2, ACT-002-H, ENGINE-006, ENGINE-010 à ENGINE-014

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

`AutonomousActionSystem` remet aujourd'hui l'Intent à :

```csharp
public interface IAutonomousIntentExecutor
{
    void Execute(Intent intent, World world);
}
```

Cette abstraction est correcte pour ENGINE-010, mais son `void` masque l'`ActionInstance` et son `Outcome`.

Or GDB-004E exige notamment de distinguer :

- activation d'une Habitude ;
- exécution réussie de son Intent ;
- renforcement uniquement après réussite.

La source d'Intent ne peut pas résoudre ce problème en mutant le World : ENGINE-010 lui interdit d'être une seconde couche d'Effects.

---

# 3. Décision

ENGINE-015 **ne modifie pas** `IAutonomousIntentExecutor`.

Il ajoute un adaptateur concret vers `PipelineRunner` capable de notifier des observateurs avant et après l'exécution.

Ainsi :

- tous les exécuteurs historiques restent compatibles ;
- `AutonomousActionSystem` reste inchangé ;
- `PipelineRunner` reste inchangé ;
- ACT `Intent` reste inchangé ;
- aucune métadonnée de source n'est ajoutée à l'Intent.

---

# 4. IAutonomousIntentExecutionObserver

Contrat :

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

Il permet à un futur système d'apprentissage de capturer les données de contexte **avant** que les Effects de l'Action modifient le World.

Un observateur ne doit pas utiliser cette phase comme une seconde source d'Action ou d'Effects.

## AfterExecution

Appelé uniquement si `PipelineRunner.Execute` retourne une `ActionInstance`.

À cet instant :

- l'Action est `Archived` ;
- son `Outcome` est défini ;
- les Effects d'une réussite ont déjà été appliqués ;
- un échec métier normal reste observable via `OutcomeForme.Echec`.

Cette phase peut ultérieurement permettre à un système autorisé de mettre à jour ses propres données d'apprentissage, mais elle ne peut jamais réappliquer ou modifier rétroactivement les Effects de l'Action terminée.

## ExecutionAborted

Appelé lorsque le pipeline lève une exception au lieu de retourner une Action.

Cette notification permet à un observateur ayant capturé un contexte en `BeforeExecution` de nettoyer son état temporaire.

L'exception originale est ensuite relancée.

---

# 5. PipelineAutonomousIntentExecutor

Le nouvel adaptateur implémente toujours :

```csharp
IAutonomousIntentExecutor
```

Flux :

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

# 6. Invariants

- Aucun changement de `IAutonomousIntentExecutor`.
- Aucun changement de `AutonomousActionSystem`.
- Aucun changement de `PipelineRunner`.
- Aucun changement d'ACT `Intent`.
- Un Actor absent du World est rejeté avant toute observation.
- `BeforeExecution` voit le World avant les Effects.
- `AfterExecution` voit l'Action archivée et le World après les Effects.
- Un `OutcomeForme.Echec` est une exécution terminée et déclenche `AfterExecution`, pas `ExecutionAborted`.
- Une exception du pipeline déclenche `ExecutionAborted`, puis est relancée.
- L'ordre des observateurs est déterministe.
- ENGINE-015 ne crée aucune Habitude, Ambition, règle de formation ou comportement concret.

---

# 7. Pourquoi cette brique précède les Habitudes

GDB-004E v1.2 distingue :

```text
Intent produit
≠
Action exécutée avec succès
```

La formation et le renforcement futurs doivent donc pouvoir lire le résultat réel sans :

- faire muter le World par `HabitIntentSource` ;
- encoder l'identité d'une Habitude dans ACT `Intent` ;
- déduire le succès depuis un Event métier particulier ;
- dupliquer `PipelineRunner`.

ENGINE-015 fournit cette frontière une seule fois pour les systèmes futurs.

---

# 8. Non-objectifs

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

# 9. Contrat QA

La validation doit vérifier au minimum :

1. exécution normale sans observateur ;
2. Actor absent rejeté avant observation ;
3. `BeforeExecution` avant application des Effects ;
4. `AfterExecution` après archivage et Effects ;
5. un échec métier normal observé par `AfterExecution` ;
6. ordre déterministe de plusieurs observateurs ;
7. exception du pipeline → `ExecutionAborted` ;
8. exception originale relancée et aucun `AfterExecution` ;
9. intégration `AutonomousActionSystem → PipelineAutonomousIntentExecutor → PipelineRunner` sans Tick supplémentaire.

Base validée avant ce lot :

```text
224 / 224
```

---

# 10. Critère de validation

ENGINE-015 pourra passer M4 lorsque la suite historique reste verte et que le moteur démontre qu'un système futur peut observer le contexte pré-exécution et l'Outcome post-exécution sans modifier les contrats historiques d'autonomie ou d'ACT.

---

# HISTORIQUE

## Version 1.0

- création d'ENGINE-015 ;
- ajout du contrat d'observation avant/après/abandon ;
- maintien intégral de `IAutonomousIntentExecutor`, `AutonomousActionSystem`, `PipelineRunner` et ACT `Intent`.

---

Fin du document
