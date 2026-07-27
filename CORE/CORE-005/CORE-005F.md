# CORE-005-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes applicables à la primitive State.

---

# 2. Contraintes

Un State :

- représente une seule condition ;
- est composé de Values ;
- reste descriptif.

---

# 3. Interdictions

Un State ne doit jamais :

- contenir un algorithme ;
- produire un Event ;
- prendre une décision ;
- modifier directement un autre State.

---

# 4. Compatibilité

Un State doit pouvoir évoluer sans modifier la définition du Component auquel il appartient.

---

# 5. Validation

Toute implémentation doit respecter ces contraintes.

---

# Historique

Version 1.0
