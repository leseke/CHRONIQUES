# CORE-007-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes applicables à la primitive Event.

---

# 2. Contraintes

Un Event :

- représente un fait unique ;
- est immuable ;
- possède une temporalité.

---

# 3. Interdictions

Un Event ne doit jamais :

- modifier une Entity ;
- modifier un State ;
- modifier une Relation ;
- exécuter une logique.

---

# 4. Compatibilité

Tout modèle événementiel utilisé dans Chroniques doit respecter ces contraintes.

---

# 5. Validation

Toute implémentation doit préserver ces propriétés.

---

# Historique

Version 1.0
