# CORE-002-D — Composition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir comment une Entity est construite.

---

# 2. Principe

Une Entity est définie par sa composition.

Elle n'est jamais définie par héritage métier.

---

# 3. Composition

Une Entity est composée d'un ensemble de Components.

Chaque Component apporte une responsabilité précise.

---

# 4. Évolution

Les Components peuvent :

- être ajoutés ;
- être retirés ;
- être remplacés ;
- évoluer.

Ces opérations n'affectent pas l'identité de l'Entity.

---

# 5. Responsabilités

L'Entity :

- compose.

Les Components :

- décrivent.

Les Systems :

- interprètent.

Cette séparation est obligatoire.

---

# 6. Minimalisme

Une Entity ne contient que ce qui est nécessaire à son identification et à sa composition.

Toute logique appartient aux Systems.

---

# 7. Compatibilité

Une Entity reste valide même si sa composition évolue au cours de son Lifecycle.

---

# 8. Validation

Une composition est conforme si :

✓ chaque Component possède une responsabilité unique ;

✓ aucune logique métier n'est portée par l'Entity ;

✓ la composition reste cohérente.

---

# Historique

Version 1.0

Première définition officielle de la composition d'une Entity.
