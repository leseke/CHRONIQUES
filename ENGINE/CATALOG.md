# ENGINE — Catalogue

> Version : 1.7
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (`CHRONIQUES-ENGINE`), TECH, QA

---

# Objectif

Ce catalogue est la source canonique pour la bibliothèque ENGINE.

ENGINE décrit l'architecture fonctionnelle et technique du moteur. Les règles métier restent définies dans leurs bibliothèques d'autorité, notamment CORE, GDB et ACT.

Le catalogue distingue :

- les spécifications existantes ;
- les spécifications rédigées rétroactivement ;
- les spécifications rédigées avant implémentation ;
- les documents encore planifiés.

---

# Documents existants

## ENGINE-000 — Principes d'architecture

Statut : Stable.

Définit notamment :

- Documentation First ;
- déterminisme ;
- contrats ;
- tests ;
- séparation des responsabilités ;
- validation avant intégration.

---

## ENGINE-001 — Journal d'événements du World

Statut : Stable — v2.x.

Décrit `World.Events`.

Le journal :

- accumule les `GameEvent` observables ;
- ne constitue pas un EventBus Publish/Subscribe ;
- n'est jamais utilisé comme canal de coordination entre Systems.

---

## ENGINE-002 — Kernel

Statut : Stable.

Rédigé rétroactivement.

Documente les primitives du Kernel présentes dans le moteur.

---

## ENGINE-003 — Scheduler et boucle de simulation

Statut : Stable.

Rédigé rétroactivement.

Documente :

- l'avancement du Tick ;
- l'ordre déterministe des Systems ;
- la boucle de simulation actuellement portée par le Scheduler.

---

## ENGINE-004 — Systems de simulation

Statut : Stable.

Rédigé rétroactivement.

Couvre notamment :

- `NeedsDecaySystem` ;
- `AgingSystem` ;
- `CalendrierSimule`.

---

## ENGINE-005 — Persistence et Serialization

Statut : Stable.

Rédigé rétroactivement.

Documente :

- `WorldRepository` ;
- snapshots ;
- sérialisation JSON ;
- restauration du World.

La sérialisation reste intégrée au même ensemble architectural que la persistance tant qu'aucune séparation technique réelle ne le justifie.

---

## ENGINE-006 — Action Pipeline

Statut : Validée.

Maturité : 4.

Première spécification ENGINE ayant parcouru le cycle complet :

```text
Spécification
↓
Implémentation
↓
Tests
↓
Validation
```

Traduit ACT en architecture concrète :

```text
Intent
↓
Planner
↓
Plan
↓
Action Instance
↓
Execution Engine
↓
Outcome
```

L'implémentation est présente et testée dans `CHRONIQUES-ENGINE`.

---

## ENGINE-008 — Systems de population

### Relations, Compétences, Héritage

Statut : Validée.

Maturité : 4.

Rédigé avant implémentation puis implémenté et validé dans `CHRONIQUES-ENGINE`.

Couvre :

- `RelationComponent` ;
- `RelationSystem` ;
- `SkillComponent` ;
- `SkillSystem` ;
- `HeritageSystem` ;
- `RelationInteractionEffect` ;
- `SkillPracticeEffect` ;
- `HeritageRefusalEffect` ;
- `PopulationEffectApplicator`.

Validation de référence du lot ENGINE-008 :

```text
dotnet build
→ succès

dotnet test
→ 122 / 122 tests réussis
→ 0 échec
```

La transmission matérielle incomplète définie conceptuellement par GDB-004J reste volontairement différée tant que le moteur ne dispose pas d'une représentation du patrimoine transmissible.

ENGINE-008 participe à la cible v0.3 sur les axes suivants :

```text
relations
compétences
héritage minimal
```

La Mémoire du Monde n'appartient pas à ENGINE-008 et relève de la phase du monde vivant, ciblée par v0.4 dans la feuille de route.

---

## ENGINE-009 — Boucle de vie minimale

Statut : Validée.

Maturité : 4.

Rédigé avant implémentation conformément au workflow Documentation First, puis implémenté et validé dans `CHRONIQUES-ENGINE`.

Objectif : relier les briques déjà présentes de la v0.3 afin de démontrer la continuité minimale :

```text
personnage actif
↓
Actions joueur
↓
Scheduler / Systems
↓
mort
↓
HeritageSystem
↓
héritier
↓
continuité de session
```

ENGINE-009 :

- ne crée aucune nouvelle règle métier ;
- ne déclenche aucune Action de PNJ automatiquement ;
- ne remplace ni ENGINE-003 ni ENGINE-006 ;
- conserve `Lifecycle` comme source de vérité de la mort ;
- conserve `HeritageSystem` comme source de vérité de la désignation ;
- autorise la couche de session à lire `World.Events` uniquement comme journal d'observabilité ;
- ne ferme pas ENGINE-C06, qui concerne l'orchestration future des habitants autonomes.

Validation de référence :

```text
dotnet build
→ succès

dotnet test
→ 134 / 134 tests réussis
→ 0 échec
```

Le test d'intégration de référence démontre :

```text
Action joueur
→ progression temporelle
→ vieillissement
→ mort
→ héritage
→ continuité avec l'héritier
```

Cette validation prouve l'assemblage architectural minimal de la v0.3 ; elle ne prétend pas à elle seule représenter toute la richesse finale d'une vie jouable.

---

## ENGINE-010 — Orchestration des habitants autonomes

Statut : Proposition.

Maturité : 2.

Première spécification ENGINE ouverte pour v0.4 — Le monde vivant.

Elle répond au besoin conservé par `ENGINE-C06`, dont la réouverture était explicitement différée jusqu'à l'entrée en Phase 3 de MASTER-005.

