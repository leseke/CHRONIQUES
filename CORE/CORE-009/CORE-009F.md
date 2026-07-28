# CORE-009-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes applicables à la primitive Space.

---

# 2. Contraintes

Space :

- fournit un référentiel de localisation ;
- permet de situer les éléments qui possèdent une existence spatiale ;
- reste indépendant de toute représentation géométrique.

---

# 3. Interdictions

Space ne doit jamais :

- définir une géométrie ;
- imposer un système de coordonnées ;
- imposer une dimension ;
- contenir une logique métier ;
- provoquer une évolution.

---

# 4. Compatibilité

Toute représentation spatiale utilisée dans Chroniques doit respecter ces contraintes.

---

# 5. Validation

Toute implémentation doit préserver le caractère conceptuel de Space.

---

# Historique

Version 1.0
