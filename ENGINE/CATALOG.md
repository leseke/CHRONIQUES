# ENGINE — Catalogue

> Version : 1.31
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
ENGINE-020  Continuité générationnelle               Proposition / M2
```

## Validation courante

```text
Base validée : 370 / 370
ENGINE-020 : +10 tests candidats
Total attendu : 380 / 380
```

## ENGINE-020

Spécification : `ENGINE/ENGINE020.md`.

Autorités : `GDB-008D v1.1`, `GDB-008G v1.2`, `GDB-004J v1.2`, `GDB-002B v1.3`.

Briques candidates :

```text
GenerationContinuityComponent
GenerationTransitionTrace
GenerationContinuityRegistry
GenerationContinuitySynchronizer
LineageWorldMemoryGenerationResolver
```

Principe : une continuité identifiée possède son propre index. Un changement de membre actif n'est accepté que s'il existe un `heritage.transmission` correspondant au Tick courant. L'index avance alors exactement de `+1`. Aucun compteur global du World ni conversion Tick-vers-génération n'est introduit.

Persistance candidate : `EntitySnapshot.GenerationContinuity` + `WorldRepository`.

QA candidate : `Engine020Tests.cs` — 10 tests couvrant création, erreurs de configuration, coexistence, avancement, idempotence, synchronisation, resolver et round-trip.

Aucun passage M4 avant validation locale.

## État des blocs

```text
ENGINE-013/014 → économie matérielle → TECH-005
ENGINE-015/016/017 → cognition autonome → TECH-006
ENGINE-018 → personnalité → 330/330
ENGINE-019 → Mémoire du Monde → 370/370
ENGINE-020 → continuité générationnelle → 380/380 attendu
```

## Frontières restantes

- démonstration multi-générations complète ;
- Type concret de Mémoire ;
- événements mondiaux autonomes complets ;
- mappings Trait/Habitude et Trait/Ambition ;
- comportements cognitifs narratifs concrets ;
- économie commerciale ;
- fairness inter-familles.

## Historique

### Version 1.31

- GDB-008D et GDB-008G rendus déterministes pour la continuité de lignée ;
- ENGINE-020 ouvert en Proposition / M2 ;
- 10 tests candidats ;
- total attendu 380 / 380.

### Version 1.30

- ENGINE-019 validée / M4 à 370 / 370.

### Versions antérieures

- construction progressive du Kernel, de la vie complète, de l'autonomie, de l'économie matérielle et de la cognition générique.
