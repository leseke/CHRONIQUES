# CORE-005-H — Relations

> Version : 1.0
>
> Statut : Fondation
>
> Type : Relations
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les relations entre State et les autres primitives.

---

# 2. Relations

Un State :

- appartient à un Component ;
- est composé de Values ;
- peut être référencé ;
- peut évoluer au cours du Lifecycle de son Entity ;
- peut être modifié par l'action d'un System ;
- peut être concerné par un Event.

---

# 3. Dépendances

Le State relie les données (Values) à leur évolution (Events).

Il constitue le point d'observation principal de la simulation.

---

# 4. Validation

Les relations sont conformes si elles respectent les responsabilités définies dans CORE.

---

# Historique

Version 1.0
