# CORE-008-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes de la primitive Time.

---

# 2. Contraintes

Time :

- ordonne les Instants ;
- permet de situer les Events ;
- reste indépendant de toute unité.

---

# 3. Interdictions

Time ne doit jamais :

- produire un Event ;
- modifier un State ;
- représenter une règle métier ;
- dépendre d'une implémentation technique.

---

# 4. Compatibilité

Toute représentation temporelle utilisée dans Chroniques doit respecter ces contraintes.

---

# 5. Validation

Toute implémentation doit préserver le caractère conceptuel de Time.

---

# Historique

Version 1.0
