# Chroniques — Feuille de Route V2.4

> Version : 2.4
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

# Ce qui change par rapport à la V2.3

La V2.4 enregistre la validation de la boucle de vie minimale de v0.3.

Principales évolutions :

- `ENGINE-009 — Boucle de vie minimale` passe à **Validée / Maturité 4** ;
- `LifeSession` relie désormais Scheduler, Lifecycle et résultat d'héritage sans introduire de nouvelle règle métier ;
- le test d'intégration v0.3 démontre le parcours minimal `Action → temps → vieillissement → mort → héritier → continuité` ;
- la couverture QA d'ENGINE-009 est complète ;
- validation technique de référence portée à **134 / 134 tests réussis** ;
- création de `TECH-002 — Boucle de vie minimale` ;
- l'ouverture de la phase v0.4 — Le monde vivant peut désormais être préparée sans confondre autonomie des PNJ et orchestration joueur de v0.3.

Cette validation prouve l'assemblage architectural minimal de la continuité d'une vie. Elle ne prétend pas à elle seule représenter toute la richesse finale du contenu, du Rendering ou des parcours joueurs.

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
├── Session / boucle de vie minimale
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

## Session / boucle de vie minimale

`LifeSession`, documentée par ENGINE-009 et TECH-002, orchestre la continuité du personnage contrôlé au-dessus du Scheduler.

Elle ne devient ni un System, ni un moteur de règles métier, ni un moteur d'autonomie PNJ.

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

Atteint le critère de sortie de la Phase 1 de MASTER-005 sur le plan de l'assemblage moteur minimal.

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
- assemblage de ces briques en une boucle de vie continue.

## État courant

Les briques structurantes de v0.3 sont désormais implémentées :

```text
Action Pipeline                ✅
Relations                      ✅
Compétences                    ✅
Héritage minimal               ✅
Boucle de vie / LifeSession    ✅
Continuité avec héritier       ✅
```

Spécifications ENGINE concernées :

```text
ENGINE-006  Validée / Maturité 4
ENGINE-008  Validée / Maturité 4
ENGINE-009  Validée / Maturité 4
```

Documentation technique aval :

```text
TECH-001  Systems de population
TECH-002  Boucle de vie minimale
```

Validation technique de référence du moteur :

```text
dotnet build
→ succès

dotnet test
→ 134 / 134 tests réussis
→ 0 échec
```

Le test d'intégration v0.3 démontre :

```text
choix / Action joueur
↓
évolution temporelle
↓
vieillissement
↓
mort
↓
transmission minimale
↓
continuité avec héritier
```

Ce résultat valide l'assemblage minimal du moteur. La richesse finale d'une vie jouable dépend encore du contenu, du catalogue d'Actions, du Rendering et des systèmes futurs ; elle ne doit pas être inférée du seul nombre de tests.

## Rendering

La boucle de vie minimale du moteur est suffisamment stable pour permettre la construction d'une première interface jouable sans utiliser le Rendering pour compenser une lacune d'orchestration Simulation.

## Validation de sortie

Le moteur sait désormais démontrer techniquement le parcours minimal :

- un personnage contrôlé agit ;
- le temps progresse ;
- il peut mourir ;
- une transmission minimale peut être produite ;
- le contrôle peut poursuivre avec l'héritier.

La validation produit/jeu complète reste distincte de cette validation architecturale.

---

# v0.4 — Le monde vivant

Correspond à la phase où Chroniques dépasse la vie individuelle pour faire évoluer le monde de manière autonome.

Cette phase devient le prochain axe d'architecture moteur après validation d'ENGINE-009.

Ajouts visés :

- PNJ autonomes ;
- économie autonome ;
- **Mémoire du Monde** ;
- événements dynamiques ;
- premières couches de comportement autonome nécessaires à cette simulation.

## Principe d'ouverture

v0.4 ne doit pas commencer par ajouter arbitrairement une IA générale.

Le prochain lot doit d'abord identifier dans les documents GDB existants le plus petit besoin d'autonomie concret, puis produire la spécification ENGINE correspondante avant toute implémentation.

Le constat historique ENGINE-C06 relatif à l'orchestration future des Actions de PNJ reste ouvert et appartient à cette phase.

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

## Version 2.4

- validation d'`ENGINE-009 — Boucle de vie minimale` ;
- ajout de `LifeSession` à l'architecture moteur courante ;
- validation du test d'intégration `Action → temps → mort → héritier → continuité` ;
- création de `TECH-002 — Boucle de vie minimale` ;
- validation moteur portée à **134 / 134 tests réussis** ;
- état v0.3 mis à jour comme assemblage moteur minimal validé ;
- v0.4 identifié comme prochain axe d'architecture ;
- maintien explicite d'ENGINE-C06 dans le périmètre futur des habitants autonomes.

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
