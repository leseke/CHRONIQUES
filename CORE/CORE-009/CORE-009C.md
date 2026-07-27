# CORE-009-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives de Space.

---

# 2. Responsabilité principale

Space fournit un référentiel de localisation.

---

# 3. Responsabilités autorisées

Space peut :

- situer une Entity ;
- situer une Relation ;
- comparer des localisations.

---

# 4. Responsabilités interdites

Space ne doit jamais :

- déplacer une Entity ;
- modifier un State ;
- produire un Event ;
- exécuter une logique.

---

# 5. Principe

Space répond uniquement à la question :

« Où ? »

---

# 6. Validation

Space est conforme si sa responsabilité reste limitée à la localisation.

---

# Historique

Version 1.0
