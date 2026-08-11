# Chroniques — Feuille de Route V2.5

> Version : 2.5
> Statut : Officiel
> Type : Roadmap
> Maturité : 2
> Bibliothèque : PROD

---

# Vision

Chroniques est un moteur de simulation narratif sur lequel un jeu est construit.

Le développement suit une approche **Documentation First** : toute règle ou architecture structurante est reliée à une autorité documentaire avant son implémentation, sauf documentation ENGINE explicitement rétroactive d'un code historique existant.

---

# Ce qui change par rapport à la V2.4

La V2.5 enregistre le premier lot validé de v0.4 — Le monde vivant.

Principales évolutions :

- `ENGINE-010 — Orchestration des habitants autonomes` passe à **Validée / Maturité 4** ;
- `AutonomousActionSystem` permet désormais au Scheduler de conduire indirectement une Action d'habitant sans intervention du joueur ;
- les frontières `IAutonomousIntentSource` et `IAutonomousIntentExecutor` séparent décision, orchestration et exécution ;
- le test d'intégration démontre `Scheduler → autonomie → Intent → ENGINE-006 → World` ;
- validation technique de référence portée à **146 / 146 tests réussis** ;
- création de `TECH-003 — Orchestration des habitants autonomes` ;
- `ENGINE-C06` est clôturé sur sa lacune d'orchestration ;
- la politique de décision des habitants reste volontairement hors du périmètre d'ENGINE-010.

---

# Principes de développement

## 1. Le code suit les spécifications

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

## 2. Documentation vivante

Une fonctionnalité structurante n'est terminée que lorsqu'elle est :

- spécifiée ;
- implémentée ;
- compilée ;
- testée ;
- validée ;
- documentée dans TECH lorsque le lot est stable.

## 3. Data-driven

Les données métier spécifiques ont vocation à être externalisées lorsqu'elles peuvent l'être.

## 4. Déterminisme

À état, seed, entrées et ordre identiques, la simulation doit produire le même résultat.

## 5. Séparation des responsabilités

- MASTER : gouvernance ;
- CORE : primitives ;
- GDB : règles et modèles de simulation ;
- ACT : langage universel des Actions ;
- ENGINE : architecture attendue ;
- CHRONIQUES-ENGINE : implémentation exécutable ;
- TECH : documentation de l'implémentation validée.

---

# Architecture moteur actuelle

```text
World
│
├── Kernel
├── World.Events
├── Scheduler / Simulation Loop
├── Systems
├── Action Pipeline
├── Session / boucle de vie minimale
├── Autonomy / orchestration habitants
├── Persistence / Serialization
└── Resource Management futur
```

## World.Events

`World.Events` reste un journal d'observabilité, jamais un EventBus entre Systems.

## Scheduler

Le Scheduler reste l'autorité sur l'avancement du Tick et l'ordre des Systems.

## LifeSession

`LifeSession` orchestre le personnage contrôlé et la continuité minimale avec l'héritier.

## Autonomy

Le premier lot d'autonomie est maintenant validé :

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

Cette architecture ne constitue pas encore une IA métier complète.

---

# Feuille de route par versions

# v0.1 — Le noyau

Fondations :

- Entity ;
- Component ;
- State ;
- Value ;
- Relation ;
- World ;
- Tick ;
- Lifecycle ;
- RNG déterministe ;
- première sérialisation.

Statut architectural : ✅

---

# v0.2 — Infrastructure de simulation

Infrastructure :

- `World.Events` ;
- Scheduler ;
- Systems ;
- Persistence / Serialization ;
- besoins ;
- vieillissement ;
- cycle de vie.

Statut architectural : ✅

---

# v0.3 — Une vie entière

Objectif : assembler les briques nécessaires à une continuité minimale d'une vie contrôlée.

## État validé

```text
Action Pipeline                ✅ ENGINE-006
Relations                      ✅ ENGINE-008
Compétences                    ✅ ENGINE-008
Héritage minimal               ✅ ENGINE-008
LifeSession                    ✅ ENGINE-009
Mort → héritier → continuité   ✅ ENGINE-009
```

Documentation TECH :

```text
TECH-001 — Systems de population
TECH-002 — Boucle de vie minimale
```

Validation de référence :

```text
dotnet build
→ succès

dotnet test
→ 134 / 134 tests réussis
```

Le test d'intégration v0.3 démontre :

