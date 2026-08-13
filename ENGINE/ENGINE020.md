# ENGINE-020 — Continuité générationnelle explicite

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : GDB-002B v1.3, GDB-004J v1.2, GDB-008D v1.1, GDB-008G v1.2, ENGINE-009, ENGINE-019

## Objectif

Fournir un index de génération persistant propre à une continuité identifiée et exploitable par ENGINE-019.

## Implémentation candidate

`GenerationContinuityComponent` conserve `ContinuityId`, `GenerationIndex`, `CurrentMemberId` et l'historique des passages.

`GenerationContinuityRegistry` crée, retrouve et avance une continuité. Un passage avance l'index d'exactement `+1`; une preuve déjà consommée est idempotente.

`GenerationContinuitySynchronizer` reçoit l'identifiant actif déjà résolu par l'orchestration de vie et n'accepte qu'un résultat `heritage.transmission` du Tick courant reliant l'ancien membre au nouveau.

`LineageWorldMemoryGenerationResolver` expose l'index à `WorldMemoryEvolutionSystem` sans mutation.

La persistance est étendue via `EntitySnapshot.GenerationContinuity` et `WorldRepository`.

## Frontières

Aucun compteur global du World. Aucune conversion Tick-vers-génération. Aucune copie automatique de Components. Plusieurs continuités peuvent coexister.

## QA candidate

`Engine020Tests.cs` ajoute 10 tests couvrant création, erreurs de configuration, coexistence, avancement exact, idempotence, synchronisation, resolver et round-trip de persistance.

Base validée : `370 / 370`.

Total attendu : `380 / 380`.

ENGINE-020 ne passe pas M4 avant validation locale.
