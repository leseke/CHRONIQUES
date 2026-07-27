# CORE-004-E — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes applicables à toute Value.

---

# 2. Contraintes

Une Value :

- représente une seule information ;
- est atomique ;
- est indépendante de la logique métier.

---

# 3. Interdictions

Une Value ne doit jamais :

- contenir une règle ;
- contenir un comportement ;
- déclencher un Event ;
- modifier une autre Value.

---

# 4. Compatibilité

Une Value doit pouvoir être utilisée dans différents Components sans modifier sa définition.

---

# 5. Validation

Toute Value doit respecter l'ensemble de ces contraintes.

---

# Historique

Version 1.0
