# ENGINE — Catalogue

> Version : 1.13
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (`CHRONIQUES-ENGINE`), TECH, QA

---

# Objectif

Ce catalogue est la source canonique pour la bibliothèque ENGINE.

ENGINE décrit l'architecture fonctionnelle et technique attendue du moteur. Les règles métier restent définies dans leurs bibliothèques d'autorité, notamment CORE, GDB et ACT.

---

# Documents existants

## ENGINE-000 — Principes d'architecture

Statut : Stable.

Définit notamment Documentation First, déterminisme, contrats, tests, séparation des responsabilités et validation avant intégration.

---

## ENGINE-001 — Journal d'événements du World

Statut : Stable — v2.x.

`World.Events` est un journal observable, jamais un EventBus entre Systems.

---

## ENGINE-002 — Kernel

Statut : Stable.

Rédigé rétroactivement pour documenter les primitives du Kernel présentes dans le moteur.

---

## ENGINE-003 — Scheduler et boucle de simulation

Statut : Stable.

Documente l'avancement du Tick, l'ordre déterministe des Systems et la boucle actuellement portée par le Scheduler.

---

## ENGINE-004 — Systems de simulation

Statut : Stable.

Couvre notamment `NeedsDecaySystem`, `AgingSystem` et `CalendrierSimule`.

---

## ENGINE-005 — Persistence et Serialization

Statut : Stable.

Documente `WorldRepository`, snapshots, sérialisation JSON et restauration du World.

---

## ENGINE-006 — Action Pipeline

Statut : Validée.

Maturité : 4.

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

---

## ENGINE-008 — Systems de population

Statut : Validée.

Maturité : 4.

Couvre Relations, Compétences, Héritage minimal et Effects de population.

Validation de référence : `122 / 122`.

---

## ENGINE-009 — Boucle de vie minimale

Statut : Validée.

Maturité : 4.

Relie Action joueur, Scheduler, mort, HeritageSystem et continuité avec l'héritier.

Validation de référence : `134 / 134`.

---

## ENGINE-010 — Orchestration des habitants autonomes

Statut : Validée.

Maturité : 4.

```text
Scheduler
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

Validation de référence : `146 / 146`.

Cette validation résout la lacune architecturale ENGINE-C06.

---

## ENGINE-011 — Décision autonome par besoins

Statut : Validée.

Maturité : 4.

Premier comportement autonome réel :

```text
Fatigue < seuil
↓
Intent se_reposer
```

Validation technique courante :

```text
158 / 158 tests réussis
```

La couverture comprend le franchissement strict du seuil et une régulation autonome multi-Tick.

---

## ENGINE-012 — Alimentation autonome minimale

Statut : Validée.

Maturité : 4.

Deuxième comportement autonome réel, fondé sur :

```text
GDB-004B v1.2
+
GDB-005E v1.1
↓
PAT-002 Alimentation
↓
VERB-002 Manger
```

Flux validé :

```text
Faim sous seuil
+
nourriture accessible
↓
Intent manger
↓
NeedsPlanner
↓
PlanStep + Cibles
↓
Manger
↓
Outcome
↓
portion consommée
+
Faim restaurée
```

ENGINE-012 introduit uniquement ce qui devient nécessaire avec le deuxième Verbe réel :

- `FoodProductComponent` ;
- `IAccessibleFoodResolver` sans inventaire imposé ;
- Cibles portées par `PlanStep` ;
- `NeedsPlanner` pour `se_reposer` et `manger` ;
- décision Faim/Fatigue déterministe ;
- `MangerDefinition` ;
- applicateurs d'Effects séparés du `PipelineRunner` ;
- entrée générique `PipelineRunner.Execute` ;
- persistance de `FoodProductComponent`.

Validation technique communiquée le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 178 / 178 tests réussis
→ 0 échec
```

La suite confirme le maintien de VERB-001, le fonctionnement de VERB-002 de bout en bout, la consommation d'une ressource réelle, l'arbitrage déterministe et l'absence d'inventaire implicite.

---

# Documents planifiés mais non créés

## ENGINE-007 — Resource Manager

Gestion future des ressources techniques : contenu externe, durée de vie, cache et ressources mémoire au sens technique.

Ce document ne désigne pas les ressources économiques de GDB-005.

Il reste réservé mais non spécifié conformément à MASTER-006.

---

# Consolidation de l'organisation initiale

```text
Simulation Loop
→ intégrée à ENGINE-003
```

```text
Serialization
→ intégrée à ENGINE-005
```

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
ENGINE-010  Validée / Maturité 4
ENGINE-011  Validée / Maturité 4
ENGINE-012  Validée / Maturité 4
```

---

# Convention de nommage

Le catalogue canonique unique est :

```text
ENGINE/CATALOG.md
```

---

# Historique

## Version 1.13

- ENGINE-012 passe à **Validée / Maturité 4** ;
- validation locale portée à **178 / 178 tests réussis** ;
- second besoin autonome `Faim → manger` confirmé de bout en bout ;
- arbitrage déterministe Faim/Fatigue validé ;
- Cibles dans le Plan, pipeline multi-Verbes et applicateurs d'Effects confirmés ;
- produit alimentaire consommable et persistance validés ;
- aucune consolidation TECH/roadmap/README déclenchée automatiquement.

## Version 1.12

- création d'ENGINE-012 — Alimentation autonome minimale ;
- prise en compte de GDB-004B v1.2 et GDB-005E v1.1 ;
- raccordement de PAT-002 / VERB-002 ;
- deuxième besoin autonome `Faim → manger` spécifié ;
- Cibles matérialisées dans le Plan ;
- séparation du runner et des applicateurs d'Effects ;
- produit alimentaire minimal et persistance ajoutés ;
- couverture QA cible portée à 17 nouveaux tests, soit 178 attendus.

## Version 1.11

- validation courante d'ENGINE-011 portée à 158 / 158 ;
- preuve multi-Tick de régulation autonome ajoutée.

## Version 1.10

- ENGINE-011 passe à Validée / Maturité 4 ;
- suite globale portée à 156 / 156.

## Version 1.9

- création d'ENGINE-011.

## Version 1.8

- ENGINE-010 passe à Validée / Maturité 4 ;
- suite globale portée à 146 / 146 ;
- ENGINE-C06 résolue.

## Version 1.7

- création d'ENGINE-010.

## Version 1.6

- ENGINE-009 validée / Maturité 4 ;
- validation portée à 134 / 134.

## Version 1.5

- création d'ENGINE-009.

## Version 1.4

- catalogue canonique unique ;
- synchronisation ENGINE-006 / ENGINE-008.

## Version 1.3

- ENGINE-008 validée / Maturité 4.

## Version 1.2

- ENGINE-006 validée ;
- création d'ENGINE-008.

## Version 1.1

- création d'ENGINE-006.

## Version 1.0

- création du catalogue lors de la documentation rétroactive d'ENGINE-002 à ENGINE-005.
