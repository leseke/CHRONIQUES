# CORE-008-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives de la primitive Time.

---

# 2. Responsabilité principale

Time fournit un ordre chronologique.

---

# 3. Responsabilités autorisées

Time peut :

- situer un Event ;
- comparer deux instants ;
- ordonner une succession.

---

# 4. Responsabilités interdites

Time ne doit jamais :

- produire un Event ;
- modifier un State ;
- exécuter une logique ;
- représenter une règle métier.

---

# 5. Principe

Time répond uniquement à la question :

« Avant ou après ? »

---

# 6. Validation

Time est conforme si sa responsabilité reste limitée à l'ordre temporel.

---

# Historique

Version 1.0
