# CORE-005-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives de la primitive State.

---

# 2. Responsabilité principale

Un State représente une condition cohérente à un instant donné.

---

# 3. Responsabilités autorisées

Un State peut :

- regrouper des Values ;
- être observé ;
- être remplacé ;
- être référencé.

---

# 4. Responsabilités interdites

Un State ne doit jamais :

- prendre une décision ;
- exécuter un traitement ;
- produire un Event ;
- modifier directement un autre State.

---

# 5. Principe

Le State décrit uniquement **ce qui est**, jamais **pourquoi** cela est.

---

# 6. Validation

Un State est conforme si sa responsabilité reste limitée à la représentation d'une condition.

---

# Historique

Version 1.0