Objectif minimal : permettre à un habitant explicitement enregistré comme autonome d'initier un Intent pendant un Tick, sans intervention du joueur, puis remettre cet Intent à un exécuteur conforme à ENGINE-006.

```text
Scheduler
↓
AutonomousActionSystem
↓
IAutonomousIntentSource
↓
Intent
↓
IAutonomousIntentExecutor
↓
ENGINE-006
↓
World
```

ENGINE-010 sépare strictement :

- orchestration ;
- décision métier ;
- exécution d'Action.

Il n'introduit :

- ni IA complète ;
- ni règle de priorité des besoins ;
- ni Habitudes ou Ambitions implémentées ;
- ni catalogue de Verbes ;
- ni économie autonome ;
- ni Mémoire du Monde ;
- ni règle `1 Action = 1 Tick`.

Le test d'intégration cible utilise « Se reposer » uniquement comme Verbe déjà exécutable afin de prouver le raccordement Scheduler → autonomie → ENGINE-006.

---

# Documents planifiés mais non créés

## ENGINE-007 — Resource Manager

Gestion future des ressources techniques :

- contenu externe chargé ;
- durée de vie des ressources ;
- cache et ressources mémoire au sens technique.

Ce document ne désigne pas la Mémoire du Monde au sens GDB.

Aucun besoin d'implémentation concret ne justifie encore sa création.

Il reste réservé mais non spécifié conformément à MASTER-006.

---

# Consolidation de l'organisation initiale

La structure initiale envisageait notamment des documents distincts pour :

- Scheduler ;
- Simulation Loop ;
- Persistence ;
- Serialization.

L'architecture réellement implémentée a montré que certaines responsabilités sont actuellement indissociables.

Ainsi :

```text
Simulation Loop
→ intégrée à ENGINE-003
```

car `Scheduler.Tick` porte actuellement l'avancement du World et l'exécution ordonnée des Systems.

Et :

```text
Serialization
→ intégrée à ENGINE-005
```

car persistance et sérialisation sont actuellement portées par le même ensemble de contrats.

Cette consolidation reflète le code réel.

Si ces responsabilités deviennent techniquement indépendantes, elles pourront être séparées par une nouvelle spécification.

---

# État de concordance

```text
ENGINE-000  Stable
ENGINE-001  Stable
ENGINE-002  Stable
ENGINE-003  Stable
ENGINE-004  Stable
ENGINE-005  Stable
ENGINE-006  Validée / Maturité 4
ENGINE-007  Réservé / non créé
ENGINE-008  Validée / Maturité 4
ENGINE-009  Validée / Maturité 4
ENGINE-010  Proposition / Maturité 2
```

---

# Convention de nommage

Le fichier canonique du catalogue ENGINE est :

```text
ENGINE/CATALOG.md
```

Tout ancien fichier alternatif de catalogue doit uniquement rediriger vers ce fichier et ne doit plus constituer une seconde source de vérité.

---

# Historique

## Version 1.7

- création de `ENGINE-010 — Orchestration des habitants autonomes` ;
- entrée documentaire dans v0.4 — Le monde vivant ;
- réouverture ciblée du besoin architectural conservé par ENGINE-C06 ;
- séparation entre orchestration autonome, source d'Intent et exécution ENGINE-006 ;
- absence volontaire de politique de décision métier tant que la GDB n'en fournit pas une suffisamment précise ;
- test d'intégration cible Scheduler → autonomie → Pipeline d'Actions.

## Version 1.6

- ENGINE-009 passe à **Validée / Maturité 4** ;
- `LifeSession` et sa couverture QA sont confirmés dans `CHRONIQUES-ENGINE` ;
- test d'intégration de continuité v0.3 confirmé ;
- validation globale portée à **134 / 134 tests réussis** ;
- distinction conservée entre validation de l'assemblage minimal et richesse finale d'une vie jouable.

## Version 1.5

- création de `ENGINE-009 — Boucle de vie minimale` ;
- enregistrement d'ENGINE-009 en Proposition / Maturité 2 ;
- ajout du critère d'intégration `personnage actif → mort → héritier → continuité` ;
- clarification explicite qu'ENGINE-009 ne ferme pas ENGINE-C06 relatif aux habitants autonomes.

## Version 1.4

- `ENGINE/CATALOG.md` devient explicitement le catalogue canonique unique ;
- synchronisation avec l'état réel d'ENGINE-006 et ENGINE-008 ;
- validation ENGINE-008 conservée à **122 / 122 tests réussis** ;
- clarification de la frontière entre mémoire technique du Resource Manager et Mémoire du Monde ;
- suppression de la Mémoire du Monde de la cible ENGINE-008 / v0.3 ;
- rappel des consolidations Scheduler/Simulation Loop et Persistence/Serialization.

## Version 1.3

- ENGINE-008 passe à Validée / Maturité 4 ;
- implémentation correspondante confirmée dans `CHRONIQUES-ENGINE` ;
- ajout des Effects de population et de `PopulationEffectApplicator` ;
- `HeritageRefusalEffect` traité par `HeritageSystem` ;
- correction du comportement du plancher familial ;
- transmission incomplète explicitement différée.

## Version 1.2

- ENGINE-006 validé après implémentation et tests ;
- création d'ENGINE-008 comme spécification préalable aux Systems de population ;
- dépendance GDB ajoutée au catalogue.

## Version 1.1

- création d'ENGINE-006 — Action Pipeline.

## Version 1.0

- création du catalogue lors de la documentation rétroactive d'ENGINE-002 à ENGINE-005.
