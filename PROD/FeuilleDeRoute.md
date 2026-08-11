# Chroniques — Feuille de Route V2.3

> Version : 2.3
> Statut : Officiel
> Type : Roadmap
> Maturité : 2
> Bibliothèque : PROD

---

# Vision

Chroniques n'est pas simplement un jeu.

Chroniques est un moteur de simulation narratif sur lequel un jeu est construit.

Le jeu n'est que la première utilisation de ce moteur.

Le développement suit une approche **Documentation First** où chaque règle ou architecture structurante est définie dans sa bibliothèque d'autorité avant son implémentation, sauf documentation ENGINE explicitement rétroactive d'un code historique déjà existant.

---

# Ce qui change par rapport à la V2.2

La V2.3 aligne la feuille de route sur l'architecture documentaire et moteur réellement adoptée.

Principales corrections :

- ajout explicite de **GDB** dans la hiérarchie de développement ;
- remplacement de l'ancien concept d'EventBus par le **journal `World.Events`** réellement implémenté ;
- consolidation de **Simulation Loop** avec le Scheduler dans ENGINE-003 ;
- consolidation de **Serialization** avec Persistence dans ENGINE-005 ;
- clarification de la frontière entre **mémoire technique de ressources** et **Mémoire du Monde** ;
- retrait du terme ambigu « mémoire » de la cible v0.3 ;
- maintien de la **Mémoire du Monde** dans v0.4, avec le monde vivant ;
- mise à jour de l'état de v0.3 avec ENGINE-008 implémenté et validé.

Les objectifs directeurs restent inchangés : parvenir d'abord à une vie entière jouable, puis à un monde autonome vivant sur plusieurs générations.

---

# Les cinq principes

## 1. Le code suit les spécifications

Aucune fonctionnalité structurante n'est développée sans être reliée à une spécification existante.

La hiérarchie de référence est :

```text
MASTER
↓
CORE
↓
GDB
↓
ACT
↓
ENGINE
↓
CHRONIQUES-ENGINE
↓
Tests
↓
TECH
```

Chaque niveau respecte les autorités des niveaux précédents.

---

## 2. Documentation vivante

Une fonctionnalité n'est considérée comme terminée que lorsqu'elle est :

- spécifiée ;
- implémentée ;
- compilée ;
- testée ;
- validée ;
- documentée dans TECH lorsque le lot est suffisamment stable.

---

## 3. Data-driven

Le moteur ne doit pas contenir les données métier spécifiques du jeu lorsqu'elles peuvent être externalisées.

Objets, personnages, métiers, bâtiments, événements, villes, compétences, religions ou dialogues ont vocation à être définis par des données externes.

Le moteur connaît leurs structures et leurs contrats, pas leur contenu final.

---

## 4. Déterminisme

À état identique, seed identique, entrées identiques et ordre de Systems identique, la simulation produit le même résultat.

Cette propriété soutient notamment :

- sauvegardes fiables ;
- replays ;
- tests reproductibles ;
- diagnostic ;
- futur multijoueur déterministe si cette direction est retenue.

---

## 5. Séparation des responsabilités

Chaque bibliothèque possède un rôle distinct.

- **MASTER** : gouvernance et architecture documentaire globale ;
- **CORE** : primitives conceptuelles fondamentales ;
- **GDB** : règles et modèles de simulation ;
- **ACT** : contrats d'Intent, Plan, Action, Outcome et concepts associés ;
- **ENGINE** : architecture interne attendue du moteur ;
- **CHRONIQUES-ENGINE** : implémentation exécutable ;
- **TECH** : documentation de l'implémentation réellement obtenue après validation.

Aucune bibliothèque ne doit redéfinir silencieusement l'autorité d'une autre.

---

# Architecture documentaire

```text
MASTER
│
├── Gouvernance
├── Architecture documentaire
└── Principes

        │
        ▼

CORE
│
├── Entity
├── Component
├── State
├── Value
├── Relation
├── Event
└── primitives fondamentales

        │
        ▼

GDB
│
├── Monde
├── Habitants
├── Relations
├── Compétences
├── Économie
├── Transmission
└── règles de simulation

        │
        ▼

ACT
│
├── Intent
├── Planner / Plan
├── Action
├── Outcome
└── contrats d'exécution

        │
        ▼

ENGINE
│
├── Kernel
├── World.Events
├── Scheduler / boucle de simulation
├── Systems
├── Action Pipeline
├── Persistence / Serialization
└── infrastructure

        │
        ▼

CHRONIQUES-ENGINE
(Code)

        │
        ▼

Tests

        │
        ▼

TECH
(Documente l'implémentation validée)
```

