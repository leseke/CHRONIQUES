# CORE-000A — Mission

> Version : 1.1
>
> Statut : Fondation
>
> Type : Mission
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir la mission, le rôle et la position de la bibliothèque CORE au sein de l'architecture documentaire de Chroniques.

Ce document constitue le point d'entrée officiel de la bibliothèque CORE.

---

# 2. Mission

CORE est le Kernel documentaire de Chroniques.

Il définit les concepts fondamentaux, les primitives conceptuelles, les règles de structuration et les invariants utilisés par l'ensemble du projet.

CORE ne décrit aucun domaine métier.

Son rôle est de fournir un langage commun à toutes les bibliothèques spécialisées.

---

# 3. Portée

CORE-000 décrit :

- la mission de CORE ;
- son périmètre ;
- sa hiérarchie documentaire ;
- son rôle dans l'architecture globale.

CORE-000 ne définit pas les primitives elles-mêmes.

Les primitives sont définies dans les séries CORE dédiées.

---

# 4. Hiérarchie documentaire

CORE constitue la source canonique de tous les concepts fondamentaux de Chroniques.

Toutes les autres bibliothèques reposent sur CORE.

Hiérarchie documentaire :

```text
CORE
├── GDB
├── ACT
├── TECH
├── QA
├── UX
├── LORE
├── PROD
├── ART
└── AUDIO
```

Une bibliothèque spécialisée peut :

- spécialiser un concept CORE ;
- appliquer un concept CORE ;
- enrichir un concept CORE dans son domaine.

Une bibliothèque spécialisée ne peut jamais :

- redéfinir une primitive CORE ;
- contredire une définition CORE ;
- modifier une règle fondamentale définie par CORE.

En cas de divergence documentaire, CORE prévaut.

---

# 5. Responsabilités

CORE est responsable de :

- la définition des primitives ;
- la cohérence conceptuelle ;
- les relations fondamentales entre concepts ;
- les règles générales de modélisation ;
- les conventions communes à l'ensemble du projet.

Les bibliothèques spécialisées sont responsables uniquement de leur domaine.

---

# 6. Public

Ce document s'adresse :

- aux architectes ;
- aux concepteurs ;
- aux développeurs ;
- aux auteurs de bibliothèques ;
- aux rédacteurs d'ADR ;
- à toute personne produisant ou faisant évoluer la documentation Chroniques.

---

# 7. Références

Cette série est liée notamment à :

- CORE-000 (Fondation)
- CORE-001 et séries suivantes
- ADR de gouvernance documentaire

---

# Historique

## Version 1.1

- clarification de la mission de CORE ;
- formalisation de la hiérarchie documentaire ;
- définition du caractère canonique de CORE ;
- clarification des responsabilités des bibliothèques spécialisées ;
- ajout des règles de dépendance documentaire.

## Version 1.0

- Création du document.
