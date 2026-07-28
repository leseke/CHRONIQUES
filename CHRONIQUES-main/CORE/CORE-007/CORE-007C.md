# CORE-007-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives de la primitive Event.

---

# 2. Responsabilité principale

Un Event représente un changement observé dans le monde.

---

# 3. Responsabilités autorisées

Un Event peut :

- documenter un changement ;
- être horodaté ;
- être référencé ;
- être historisé.

---

# 4. Responsabilités interdites

Un Event ne doit jamais :

- modifier un State ;
- créer une Entity ;
- prendre une décision ;
- exécuter un traitement.

---

# 5. Principe

Un Event décrit **ce qui s'est produit**.

Il ne décrit jamais **comment** cela s'est produit.

---

# 6. Validation

Un Event est conforme si sa responsabilité reste exclusivement descriptive.

---

# Historique

Version 1.0