---

# Architecture générale du moteur

```text
Chroniques
│
├── Simulation
│      Logique déterministe en C# pur
│
├── Content
│      Données externes
│
├── Rendering
│      Adaptateurs de rendu
│
├── Tools
│      Outils de développement
│
├── Documentation
│
└── Tests
```

La couche Simulation ignore la manière dont elle est affichée.

Le rendu représente l'état courant sans devenir une source de vérité métier.

---

# Architecture moteur actuelle

Le moteur se développe autour des responsabilités suivantes :

```text
World
│
├── Kernel
├── World.Events
├── Scheduler / Simulation Loop
├── Systems
├── Action Pipeline
├── Persistence / Serialization
└── Resource Management futur
```

## World.Events

`World.Events` est un journal d'observabilité.

Il ne constitue pas un EventBus Publish/Subscribe entre Systems.

Les Systems observent l'état du World pour décider d'agir.

## Scheduler / Simulation Loop

La boucle de simulation actuellement implémentée est portée par le Scheduler et documentée par ENGINE-003.

Aucune séparation artificielle n'est créée tant que le code ne matérialise pas deux responsabilités indépendantes.

## Persistence / Serialization

La persistance et la sérialisation sont actuellement documentées ensemble par ENGINE-005 car elles partagent le même ensemble de contrats.

## Resource Management

ENGINE-007 reste réservé à un futur Resource Manager technique.

Le mot « mémoire » dans ce contexte désigne éventuellement la mémoire technique, le cache ou la durée de vie des ressources. Il ne désigne pas la **Mémoire du Monde** définie par la GDB.

---

# Feuille de route par versions

L'objectif directeur reste le critère de sortie de la Phase 1 de MASTER-005 :

> Une vie entière jouable, du premier choix au dernier, avec continuité par héritage.

---

# v0.1 — Le noyau

Construction des fondations du moteur.

## Infrastructure

- Entity ;
- Component ;
- State ;
- Value ;
- Relation ;
- World ;
- Tick ;
- Time ;
- Lifecycle ;
- RNG déterministe ;
- première sérialisation JSON.

## Documentation

- MASTER ;
- CORE.

## Validation

- tests unitaires du Kernel ;
- sauvegarde/restauration déterministe ;
- World vide reproductible.

---

# v0.2 — Infrastructure de simulation

Construction de l'infrastructure permettant au monde de vivre dans le temps.

## ENGINE

- journal `World.Events` ;
- Scheduler / boucle de simulation ;
- Systems ;
- Persistence / Serialization ;
- Lifecycle du World et des Entities selon les contrats concernés.

## Simulation

- premier personnage ;
- besoins ;
- vieillissement ;
- cycle de vie ;
- évolution temporelle.

## Validation

Un personnage peut :

- naître ;
- vivre ;
- voir évoluer ses besoins ;
- vieillir ;
- mourir ;

sans moteur graphique.

Toute la simulation reste déterministe.

---

# v0.3 — Une vie entière

Atteint le critère de sortie de la Phase 1 de MASTER-005.

## ACT

- Intent ;
- Planner / Plan ;
- Action ;
- Outcome ;
- Effects ;
- événements observables associés lorsque nécessaire.

## Simulation

- relations ;
- compétences ;
- héritage minimal ;
- assemblage de ces briques en une boucle de vie complète.

## État courant

Les briques ENGINE-008 suivantes sont implémentées :

```text
Relations          ✅
Compétences        ✅
Héritage minimal   ✅
```

Validation technique de référence du moteur :

```text
122 / 122 tests réussis
```

La prochaine étape de v0.3 consiste à vérifier et spécifier l'assemblage nécessaire pour qu'une partie traverse réellement :

```text
création / début de vie
↓
choix et actions
↓
évolution temporelle
↓
relations / compétences
↓
vieillissement
↓
mort
↓
transmission minimale
↓
continuité avec héritier
```

## Rendering

Une première interface jouable peut être construite lorsque la boucle de vie minimale du moteur est suffisamment stable.

Le rendu ne doit pas être utilisé pour compenser une boucle Simulation incomplète.

## Validation de sortie

