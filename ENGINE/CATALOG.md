# ENGINE — Catalogue

> Version : 1.33
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
dotnet build
→ succès

dotnet test
→ 380 / 380 tests réussis
→ 0 échec
```

## Blocs consolidés

```text
ENGINE-013 / 014
→ production + circulation
→ TECH-005

ENGINE-015 / 016 / 017
→ cognition autonome générique
→ TECH-006

ENGINE-018 / 019 / 020
→ cognition durable + Mémoire + continuité générationnelle
→ TECH-007
→ AUDIT-MEMOIRE-GENERATIONS-Consolidation.md
```

## Bloc mémoire et générations

```text
PersonalityComponent
↓
Traits / Inflexions persistants

WorldMemoryComponent
↓
Anecdote → Souvenir → Légende → Tradition

GenerationContinuityComponent
↓
index de génération propre à une continuité
↓
LineageWorldMemoryGenerationResolver
↓
Mémoire évaluée à la génération de cette lignée
```

Invariants : aucun Trait concret par défaut, aucun Type concret de Mémoire, aucune mémorisation automatique des Events, aucun compteur générationnel global, aucune conversion Tick → génération.

## Frontières restantes

- démonstration multi-générations complète de bout en bout ;
- événements mondiaux autonomes complets ;
- Types concrets de Mémoire ;
- mappings Trait/Habitude et Trait/Ambition ;
- comportements cognitifs narratifs concrets ;
- économie commerciale ;
- fairness inter-familles.

ENGINE-007 reste réservé au Resource Manager.

## Historique

### Version 1.33

- consolidation MASTER-006 du jalon ENGINE-018 à ENGINE-020 ;
- TECH-007 créé ;
- audit Mémoire + Générations clos / M4 ;
- validation courante maintenue à 380 / 380 ;
- prochaine frontière : démonstration multi-générations complète.

### Version 1.32

- ENGINE-020 validée / M4 à 380 / 380.

### Version 1.30

- ENGINE-019 validée / M4 à 370 / 370.

---

Fin du document
