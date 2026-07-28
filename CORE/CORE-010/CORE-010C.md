# CORE-010-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives de Lifecycle.

---

# 2. Responsabilité principale

Lifecycle représente la continuité temporelle d'une primitive évolutive.

---

# 3. Responsabilités autorisées

Lifecycle peut :

- organiser des States ;
- référencer des Events ;
- représenter une succession chronologique.

---

# 4. Responsabilités interdites

Lifecycle ne doit jamais :

- modifier un State ;
- produire un Event ;
- créer une primitive ;
- exécuter une logique.

---

# 5. Principe

Lifecycle répond à la question :

« Comment cette continuité a-t-elle évolué ? »

---

# 6. Validation

Lifecycle est conforme si sa responsabilité reste exclusivement descriptive.

---

# Historique

Version 1.0
