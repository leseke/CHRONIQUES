# ENGINE — Catalogue

> Version : 1.34
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
ENGINE-021  Démonstration multi-générations          Proposition / M2
```

## Validation courante

```text
Base validée : 380 / 380
ENGINE-021 : +2 tests d'intégration candidats
Total attendu : 382 / 382
```

## ENGINE-021

Le lot n'ajoute aucun framework. Il compose les briques validées pour prouver :

```text
A → B → C
+
autonomie après chaque succession
+
GenerationIndex 0 → 1 → 2
+
Mémoire Anecdote → Souvenir → Légende
+
déterminisme du scénario complet
```

QA : `Engine021MultiGenerationIntegrationTests.cs`.

Aucun passage M4 avant validation locale.

## Blocs consolidés

```text
ENGINE-013 / 014 → TECH-005
ENGINE-015 / 016 / 017 → TECH-006
ENGINE-018 / 019 / 020 → TECH-007
```

## Frontières restantes

- validation locale ENGINE-021 ;
- événements mondiaux autonomes complets ;
- Types concrets de Mémoire ;
- mappings Trait/Habitude et Trait/Ambition ;
- économie commerciale ;
- fairness inter-familles.

ENGINE-007 reste réservé au Resource Manager.

## Historique

### Version 1.34

- ENGINE-021 ouvert en Proposition / M2 ;
- preuve multi-générations candidate ajoutée ;
- 2 tests d'intégration ;
- total attendu : 382 / 382.

### Version 1.33

- consolidation MASTER-006 du jalon ENGINE-018 à ENGINE-020 ;
- validation courante : 380 / 380.

---

Fin du document
