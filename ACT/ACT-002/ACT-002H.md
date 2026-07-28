# ACT-002-H — Intent

> Version : 1.1
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# Objectif

Définir la notion d'Intent comme origine de toute action dans Chroniques.

---

# Principe

Une Action n'apparaît jamais spontanément.

Elle est toujours produite par une intention.

---

# Définition

Un Intent représente un objectif.

Il décrit ce que souhaite accomplir un acteur.

Il ne décrit pas la manière d'y parvenir.

---

# Exemples

Intent :

Se nourrir

↓

Actions possibles

Cueillir

Acheter

Voler

Cuisiner

Manger

---

Intent :

Construire une maison

↓

Fabriquer des briques

Transporter

Assembler

Construire

---

Intent :

S'enrichir

↓

Produire

Vendre

Négocier

Investir

---

# Caractéristiques

Un Intent :

- possède un objectif ;

- possède une priorité ;

- peut être abandonné ;

- peut être suspendu ;

- peut être remplacé ;

- peut être satisfait.

---

# Indépendance

Un Intent ne connaît pas :

- les Actions ;

- les Effets ;

- les Events.

Il décrit uniquement le résultat recherché.

---

# Production

Un Intent est interprété par un Planner.

Le Planner choisit une ou plusieurs Action Definitions.

---

# Contrat

Un Intent ne peut jamais modifier directement le monde.

Il produit uniquement un plan.

---

# Validation

Un Intent est valide si :

✓ il décrit un objectif ;

✓ il est indépendant des implémentations ;

✓ plusieurs plans peuvent le satisfaire.

---

# Historique

## Version 1.1

- en-tête aligné sur le format des autres sections d'ACT-002 (ajout de Statut, Type, Bibliothèque). Corrige le constat ACT-C03.

## Version 1.0

- Création du document.