Le joueur peut :

- vivre une vie complète ;
- mourir ;
- poursuivre avec son héritier.

---

# v0.4 — Le monde vivant

Correspond à la phase où Chroniques dépasse la vie individuelle pour faire évoluer le monde de manière autonome.

Ajouts visés :

- PNJ autonomes ;
- économie autonome ;
- **Mémoire du Monde** ;
- événements dynamiques ;
- premières couches de comportement autonome nécessaires à cette simulation.

## Mémoire du Monde

La Mémoire du Monde est un concept de simulation et de narration persistante défini par la GDB.

Elle ne doit être confondue ni avec :

- `World.Events`, journal technique d'observabilité ;
- la mémoire RAM ou le cache d'un Resource Manager ;
- les `Episode` d'une relation sociale ;
- un hypothétique stockage omniscient de souvenirs individuels.

Elle fera l'objet d'une spécification ENGINE dédiée uniquement lorsqu'un besoin d'implémentation concret sera ouvert pour v0.4.

## Validation

Le monde continue d'évoluer sur plusieurs générations sans intervention permanente du joueur.

---

# v0.5 — La profondeur

Correspond à l'approfondissement des systèmes spécialisés.

Ajouts possibles selon les documents d'autorité :

- économie avancée ;
- métiers ;
- médecine ;
- justice ;
- crime ;
- politique ;
- religion ;
- combat.

## Validation

Trois vies différentes produisent trois histoires profondément différentes sans scripts imposant artificiellement leur déroulement.

---

# v0.6 — Les outils

Ajouts visés :

- éditeur de contenu ;
- debugger de simulation ;
- inspection du World ;
- outils de production ;
- diagnostics de déterminisme et de performance si nécessaires.

---

# v1.0 — Première alpha

Le moteur est considéré suffisamment stable pour une première alpha complète.

Objectifs :

- boucle complète ;
- sauvegarde versionnée ;
- équilibrage ;
- interface aboutie ;
- direction artistique ;
- stabilité ;
- diagnostics suffisants pour reproduire les anomalies de simulation.

---

# Workflow de développement

Toute fonctionnalité structurante suit le cycle :

```text
MASTER / CORE / GDB / ACT
↓
ENGINE
↓
Implémentation
↓
Build
↓
Tests
↓
Validation
↓
TECH
↓
Intégration
```

Aucun document TECH ne doit inventer une fonctionnalité inexistante.

Aucun code structurant ne doit introduire une règle sans autorité documentaire correspondante.

---

# Objectif long terme

Construire un moteur de simulation capable de faire vivre un monde autonome où :

- chaque personnage peut poursuivre ses propres objectifs ;
- les relations évoluent naturellement ;
- l'économie fonctionne indépendamment du joueur ;
- les générations se succèdent ;
- le monde conserve une mémoire narrative de certains faits ;
- les événements émergent de la simulation.

Le jeu est la première utilisation de ce moteur, pas sa seule finalité possible.

---

# Historique

## Version 2.3

- ajout de GDB dans la hiérarchie officielle ;
- remplacement de l'ancien EventBus par le journal `World.Events` réellement implémenté ;
- consolidation Scheduler / Simulation Loop ;
- consolidation Persistence / Serialization ;
- clarification du Resource Manager et de la mémoire technique ;
- suppression du terme ambigu « mémoire » de v0.3 ;
- maintien explicite de la Mémoire du Monde en v0.4 ;
- mise à jour de v0.3 avec Relations, Compétences et Héritage minimal implémentés ;
- ajout de la boucle de vie complète comme prochain objectif d'intégration de v0.3 ;
- validation moteur de référence : **122 / 122 tests réussis**.

## Version 2.2

- création officielle de la bibliothèque ENGINE ;
- intégration de l'architecture documentaire complète ;
- formalisation du workflow Documentation → Implémentation → Tests → TECH ;
- ajout de l'architecture moteur initiale ;
- restructuration de v0.2 autour de l'infrastructure moteur.

## Version 2.1

- suppression de la section « Choix techniques (ADR-002) » au profit de références vers ADR-002 ;
- inversion des versions v0.4 et v0.5 afin de respecter MASTER-005 ;
- ajout de l'en-tête conforme à MASTER-004.

## Version 2.0

- remplace la V1 ;
- intégration des décisions d'ADR-002 ;
- alignement de la feuille de route sur MASTER-005.
