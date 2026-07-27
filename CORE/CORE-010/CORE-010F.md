# CORE-010-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes applicables à Lifecycle.

---

# 2. Contraintes

Lifecycle :

- représente une seule continuité ;
- s'appuie sur Time ;
- organise States et Events.

---

# 3. Interdictions

Lifecycle ne doit jamais :

- modifier une primitive ;
- produire un Event ;
- produire un State ;
- contenir une logique métier.

---

# 4. Compatibilité

Toute implémentation doit respecter les responsabilités définies par CORE.

---

# 5. Validation

Les contraintes sont conformes si Lifecycle demeure purement descriptif.

---

# Historique

Version 1.0
