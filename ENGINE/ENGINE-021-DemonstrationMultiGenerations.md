# ENGINE-021 — Démonstration multi-générations intégrée

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : ENGINE-009, ENGINE-010, ENGINE-019, ENGINE-020, GDB-002B v1.3, GDB-004J v1.2, GDB-008D v1.1, GDB-008G v1.2

## Objectif

Démontrer de bout en bout, sans nouveau framework métier, qu'une même Chronique peut traverser au moins deux transmissions générationnelles tout en conservant autonomie et Mémoire du Monde.

## Scénario de référence

```text
A actif / génération 0
↓
autonomie réelle
↓
A meurt
↓
HeritageSystem : A → B
↓
LifeSession : B actif
↓
GenerationContinuity : génération 1
↓
WorldMemory : réévaluation génération 1
↓
B continue d'agir autonomement
↓
B meurt
↓
HeritageSystem : B → C
↓
LifeSession : C actif
↓
GenerationContinuity : génération 2
↓
WorldMemory : réévaluation génération 2
↓
C continue d'agir autonomement
```

## Composition imposée

La preuve réutilise les briques validées :

- `Scheduler` ;
- `NeedsDecaySystem` ;
- `AutonomousActionSystem` ;
- `NeedsIntentSource` ;
- `PipelineAutonomousIntentExecutor` ;
- `AgingSystem` ;
- `HeritageSystem` ;
- `LifeSession` ;
- `GenerationContinuitySynchronizer` ;
- `LineageWorldMemoryGenerationResolver` ;
- `WorldMemoryEvolutionSystem`.

Aucune nouvelle règle métier de succession, de durée de génération ou de Mémoire n'est ajoutée.

## QA candidate

`Engine021MultiGenerationIntegrationTests.cs` ajoute 6 tests :

1. A → B → C produit exactement les générations 1 puis 2 ;
2. la Mémoire est réévaluée aux générations 1 et 2 ;
3. B exécute encore des Actions autonomes après la mort de A ;
4. C exécute encore des Actions autonomes après la mort de B ;
5. la mort d'une Entity hors continuité ne modifie pas l'index ;
6. deux exécutions identiques produisent la même trace générationnelle et le même état mémoire.

Base validée : `380 / 380`.

Total attendu : `386 / 386`.

ENGINE-021 ne passe pas M4 avant validation locale.
