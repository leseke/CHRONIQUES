# Chroniques

**Chaque vie raconte une Chronique.**

> Version : 1.3  
> Statut : Officiel  
> Bibliothèque racine : CHRONIQUES

---

# Présentation

Bienvenue dans le dépôt documentaire officiel de **Chroniques**.

Ce dépôt constitue la base de connaissances centrale du projet. Il regroupe les documents définissant la vision, les règles de simulation, les contrats d'Actions, l'architecture du moteur, la validation et la production.

Le code exécutable vit dans le dépôt séparé :

```text
CHRONIQUES-ENGINE
```

---

# Philosophie

Chroniques suit une approche **Documentation First**.

Une règle ou une architecture structurante doit être reliée à sa bibliothèque d'autorité avant son implémentation, sauf lorsqu'un document ENGINE est explicitement rédigé rétroactivement pour documenter un code historique déjà existant.

La documentation constitue la source de vérité conceptuelle et architecturale.

Le code constitue la vérité de l'implémentation exécutable.

TECH documente cette implémentation après validation.

---

# Hiérarchie de travail

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

Aucune couche aval ne doit contredire une autorité amont applicable.

---

# Architecture du dépôt

```text
CHRONIQUES/
│
├── MASTER/
├── CORE/
├── GDB/
├── ACT/
├── ENGINE/
├── TECH/
├── QA/
├── UX/
├── LORE/
├── PROD/
├── ART/
├── AUDIO/
├── MKT/
├── ADR/
├── AUDIT/
└── README.md
```

---

# Responsabilités

## MASTER

Gouvernance, standards, phases, qualité et cohérence du projet.

## CORE

Primitives fondamentales : Entity, Component, Value, State, Relation, Event, Time, Lifecycle.

## GDB

Règles de simulation : monde, habitants, besoins, relations, compétences, économie, transmission, systèmes sociaux, événements émergents.

## ACT

Langage universel des Actions : Intent, Plan, Action, Outcome, Effects et contrats associés.

## ENGINE

Architecture attendue du moteur de simulation.

## CHRONIQUES-ENGINE

Implémentation C#/.NET déterministe et indépendante du rendu.

## TECH

Documentation de l'implémentation réellement obtenue après validation.

## AUDIT

Contrôles de cohérence, divergences et clôtures de constats transverses.

---

# Catalogue ENGINE actuel

```text
ENGINE-000  Principes d'architecture
ENGINE-001  Journal World.Events
ENGINE-002  Kernel
ENGINE-003  Scheduler et boucle de simulation
ENGINE-004  Systems
ENGINE-005  Persistence / Serialization
ENGINE-006  Action Pipeline                    ✅ Maturité 4
ENGINE-007  Resource Manager — réservé
ENGINE-008  Systems de population              ✅ Maturité 4
ENGINE-009  Boucle de vie minimale             ✅ Maturité 4
ENGINE-010  Orchestration habitants autonomes  ✅ Maturité 4
```

---

# État moteur validé

Le moteur contient notamment :

```text
Kernel
World / Entity
Components
Lifecycle
Scheduler
Persistence
Action Pipeline
Relations
Compétences
Héritage minimal
Effects de population
LifeSession
AutonomousActionSystem
```

Validation globale actuelle :

```text
dotnet build
→ succès

dotnet test
→ 146 / 146 tests réussis
→ 0 échec
```

---

# v0.3 — Boucle de vie minimale

La continuité architecturale suivante est validée :

```text
Action joueur
↓
évolution temporelle
↓
vieillissement
↓
mort
↓
héritage minimal
↓
continuité avec l'héritier
```

Cette chaîne est portée notamment par ENGINE-009 et TECH-002.

---

# v0.4 — Le monde vivant

Le premier lot de v0.4 est désormais validé.

```text
Scheduler.Tick
↓
AutonomousActionSystem
↓
IAutonomousIntentSource
↓
Intent?
↓
IAutonomousIntentExecutor
↓
ENGINE-006
↓
World
```

Ce lot permet à un habitant explicitement enregistré comme autonome d'initier une Action sans intervention du joueur.

Il ne définit pas encore la politique métier qui choisit les Intents.

---

# ENGINE-C06

Le constat historique portant sur l'absence de raccordement entre Scheduler et Actions autonomes est désormais :

```text
ENGINE-C06
→ Clos
```

Sa clôture est enregistrée dans :

```text
AUDIT/ENGINE-C06-Cloture.md
```

La clôture concerne l'orchestration, pas la future intelligence décisionnelle des habitants.

---

# TECH

La bibliothèque TECH est active.

```text
TECH-001 — Systems de population
→ ENGINE-008
→ 122 / 122 à validation initiale

TECH-002 — Boucle de vie minimale
→ ENGINE-009
→ 134 / 134 à validation initiale

TECH-003 — Orchestration des habitants autonomes
→ ENGINE-010
→ 146 / 146 à validation initiale
```

---

# Chaînes de traçabilité

Exemple population :

```text
GDB-004C
↓
ENGINE-008
↓
RelationSystem.cs
↓
RelationSystemTests.cs
↓
TECH-001
```

Exemple boucle de vie :

```text
ENGINE-009
↓
LifeSession.cs
↓
LifeSessionTests.cs
↓
TECH-002
```

Exemple autonomie :

```text
MASTER-005 Phase 3
↓
GDB-004A / GDB-004B
↓
ENGINE-010
↓
AutonomousActionSystem.cs
↓
AutonomousActionSystemTests.cs
↓
146 / 146
↓
TECH-003
```

---

# Principe de responsabilité unique

Une information officielle doit posséder une source d'autorité identifiable.

Lorsqu'un document dépend d'un autre, il doit privilégier la référence et la traçabilité plutôt qu'une duplication normative.

---

# Validation

Une fonctionnalité structurante suit idéalement :

```text
Spécification
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
```

Une fonctionnalité n'est jamais considérée comme implémentée uniquement parce qu'un document la décrit.

---

# Étape actuelle

Le projet a ouvert **v0.4 — Le monde vivant**.

Le premier raccordement d'autonomie est validé.

La prochaine frontière consiste à examiner les autorités GDB capables de définir une première politique déterministe de décision d'habitant, sans inventer cette politique directement dans ENGINE ou dans le code.

Documents à auditer en priorité :

```text
GDB-004B — Besoins
GDB-004D — Personnalités
GDB-004E — Habitudes
GDB-004F — Ambitions
GDB-002E — Opportunités
```

---

# Objectif

Construire une base documentaire et un moteur suffisamment clairs, cohérents et durables pour accompagner Chroniques sur plusieurs années, avec une traçabilité complète entre :

```text
règle
→ architecture
→ code
→ tests
→ documentation technique
```

---

# Historique

## Version 1.3

- ENGINE-010 validée / Maturité 4 ;
- premier lot d'autonomie v0.4 validé ;
- validation globale portée à 146 / 146 ;
- TECH-003 créé ;
- ENGINE-C06 clos ;
- état courant et prochaine frontière v0.4 synchronisés.

## Version 1.2

- ENGINE-009 validée ;
- TECH-002 créé ;
- validation portée à 134 / 134.
