# ENGINE-021 — Démonstration multi-générations intégrée

> Version : 1.1
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE

## Objectif

Valider par intégration la continuité d'une Chronique sur deux transmissions successives sans ajouter de nouveau framework.

## Preuve candidate

Le scénario compose les implémentations validées de l'autonomie, du vieillissement, de l'héritage, de `LifeSession`, de la continuité générationnelle et de la Mémoire du Monde.

Il vérifie en une seule exécution :

```text
A → B → C
GenerationIndex : 0 → 1 → 2
Mémoire : Anecdote → Souvenir → Légende
autonomie de B après A
autonomie de C après B
```

Un second test rejoue le même état initial et compare les traces générationnelles et mémorielles pour confirmer le déterminisme.

La règle de Mémoire utilisée est uniquement une règle factice de QA.

## Validation candidate

`Engine021MultiGenerationIntegrationTests.cs` : **2 tests**.

```text
Base validée : 380 / 380
Total attendu : 382 / 382
```

Aucun passage M4 avant validation locale.
