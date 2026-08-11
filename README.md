# Chroniques

**Chaque vie raconte une Chronique.**

> Version : 1.4  
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

TECH documente cette implémentation après validation, à un point de consolidation pertinent conformément à MASTER-006 v1.1.

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

# Gouvernance de validation

Chroniques distingue désormais officiellement :

```text
validation courante
≠
consolidation documentaire
```

Une validation courante synchronise immédiatement les sources de vérité directement concernées.

Une consolidation transverse intervient à un jalon significatif : capacité majeure, fin de bloc cohérent, changement de phase/version, fermeture de bibliothèque/sous-ensemble ou audit critique.

Cette règle est portée par :

```text
MASTER-006 v1.1
```

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

Langage universel des Actions : Intent, Plan, Pattern, Verbe, Action, Outcome, Effects et contrats associés.

## ENGINE

Architecture attendue du moteur de simulation.

## CHRONIQUES-ENGINE

Implémentation C#/.NET déterministe et indépendante du rendu.

## TECH

Documentation de l'implémentation réellement obtenue et validée.

## AUDIT

Contrôles de cohérence, divergences et clôtures de constats ou de jalons transverses.

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
ENGINE-011  Décision autonome par besoins      ✅ Maturité 4
ENGINE-012  Alimentation autonome minimale     ✅ Maturité 4
```

---

# ACT concret actuel

Les sous-bibliothèques PATTERNS et VERBS sont ouvertes et possèdent désormais deux chaînes validées :

```text
Entretien
↓
PAT-001 — Repos
↓
VERB-001 — Se reposer
```

```text
Entretien
↓
PAT-002 — Alimentation
↓
VERB-002 — Manger
```

Les quatre documents sont Officiels / Maturité 4 dans leur périmètre validé.

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
NeedsIntentSource
FoodProductComponent
NeedsPlanner
NeedsExecutionEngine
ActionEffectDispatcher
```

Validation globale actuelle communiquée le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 178 / 178 tests réussis
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

v0.4 comporte désormais deux lots validés.

## Lot 1 — Orchestration autonome

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

Porté par ENGINE-010 et TECH-003.

## Lot 2 — Décision autonome par besoins

```text
Fatigue < seuil
↓
Intent se_reposer
↓
VERB-001
↓
Fatigue restaurée
```

et :

```text
Faim < seuil
+
nourriture accessible
↓
Intent manger
↓
VERB-002
↓
portion consommée
+
Faim restaurée
```

Lorsque les deux besoins sont actionnables, le moteur choisit le besoin dont la satisfaction est la plus basse ; l'égalité est départagée de manière déterministe.

Cette capacité est portée par ENGINE-011, ENGINE-012 et TECH-004.

---

# Ressource alimentaire minimale

L'alimentation ne crée jamais gratuitement une ressource.

Le bloc validé impose :

```text
produit alimentaire réel
+
accessible
+
portion disponible
↓
Action Manger réussie
↓
portion - 1
+
Faim restaurée
```

L'accès est isolé derrière `IAccessibleFoodResolver` afin de ne pas inventer prématurément un système général d'inventaire ou de propriété.

---

# ENGINE-C06

Le constat historique portant sur l'absence de raccordement entre Scheduler et Actions autonomes est :

```text
ENGINE-C06
→ Clos
```

Sa clôture concerne l'orchestration et reste documentée dans :

```text
AUDIT/ENGINE-C06-Cloture.md
```

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

TECH-004 — Décision autonome par besoins
→ ENGINE-011 + ENGINE-012
→ 178 / 178 à consolidation
```

---

# Audit de jalon

Le premier bloc de décision autonome a reçu un contrôle de concordance dédié :

```text
AUDIT/AUDIT-AUTONOMIE-BESOINS-Consolidation.md
→ Clos
```

Ce contrôle confirme la chaîne GDB → ACT → ENGINE → code → tests → TECH dans le périmètre repos + alimentation.

La synthèse haute d'`AUDIT-GLOBALE.md` reste historique et devra être réconciliée lors d'un futur passage global sans écraser son backlog.

---

# Chaîne de traçabilité autonomie actuelle

```text
MASTER-005 Phase 3
↓
GDB-004B v1.2
+
GDB-005E v1.1
↓
PAT-001 / VERB-001
PAT-002 / VERB-002
↓
ENGINE-010 / 011 / 012
↓
CHRONIQUES-ENGINE
↓
178 / 178
↓
TECH-003 / TECH-004
```

---

# Étape actuelle

Le projet poursuit **v0.4 — Le monde vivant**.

Le bloc d'**autonomie physiologique minimale** est consolidé.

La prochaine frontière recommandée n'est pas l'ajout mécanique d'un troisième besoin, mais un pas vers un monde capable de fonctionner réellement sans le joueur :

```text
travail autonome
+
économie autonome minimale
```

Les autorités à auditer avant code comprennent notamment :

```text
GDB-004A — Habitants du Monde
GDB-004B — Besoins
GDB-005 — Économie
GDB-012 — Métiers et activités
GDB-019 — Mécanismes économiques et commerciaux
ACT/PATTERNS
ACT/VERBS
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

## Version 1.4

- MASTER-006 v1.1 formalise validation courante vs consolidation documentaire ;
- ENGINE-011 et ENGINE-012 validées / Maturité 4 ;
- PAT/VERB 001 et 002 validés ;
- validation globale portée à **178 / 178 tests réussis** ;
- TECH-004 créé ;
- bloc autonomie repos + alimentation consolidé ;
- audit de jalon créé ;
- prochaine frontière v0.4 recentrée sur travail autonome et économie minimale.

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
