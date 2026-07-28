# CORE-010-G — Invariants

> Version : 1.0
>
> Statut : Fondation
>
> Type : Invariants
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les propriétés toujours vraies de Lifecycle.

---

# 2. Invariants

## Invariant 1

Lifecycle représente toujours une seule continuité.

---

## Invariant 2

Lifecycle est descriptif.

---

## Invariant 3

Lifecycle ne contient aucune logique métier.

---

## Invariant 4

Lifecycle s'appuie sur Time.

---

## Invariant 5

Lifecycle référence uniquement les éléments appartenant à une même continuité.

---

## Invariant 6

L'historique d'un Lifecycle est cumulatif.

Les nouveaux éléments complètent la continuité sans modifier les éléments historiques.

---

# 3. Validation

Toute évolution de CORE doit préserver ces invariants.

---

# Historique

Version 1.0
