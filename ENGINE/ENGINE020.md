# ENGINE-020 — Continuité générationnelle explicite

> Version : 1.1
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : GDB-002B v1.3, GDB-004J v1.2, GDB-008D v1.1, GDB-008G v1.2, ENGINE-009, ENGINE-019
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 380 / 380 tests réussis

## Objectif

Fournir un index de génération persistant propre à une continuité identifiée et exploitable par ENGINE-019.

## Implémentation validée

`GenerationContinuityComponent` conserve `ContinuityId`, `GenerationIndex`, `CurrentMemberId` et l'historique des passages.

`GenerationContinuityRegistry` crée, retrouve et avance une continuité. Un passage avance l'index d'exactement `+1`; une preuve déjà consommée est idempotente.

`GenerationContinuitySynchronizer` reçoit l'identifiant actif déjà résolu par l'orchestration de vie et n'accepte qu'un résultat `heritage.transmission` du Tick courant reliant l'ancien membre au nouveau.

`LineageWorldMemoryGenerationResolver` expose l'index à `WorldMemoryEvolutionSystem` sans mutation.

La persistance est assurée via `EntitySnapshot.GenerationContinuity` et `WorldRepository`.

## Frontières validées

- aucun compteur global du World ;
- aucune conversion Tick-vers-génération ;
- aucune copie automatique de Components ;
- plusieurs continuités peuvent coexister ;
- seule une transmission réellement adoptée fait progresser une continuité ;
- l'index avance exactement de `+1` ;
- une preuve déjà consommée est idempotente.

## QA validée

`Engine020Tests.cs` ajoute 10 tests couvrant création, erreurs de configuration, coexistence, avancement exact, idempotence, synchronisation, resolver et round-trip de persistance.

Base précédente : `370 / 370`.

Validation locale :

```text
dotnet test
→ 380 / 380 tests réussis
→ 0 échec
```

ENGINE-020 est **Validée / Maturité 4**.

## Historique

### Version 1.1

- validation locale à `380 / 380` ;
- passage en Validée / Maturité 4 ;
- continuité générationnelle persistante et resolver Mémoire confirmés.

### Version 1.0

- création d'ENGINE-020 ;
- continuité de lignée, synchronisation et resolver générationnel introduits ;
- 10 tests candidats ajoutés.
