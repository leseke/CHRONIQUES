# ACT — Action Library

> **Version :** 1.2
>
> **Statut :** Foundation
>
> **Bibliothèque :** ACT
>
> **Dépendances :** MASTER, GDB
>
> **Bibliothèques utilisatrices :** TECH, QA, UX
>
> **Domaines fonctionnels utilisateurs (non-bibliothèques) :** intelligence artificielle, conception du gameplay

---

# 1. Mission

La bibliothèque **ACT** définit le langage universel des actions de Chroniques.

Elle décrit **ce que les acteurs peuvent entreprendre**, indépendamment de leur nature, de leur profession, de leur culture ou du contexte dans lequel ils évoluent.

ACT ne décrit ni le monde, ni son implémentation technique.

Elle décrit uniquement les possibilités d'action.

---

# 2. Objectifs

ACT poursuit plusieurs objectifs fondamentaux :

- normaliser toutes les actions du jeu ;
- fournir une référence unique au gameplay ;
- éviter la duplication des mécaniques ;
- permettre la réutilisation des systèmes ;
- servir de base au moteur de simulation ;
- fournir une spécification exploitable par les développeurs ;
- faciliter les tests et la validation.

---

# 3. Position dans Chroniques

```
MASTER
        │
        ▼
      GDB
        │
        ▼
      ACT
        │
        ▼
      TECH
        │
        ▼
      CODE
```

Chaque couche possède une responsabilité unique.

MASTER définit la vision.

GDB décrit le monde.

ACT décrit les actions.

TECH implémente ces actions.

Le code exécute TECH.

---

# 4. Principes

Une action possède toujours :

- un acteur ;
- une ou plusieurs cibles ;
- un contexte ;
- des conditions ;
- un déroulement ;
- des conséquences.

Une action peut :

- réussir ;
- échouer ;
- être interrompue ;
- produire de nouveaux événements.

---

# 5. Ce que contient ACT

ACT contient :

- les règles universelles de l'action ;
- les modèles d'action ;
- les patterns de gameplay ;
- les verbes fondamentaux ;
- les interactions entre actions ;
- les événements générés ;
- les références techniques.

---

# 6. Ce que ACT ne contient pas

ACT ne décrit jamais :

- les objets du monde (GDB) ;
- les données techniques (TECH) ;
- le code source ;
- les graphismes ;
- les dialogues ;
- le lore.

---

# 7. Architecture

La structure ci-dessous distingue ce qui existe aujourd'hui de ce qui reste à créer. Voir ACT/CATALOG.md pour l'état exact et à jour.

```
ACT/

README.md
CATALOG.md

ACT-001 Fondements               (existant)
ACT-002 Modèle universel         (existant)
ACT-003 Cycle de vie             (planifié, non créé)
ACT-004 Acteurs                  (planifié, non créé)
ACT-005 Cibles                   (planifié, non créé)
ACT-006 Conditions                (planifié, non créé)
ACT-007 Conséquences             (planifié, non créé)
ACT-008 Taxonomie                (planifié, non créé)
ACT-009 Composition              (planifié, non créé)
ACT-010 Événements               (planifié, non créé)

PATTERNS/                        (planifié, non créé)

VERBS/                           (planifié, non créé)
```

---

# 8. Les quatre niveaux

Toute action appartient à quatre niveaux.

Principe

↓

Pattern

↓

Verbe

↓

Action exécutée

Exemple :

Influence

↓

Persuasion

↓

Convaincre

↓

Paul convainc Marie.

Les niveaux Pattern et Verbe sont définis par ce document dès aujourd'hui, mais leur bibliothèque de référence (PATTERNS/, VERBS/) n'est pas encore créée : voir ACT/CATALOG.md.

---

# 9. Philosophie

Le gameplay ne doit jamais être conçu à partir des métiers, des factions ou des systèmes.

Le gameplay est construit à partir d'actions universelles réutilisables.

Les domaines du monde utilisent ces actions sans les modifier.

---

# 10. Règle fondamentale

> Toute interaction observable dans Chroniques doit pouvoir être expliquée par une combinaison de verbes documentés dans ACT.

---

# 11. Impact technique

Cette bibliothèque sert directement à :

- la conception du gameplay ;
- l'architecture du moteur ;
- les systèmes IA ;
- la génération d'événements ;
- les tests QA ;
- la documentation développeur.

Parmi ces usages, seuls TECH, QA et UX sont des bibliothèques du dépôt au sens de MASTER-003. Les systèmes IA et la conception du gameplay sont des domaines fonctionnels qui consomment ACT sans lui correspondre une bibliothèque documentaire dédiée.

---

# 12. Évolution

Toute nouvelle mécanique doit respecter les principes suivants :

1. ne pas dupliquer un verbe existant ;
2. privilégier la réutilisation ;
3. documenter le pattern associé ;
4. conserver la compatibilité avec les systèmes existants ;
5. mettre à jour CATALOG.

---

# 13. Bibliothèques liées

MASTER → Vision

GDB → Monde

TECH → Implémentation

QA → Validation

UX → Interface

LORE → Histoire

---

# 14. Statut

ACT constitue la référence officielle du gameplay de Chroniques.

Toute nouvelle mécanique doit être documentée dans ACT avant son implémentation dans TECH.

---

# Historique

## Version 1.2

- fichier renommé `Readme.md` → `readme.md` pour aligner la casse sur les autres bibliothèques de premier niveau (TECH, QA, UX, LORE, PROD, ART, AUDIO, MKT, GDB). Corrige GLOBAL-C01.

## Version 1.1

- correction du champ `Bibliothèque` de l'en-tête, qui indiquait « Gameplay » au lieu de « ACT » ;
- distinction explicite entre bibliothèques utilisatrices (TECH, QA, UX) et domaines fonctionnels utilisateurs (IA, conception du gameplay), qui n'étaient pas identifiés comme tels ;
- section 7 et section 8 mises à jour pour indiquer explicitement quels chapitres et dossiers existent réellement, par opposition à ceux qui sont seulement planifiés.

Corrige les constats ACT-C01 et ACT-C04.

## Version 1.0

- Création du document.
