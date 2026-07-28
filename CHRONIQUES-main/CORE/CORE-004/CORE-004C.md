# CORE-004-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives d'une Value.

---

# 2. Responsabilité principale

Une Value représente une donnée élémentaire.

---

# 3. Responsabilités autorisées

Une Value peut :

- être stockée ;
- être lue ;
- être comparée ;
- être remplacée.

---

# 4. Responsabilités interdites

Une Value ne doit jamais :

- contenir une logique métier ;
- modifier une autre Value ;
- produire un Event ;
- prendre une décision.

---

# 5. Principe

Une Value possède toujours une seule signification.

---

# 6. Validation

Une Value est conforme si sa responsabilité reste limitée à la représentation d'une information.

---

# Historique

Version 1.0
