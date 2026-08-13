# ENGINE — Catalogue

> Version : 1.32
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE

## Documents

```text
ENGINE-000  Principes d'architecture                  Stable
ENGINE-001  Journal d'événements du World            Stable
ENGINE-002  Kernel                                   Stable
ENGINE-003  Scheduler                                Stable
ENGINE-004  Systems                                  Stable
ENGINE-005  Persistence                              Stable
ENGINE-006  Action Pipeline                          Validée / M4
ENGINE-007  Resource Manager                         Réservé
ENGINE-008  Population                               Validée / M4
ENGINE-009  Boucle de vie                            Validée / M4
ENGINE-010  Orchestration autonome                   Validée / M4
ENGINE-011  Décision par besoins                     Validée / M4
ENGINE-012  Alimentation autonome                    Validée / M4
ENGINE-013  Production autonome                      Validée / M4
ENGINE-014  Circulation autonome                     Validée / M4
ENGINE-015  Observation exécution autonome           Validée / M4
ENGINE-016  Habitudes génériques                     Validée / M4
ENGINE-017  Ambitions génériques                     Validée / M4
ENGINE-018  Personnalité générique                   Validée / M4
ENGINE-019  Mémoire du Monde                         Validée / M4
ENGINE-020  Continuité générationnelle               Validée / M4
```

## Validation courante

```text
dotnet test
→ 380 / 380 tests réussis
→ 0 échec
```

## Bloc mémoire et générations

```text
ENGINE-019
→ Mémoire du Monde générique
→ 370 / 370 à validation

ENGINE-020
→ continuité générationnelle explicite
→ 380 / 380 à validation
```

Autorités principales : `GDB-002B v1.3`, `GDB-008D v1.1`, `GDB-008G v1.2`, `GDB-004J v1.2`.

Briques validées ENGINE-020 :

```text
GenerationContinuityComponent
GenerationTransitionTrace
GenerationContinuityRegistry
GenerationContinuitySynchronizer
LineageWorldMemoryGenerationResolver
```

Principe validé : une continuité identifiée possède son propre index. Un changement de membre n'est accepté qu'avec un `heritage.transmission` correspondant. L'index progresse exactement de `+1`. Aucun compteur global du World ni conversion Tick-vers-génération n'est introduit.

Persistance validée : `EntitySnapshot.GenerationContinuity` + `WorldRepository`.

QA ENGINE-020 : `Engine020Tests.cs` — 10 tests.

## État des blocs

```text
ENGINE-013/014 → économie matérielle → TECH-005
ENGINE-015/016/017 → cognition autonome → TECH-006
ENGINE-018 → personnalité → 330/330
ENGINE-019/020 → mémoire + continuité générationnelle → 380/380
```

## Frontières restantes

- démonstration multi-générations complète de bout en bout ;
- Type concret de Mémoire ;
- événements mondiaux autonomes complets ;
- mappings Trait/Habitude et Trait/Ambition ;
- comportements cognitifs narratifs concrets ;
- économie commerciale ;
- fairness inter-familles.

## Historique

### Version 1.32

- ENGINE-020 passe à **Validée / Maturité 4** ;
- suite globale portée à **380 / 380 tests réussis** ;
- continuité de lignée persistante et resolver générationnel validés ;
- ENGINE-019 + ENGINE-020 constituent désormais un bloc cohérent Mémoire/Générations.

### Version 1.31

- ENGINE-020 ouvert en Proposition / M2 ;
- 10 tests candidats ;
- total attendu 380 / 380.

### Version 1.30

- ENGINE-019 validée / M4 à 370 / 370.

### Versions antérieures

- construction progressive du Kernel, de la vie complète, de l'autonomie, de l'économie matérielle et de la cognition générique.
