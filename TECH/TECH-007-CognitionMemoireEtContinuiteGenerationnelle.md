# TECH-007 — Cognition durable, Mémoire et continuité générationnelle

> Version : 1.0
> Statut : Validé
> Maturité : 4
> Bibliothèque : TECH
> Validation : 380 / 380 tests réussis

## Périmètre

Ce document consolide l'implémentation validée de :

```text
ENGINE-018 — Personnalité générique minimale
ENGINE-019 — Mémoire du Monde minimale
ENGINE-020 — Continuité générationnelle explicite
```

## Personnalité

Le moteur persiste des Traits génériques avec Valeur, Poids de référence et Inflexions causales. Il sait stabiliser un Trait vers sa référence et appliquer des Inflexions légères ou profondes à partir de règles injectées.

Aucun Trait concret ni mapping Trait/Habitude ou Trait/Ambition n'est fourni par défaut.

## Mémoire du Monde

Chaque élément narratif de mémoire est porté par une Entity avec `WorldMemoryComponent`.

Le moteur applique les paliers :

```text
Anecdote → Souvenir → Légende → Tradition
```

Les qualifications de significativité, liaison, transmission, influence régionale, contradiction et pratique restent fournies par des règles concrètes. ENGINE n'invente aucun score universel.

## Continuité générationnelle

Une continuité identifiée possède son propre `GenerationIndex` persistant et son `CurrentMemberId`.

```text
continuité L : A
↓
heritage.transmission A → B
↓
adoption effective de B
↓
GenerationIndex(L) + 1
```

Une mort quelconque du World ne change jamais automatiquement la génération d'une lignée.

`LineageWorldMemoryGenerationResolver` expose cet index à ENGINE-019 sans mutation.

## Persistance

`WorldRepository` persiste désormais notamment :

```text
PersonalityComponent
WorldMemoryComponent
GenerationContinuityComponent
```

Les règles, resolvers et autres services runtime restent injectés.

## Frontières

Ce bloc n'introduit pas :

- Trait métier concret ;
- mapping psychologique concret ;
- Type concret de Mémoire ;
- compteur générationnel global ;
- conversion Tick → génération ;
- événement mondial autonome complet ;
- copie automatique de Components entre générations.

## Validation

```text
ENGINE-018 → 330 / 330
ENGINE-019 → 370 / 370
ENGINE-020 → 380 / 380
```

Validation courante consolidée : **380 / 380**.

---

Fin du document
