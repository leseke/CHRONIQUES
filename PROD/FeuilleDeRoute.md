# Chroniques — Feuille de Route V2.2

> Version : 2.2
> Statut : Officiel
> Type : Roadmap
> Maturité : 2
> Bibliothèque : PROD

---

# Vision

Chroniques n'est pas simplement un jeu.

Chroniques est un moteur de simulation narratif sur lequel un jeu est construit.

Le jeu n'est que la première utilisation de ce moteur.

Le développement du moteur suit une approche **Documentation First**, où chaque composant est spécifié avant d'être implémenté.

---

# Ce qui change par rapport à la V2.1

La V2.2 formalise l'organisation documentaire désormais adoptée par le projet.

Les principales évolutions sont :

- création officielle de la bibliothèque **ENGINE** ;
- intégration du processus **Documentation → Implémentation → Tests → TECH** ;
- distinction explicite entre les spécifications d'architecture (ENGINE) et la documentation technique (TECH) ;
- ajout d'une phase d'infrastructure moteur avant le développement des systèmes de gameplay.

Aucun objectif fonctionnel des versions précédentes n'est modifié.

---

# Les cinq principes

## 1. Le code suit les spécifications

Aucune fonctionnalité n'est développée sans être reliée à une spécification existante.

Le développement suit la hiérarchie documentaire suivante :

```
MASTER
    ↓
CORE
    ↓
ACT
    ↓
ENGINE
    ↓
Implémentation
    ↓
Tests
    ↓
TECH
```

Chaque niveau dépend uniquement des niveaux précédents.

---

## 2. Documentation vivante

Une fonctionnalité est terminée uniquement lorsqu'elle est :

- spécifiée ;
- implémentée ;
- testée ;
- documentée dans TECH.

---

## 3. Data-driven

Le moteur ne contient aucune donnée métier.

Objets, personnages, métiers, bâtiments, événements, villes, compétences, religions ou dialogues sont entièrement définis par des données externes.

Le moteur ne connaît que leur structure.

---

## 4. Déterminisme

À état identique et entrées identiques, la simulation produit toujours exactement le même résultat.

Cette propriété garantit :

- des sauvegardes fiables ;
- les replays ;
- les tests reproductibles ;
- le futur multijoueur déterministe.

---

## 5. Séparation des responsabilités

Chaque bibliothèque possède un rôle clairement défini.

- **MASTER** : vision et architecture globale.
- **CORE** : concepts fondamentaux.
- **ACT** : comportements et moteur d'actions.
- **ENGINE** : architecture interne du moteur.
- **TECH** : documentation générée à partir du code réellement implémenté.

Aucune bibliothèque ne duplique la responsabilité d'une autre.

---

# Architecture documentaire

Le projet est organisé autour des bibliothèques suivantes.

```
MASTER
│
├── Vision
├── Architecture
└── Principes

        │
        ▼

CORE
│
├── Monde
├── Entités
├── États
├── Valeurs
└── Relations

        │
        ▼

ACT
│
├── Intent
├── Plan
├── Action
└── Outcome

        │
        ▼

ENGINE
│
├── EventBus
├── Scheduler
├── Simulation Loop
├── Systems
├── Persistence
└── Infrastructure

        │
        ▼

CHRONIQUES-ENGINE
(Code)

        │
        ▼

TECH
(Documenté à partir du code)
```

---

# Architecture générale

```
Chroniques
│
├── Simulation
│      Gameplay intégral
│
├── Content
│      Données externes
│
├── Rendering
│      Adaptateur Godot
│
├── Tools
│      Outils de développement
│
├── Documentation
│
└── Tests
```

La simulation ignore totalement la manière dont elle est affichée.

Le moteur de rendu ne fait que représenter l'état courant du monde.

---

# Architecture moteur

Le moteur est développé progressivement autour des composants suivants.

```
World
│
├── Kernel
├── Scheduler
├── EventBus
├── Simulation Loop
├── Systems
├── Action Pipeline
├── Persistence
├── Serialization
└── Resource Management
```

Chaque composant possède une spécification dédiée dans la bibliothèque ENGINE avant son implémentation.

---

# Couche Simulation

Toute la logique métier est développée en C# pur.

La couche Simulation implémente directement les spécifications :

- CORE
- ACT
- ENGINE

Elle reste indépendante :

- du moteur graphique ;
- de l'interface utilisateur ;
- des outils.

---

# Feuille de route par versions

