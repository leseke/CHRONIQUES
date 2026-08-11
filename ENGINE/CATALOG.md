# ENGINE — Catalogue

> Version : 1.8
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

Première spécification ENGINE à avoir parcouru le cycle complet :

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

---

## ENGINE-008 — Systems de population

### Relations, Compétences, Héritage

Statut : Validée.

Maturité : 4.

Couvre :

- `RelationComponent` / `RelationSystem` ;
- `SkillComponent` / `SkillSystem` ;
- `HeritageSystem` ;
- Effects de population ;
- `PopulationEffectApplicator`.

Validation de référence du lot :

```text
dotnet build
→ succès

dotnet test
→ 122 / 122 tests réussis
```

La transmission matérielle complète reste différée tant que le patrimoine transmissible n'est pas représenté.

---

## ENGINE-009 — Boucle de vie minimale

Statut : Validée.

Maturité : 4.

Relie les briques v0.3 en une continuité minimale :

```text
Action joueur
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

Validation de référence :

```text
dotnet build
→ succès

dotnet test
→ 134 / 134 tests réussis
```

ENGINE-009 n'avait volontairement pas fermé ENGINE-C06 : l'autonomie des habitants relevait de la Phase 3.

---

## ENGINE-010 — Orchestration des habitants autonomes

Statut : Validée.

Maturité : 4.

Première spécification ENGINE validée de v0.4 — Le monde vivant.

Objectif : permettre à un habitant explicitement enregistré comme autonome d'initier un Intent pendant un Tick sans intervention du joueur, puis remettre cet Intent à un exécuteur conforme à ENGINE-006.

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

ENGINE-010 sépare strictement :

- orchestration ;
- décision métier ;
- exécution d'Action.

Il n'introduit ni IA complète, ni formule de priorité des besoins, ni Habitudes/Ambitions, ni économie autonome, ni Mémoire du Monde, ni règle `1 Action = 1 Tick`.

Validation de référence :

```text
dotnet build
→ succès

dotnet test
→ 146 / 146 tests réussis
→ 0 échec
```

Le lot ajoute 12 tests, dont une intégration réelle :

```text
Scheduler.Tick
↓
AutonomousActionSystem
↓
Intent "se_reposer"
↓
PipelineRunner
↓
Action Archived
↓
Outcome réussi
↓
World modifié
```

Cette validation résout la lacune architecturale `ENGINE-C06` relative au raccordement Scheduler / Actions autonomes. Elle ne clôt pas la future politique de décision des PNJ.

---

# Documents planifiés mais non créés

## ENGINE-007 — Resource Manager

Gestion future des ressources techniques : contenu externe, durée de vie, cache et ressources mémoire au sens technique.

Ce document ne désigne pas la Mémoire du Monde au sens GDB.

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

Ces consolidations restent valides tant que le code ne matérialise pas des responsabilités indépendantes.

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
```

---

# Convention de nommage

Le catalogue canonique unique est :

```text
ENGINE/CATALOG.md
```

Tout ancien catalogue alternatif doit uniquement rediriger vers ce fichier.

---

# Historique

## Version 1.8

- ENGINE-010 passe à **Validée / Maturité 4** ;
- implémentation `AutonomousActionSystem` et contrats d'injection confirmés ;
- couverture ENGINE-010 validée ;
- suite globale portée à **146 / 146 tests réussis** ;
- intégration Scheduler → autonomie → ENGINE-006 confirmée ;
- lacune ENGINE-C06 considérée résolue ;
- frontière maintenue avec la politique future de décision des PNJ.

## Version 1.7

- création de `ENGINE-010 — Orchestration des habitants autonomes` ;
- entrée documentaire dans v0.4 ;
- réouverture ciblée d'ENGINE-C06 ;
- séparation orchestration / source d'Intent / exécution ENGINE-006.

## Version 1.6

- ENGINE-009 validée / Maturité 4 ;
- validation portée à 134 / 134 tests ;
- création du point de sortie v0.3.

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
