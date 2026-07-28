# CORE-003-H — Relations

> Version : 1.0
>
> Statut : Fondation
>
> Type : Relations
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les relations entre Component et les autres primitives.

---

# 2. Relations

Un Component :

- appartient à une Entity ;
- contient des Values ;
- peut porter un State ;
- peut être référencé ;
- évolue au cours du Lifecycle de son Entity ;
- peut être impliqué indirectement dans des Events.

---

# 3. Dépendances

Le Component complète l'Entity.

Les Systems interprètent les Components.

Les Events décrivent leurs évolutions.

---

# 4. Validation

Les relations sont conformes si elles respectent les responsabilités définies dans CORE.

---

# Historique

Version 1.0
