# CORE-001-E — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir précisément les responsabilités de la bibliothèque CORE.

CORE constitue le noyau conceptuel de Chroniques.

Sa responsabilité est de fournir les primitives universelles sur lesquelles repose l'ensemble du projet.

---

# 2. Responsabilité principale

CORE définit les concepts fondamentaux.

Ces concepts sont :

- universels ;
- indépendants des mécaniques ;
- indépendants de l'implémentation ;
- réutilisables dans toutes les bibliothèques.

---

# 3. Ce que CORE définit

CORE définit notamment :

- les primitives conceptuelles ;
- leurs responsabilités ;
- leurs relations ;
- leurs invariants ;
- leurs règles d'utilisation.

---

# 4. Ce que CORE ne définit jamais

CORE ne définit jamais :

- les règles du monde ;
- les mécaniques de gameplay ;
- les comportements des IA ;
- les interfaces utilisateur ;
- les systèmes techniques ;
- les données métier.

Ces responsabilités appartiennent aux autres bibliothèques.

---

# 5. Relations avec les autres bibliothèques

MASTER définit la vision.

STANDARDS définit les conventions.

CORE définit le langage conceptuel.

GDB décrit le monde.

ACT décrit les actions.

PLN décrit la prise de décision.

TECH implémente les concepts.

QA valide les implémentations.

---

# 6. Principe de non-duplication

Un concept défini dans CORE ne doit jamais être redéfini ailleurs.

Les autres bibliothèques le référencent.

---

# 7. Validation

CORE remplit sa mission si :

✓ chaque primitive possède une responsabilité unique ;

✓ aucune bibliothèque métier ne redéfinit une primitive ;

✓ les dépendances restent descendantes.

---

# Historique

Version 1.0

Première définition officielle des responsabilités de CORE.
