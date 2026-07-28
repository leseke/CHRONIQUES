# ACT-002-G — Outcome

> Version : 1.1
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# Objectif

Définir la notion d'Outcome comme résultat d'une action exécutée dans Chroniques.

L'Outcome relie le Modèle d'exécution à l'intention qui l'a produit : il indique ce qui a réellement eu lieu.

---

# Principe

Une Action ne réussit jamais par défaut.

Son exécution produit un Outcome, qui décrit ce qui s'est réellement passé, indépendamment de ce qui était souhaité.

L'écart entre l'intention et l'Outcome est la source des histoires émergentes.

---

# Définition

Un Outcome représente le résultat observé d'une action exécutée.

Il est produit par le Modèle d'exécution, une fois la résolution effectuée.

Il précède la production des Effets et des Events.

---

# Formes

Un Outcome prend l'une des formes suivantes :

- Réussite ;

- Réussite partielle ;

- Échec ;

- Interruption.

La réussite partielle est la forme la plus féconde : l'acteur obtient son objectif, mais pas comme prévu, ou à un prix imprévu.

---

# Exemples

Action :

Convaincre

↓

Outcome possible

Réussite

Réussite partielle

Échec

---

Action :

Voler

↓

Outcome possible

Réussite

Échec

Interruption

---

# Caractéristiques

Un Outcome :

- découle d'une résolution, jamais d'un choix arbitraire ;

- est déterministe à graine égale ;

- précède les Effets ;

- ne modifie pas lui-même le monde.

---

# Indépendance

Un Outcome ne connaît pas :

- l'Intent d'origine ;

- les Effets qu'il déclenchera ;

- les Events publiés ensuite.

Il décrit uniquement ce qui a eu lieu.

---

# Production

Un Outcome est produit par le Modèle d'exécution.

Il est ensuite transmis à la phase de production des Effets, qui seule modifie le monde.

---

# Contrat

Un Outcome ne peut jamais modifier directement le monde.

Il constitue une donnée de résultat, consommée par les Effets.

---

# Validation

Un Outcome est valide si :

✓ il décrit un résultat observé ;

✓ il est reproductible à graine égale ;

✓ il précède toute modification du monde.

---

# Historique

## Version 1.1

- en-tête aligné sur le format des autres sections d'ACT-002 (ajout de Statut, Type, Bibliothèque). Corrige le constat ACT-C03.

## Version 1.0

- Création du document.
