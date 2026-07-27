# CORE-007-D — Composition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir la composition conceptuelle d'un Event.

---

# 2. Principe

Un Event représente un fait ayant eu lieu.

Une fois créé, il devient immuable.

---

# 3. Composition

Un Event peut être composé de :

- participants ;
- References ;
- Values ;
- Time.

CORE n'impose aucun format particulier.

---

# 4. Immutabilité

Un Event ne peut jamais être modifié.

Toute évolution du monde produit un nouvel Event.

---

# 5. Traçabilité

Les Events constituent l'historique observable de la simulation.

Ils peuvent être conservés afin de reconstruire l'évolution du monde.

---

# 6. Validation

Un Event est conforme si :

✓ il est immuable ;

✓ il représente un fait unique ;

✓ il peut être référencé.

---

# Historique

Version 1.0