L'objectif directeur reste le critère de sortie de la Phase 1 de MASTER-005 :

> Une vie entière jouable, du premier choix au dernier.

Les versions suivantes y conduisent progressivement.

---

# v0.1 — Le noyau

Construction des fondations du moteur.

## Infrastructure

- Entity
- Component
- State
- Value
- Relation
- World
- Tick
- Time
- Lifecycle
- RNG déterministe
- Sérialisation JSON

## Documentation

- MASTER
- CORE

## Validation

- tests unitaires du Kernel
- sauvegarde/restauration déterministe
- World vide entièrement reproductible

---

# v0.2 — Infrastructure de simulation

Construction de l'infrastructure permettant au monde de vivre.

## ENGINE

- EventBus
- Scheduler
- Simulation Loop
- Systems
- Persistence
- Serialization
- World Lifecycle

## Simulation

- premier personnage
- besoins
- vieillissement
- cycle de vie
- évolution temporelle

## Validation

Un personnage peut :

- naître ;
- vivre ;
- voir évoluer ses besoins ;
- vieillir ;
- mourir ;

sans aucun moteur graphique.

Toute la simulation reste déterministe.

---

# v0.3 — Une vie entière

Atteint le critère de sortie de la Phase 1 de MASTER-005.

## ACT

- Intent
- Plan
- Action
- Outcome
- Effects
- Events

## Simulation

- relations
- mémoire
- compétences
- héritage minimal

## Rendering

Première interface Godot jouable.

## Validation

Le joueur peut :

- vivre une vie complète ;
- mourir ;
- poursuivre avec son héritier.

---

# v0.4 — Le monde vivant

Correspond à la Phase 3 de MASTER-005.

Ajout :

- PNJ autonomes
- économie autonome
- mémoire du monde
- événements dynamiques

Validation :

Le monde continue d'évoluer sur plusieurs générations sans intervention du joueur.

---

# v0.5 — La profondeur

Correspond à la Phase 4 de MASTER-005.

Ajout :

- économie avancée
- métiers
- médecine
- justice
- crime
- politique
- religion
- combat

Validation :

Trois vies différentes produisent trois histoires profondément différentes.

---

# v0.6 — Les outils

Ajout :

- éditeur de contenu
- debugger de simulation
- inspection du monde
- outils de production

---

# v1.0 — Première alpha

Le moteur est considéré comme stable.

Objectifs :

- boucle complète
- sauvegarde versionnée
- équilibrage
- interface aboutie
- direction artistique
- stabilité

---

# Workflow de développement

Toute fonctionnalité suit obligatoirement le cycle suivant.

```
MASTER

↓

CORE

↓

ACT

↓

ENGINE

↓

Implémentation

↓

Tests

↓

TECH

↓

Validation

↓

Intégration
```

Aucun document TECH ne décrit une fonctionnalité inexistante.

Aucun code n'est développé sans spécification validée.

---

# Objectif long terme

Construire un moteur de simulation capable de faire vivre un monde autonome où :

- chaque personnage poursuit ses propres objectifs ;
- les relations évoluent naturellement ;
- l'économie fonctionne indépendamment du joueur ;
- les générations se succèdent ;
- les événements émergent de la simulation.

Le jeu n'est que la première utilisation de ce moteur.

L'objectif ultime est de disposer d'un moteur suffisamment générique pour supporter plusieurs expériences interactives reposant sur la même architecture de simulation.

---

# Historique

## Version 2.2

- création officielle de la bibliothèque ENGINE ;
- intégration de l'architecture documentaire complète ;
- formalisation du workflow MASTER → CORE → ACT → ENGINE → Code → Tests → TECH ;
- ajout de l'architecture moteur (EventBus, Scheduler, Simulation Loop, Systems, Persistence, Serialization, World Lifecycle) ;
- clarification du rôle de chaque bibliothèque documentaire ;
- restructuration de la v0.2 autour de l'infrastructure moteur avant les systèmes de gameplay ;
- maintien des objectifs fonctionnels des versions précédentes.

## Version 2.1

- suppression de la section « Choix techniques (ADR-002) » au profit de références vers ADR-002 ;
- inversion des versions v0.4 et v0.5 afin de respecter MASTER-005 ;
- ajout de l'en-tête conforme à MASTER-004.

## Version 2.0

- remplace la V1 ;
- intégration des décisions d'ADR-002 ;
- alignement de la feuille de route sur MASTER-005.