```text
Action joueur
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

Ce résultat valide l'assemblage moteur minimal. Il ne prétend pas représenter toute la richesse finale du contenu ou du Rendering.

---

# v0.4 — Le monde vivant

Objectif : donner au monde une existence indépendante de l'intervention permanente du joueur.

Cible de phase :

- habitants autonomes ;
- économie qui évolue ;
- événements du monde ;
- Mémoire du Monde ;
- évolution crédible sur plusieurs générations.

## Lot 1 — Orchestration autonome

Statut : ✅ Validé

Spécification :

```text
ENGINE-010 — Orchestration des habitants autonomes
```

Implémentation :

```text
IAutonomousIntentSource
IAutonomousIntentExecutor
AutonomousActionSystem
```

Validation :

```text
dotnet build
→ succès

dotnet test
→ 146 / 146 tests réussis
→ 0 échec
```

Test d'intégration :

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

Documentation technique :

```text
TECH-003 — Orchestration des habitants autonomes
```

Constat historique :

```text
ENGINE-C06
→ Clos
```

## Frontière du lot 1

ENGINE-010 valide :

```text
quand et comment un habitant autonome peut remettre un Intent au pipeline
```

Il ne définit pas :

```text
pourquoi cet habitant choisit précisément cet Intent
```

La politique de décision reste donc la prochaine frontière conceptuelle naturelle.

## Étape suivante de v0.4

Avant tout nouveau code, auditer les autorités GDB qui peuvent justifier une première politique déterministe de décision :

```text
GDB-004B — Besoins
GDB-004D — Personnalités
GDB-004E — Habitudes
GDB-004F — Ambitions
GDB-002E — Opportunités
```

Objectif : déterminer si les règles existantes sont assez précises pour spécifier une politique minimale `Entity + World + Tick → Intent?`.

Si elles ne le sont pas, la GDB doit être précisée avant toute nouvelle spécification ENGINE.

## Autres lots v0.4 à ouvrir seulement au besoin

- Mémoire du Monde ;
- événements dynamiques ;
- économie autonome minimale ;
- travail et activités autonomes ;
- interactions autonomes entre habitants.

Aucun ordre artificiel n'est imposé tant que le besoin concret n'est pas établi.

## Critère de sortie

Le monde évolue de façon crédible pendant plusieurs générations sans intervention permanente du joueur.

v0.4 n'est donc **pas** terminée avec ENGINE-010 : seul son premier raccordement architectural est validé.

---

# v0.5 — La profondeur

Ajouts possibles selon les autorités :

- économie avancée ;
- métiers ;
- médecine ;
- justice ;
- crime ;
- politique ;
- religion ;
- combat ;
- patrimoine avancé.

Critère : trois parcours radicalement différents produisent des histoires profondément différentes.

---

# v0.6 — Les outils

Ajouts visés :

- éditeur de contenu ;
- debugger de simulation ;
- inspection du World ;
- diagnostics déterministes ;
- outils de production.

---

# v1.0 — Première alpha

Objectifs :

- boucle complète ;
- sauvegarde versionnée ;
- équilibrage ;
- interface aboutie ;
- direction artistique ;
- stabilité ;
- diagnostics suffisants.

---

# Workflow de développement

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

- chaque personnage poursuit ses propres objectifs ;
- les relations évoluent naturellement ;
- l'économie fonctionne indépendamment du joueur ;
- les générations se succèdent ;
- le monde conserve une mémoire narrative ;
- les événements émergent de la simulation.

---

# Historique

## Version 2.5

- ENGINE-010 validée / Maturité 4 ;
- premier raccordement d'habitants autonomes au Scheduler validé ;
- suite globale portée à **146 / 146 tests réussis** ;
- création de TECH-003 ;
- clôture d'ENGINE-C06 ;
- distinction explicite entre orchestration autonome et politique de décision ;
- prochaine étape recentrée sur l'audit des autorités GDB avant tout nouveau code.

## Version 2.4

- ENGINE-009 validée / Maturité 4 ;
- boucle de vie minimale v0.3 validée ;
- suite portée à 134 / 134 ;
- création de TECH-002 ;
- ouverture de la préparation v0.4.

## Version 2.3

- alignement de la roadmap sur l'architecture documentaire et moteur ;
- ENGINE-008 validée ;
- cible v0.3 clarifiée.

## Version 2.2

- introduction de la bibliothèque ENGINE et du workflow Documentation → Code → Tests → TECH.

## Version 2.1

- ordre des phases aligné sur MASTER-005 ;
- suppression des duplications de décisions techniques.

## Version 2.0

- remplace la V1 et intègre les décisions architecturales initiales.
