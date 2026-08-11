# TECH

> Version : 1.4  
> Statut : Active  
> Type : Bibliothèque  
> Maturité : 2  
> Bibliothèque : TECH

---

## Rôle

Le dossier **TECH** regroupe la documentation des implémentations techniques réellement présentes et validées dans Chroniques.

TECH ne définit pas les règles métier.

Il documente la manière dont les spécifications validées sont effectivement traduites dans :

```text
CHRONIQUES-ENGINE
```

---

## Position documentaire

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

### GDB

Définit les règles de simulation.

### ACT

Définit les contrats relatifs aux Actions.

### ENGINE

Définit l'architecture attendue du moteur.

### CHRONIQUES-ENGINE

Contient l'implémentation exécutable.

### TECH

Documente l'implémentation réellement obtenue et validée.

---

## Règle fondamentale

Un document TECH :

```text
décrit
```

mais ne :

```text
prescrit pas une nouvelle règle métier
```

Toute nouvelle règle doit d'abord être définie dans sa bibliothèque d'autorité.

Conformément à MASTER-006 v1.1, TECH n'est pas nécessairement régénéré après chaque incrément validé.

Un document TECH peut consolider plusieurs lots ENGINE lorsque ceux-ci forment une capacité technique cohérente et qu'un point de consolidation documentaire significatif est atteint.

---

## Contenu actuel

### TECH-001 — Systems de population

Statut : Validé.

Spécification :

```text
ENGINE-008
```

Documente notamment :

- `RelationComponent` / `RelationSystem` ;
- `SkillComponent` / `SkillSystem` ;
- `HeritageSystem` ;
- Effects de population ;
- `PopulationEffectApplicator`.

Validation initiale :

```text
122 / 122 tests réussis
```

---

### TECH-002 — Boucle de vie minimale

Statut : Validé.

Spécification :

```text
ENGINE-009
```

Documente notamment :

- `LifeSession` ;
- `LifeSessionState` ;
- orchestration de `Scheduler.Tick(World)` ;
- détection de la mort via `Lifecycle` ;
- continuité du contrôle avec l'héritier ;
- terminaison sans successeur ;
- invariants QA et déterminisme de la séquence de contrôle.

Validation initiale :

```text
134 / 134 tests réussis
```

---

### TECH-003 — Orchestration des habitants autonomes

Statut : Validé.

Spécification :

```text
ENGINE-010
```

Documente notamment :

- `IAutonomousIntentSource` ;
- `IAutonomousIntentExecutor` ;
- `AutonomousActionSystem` ;
- ordre déterministe des Acteurs autonomes ;
- filtrage Entity absente / morte ;
- cohérence `intent.Acteur` ;
- absence d'avancement autonome du Tick ;
- intégration réelle Scheduler → autonomie → ENGINE-006 → World ;
- résolution technique d'ENGINE-C06.

Validation initiale :

```text
146 / 146 tests réussis
```

---

### TECH-004 — Décision autonome par besoins

Statut : Validé.

Spécifications :

```text
ENGINE-011
ENGINE-012
```

TECH-004 consolide le premier bloc de décision autonome réellement exploitable :

```text
Fatigue → se_reposer
Faim + nourriture accessible → manger
```

Il documente notamment :

- `NeedsIntentSource` ;
- seuils configurables de Fatigue et Faim ;
- arbitrage déterministe entre besoins actionnables ;
- `FoodProductComponent` ;
- `IAccessibleFoodResolver` ;
- Cibles portées par `PlanStep` ;
- `NeedsPlanner` ;
- `NeedsExecutionEngine` ;
- `MangerDefinition` ;
- séparation du `PipelineRunner` et des applicateurs d'Effects ;
- consommation réelle d'une portion alimentaire ;
- restauration de Faim ;
- persistance du produit alimentaire ;
- conservation de la compatibilité avec `VERB-001 — Se reposer`.

Validation de consolidation :

```text
178 / 178 tests réussis
```

---

## Contenu futur

Les prochains documents TECH seront créés lorsqu'un ensemble technique suffisamment stable nécessite une documentation d'implémentation.

```text
TECH-005
TECH-006
...
```

Aucun sujet n'est réservé à l'avance.

---

## Ce que TECH peut documenter

TECH peut notamment couvrir :

- architecture logicielle réelle ;
- structure des projets ;
- implémentations des Systems ;
- persistance ;
- sérialisation ;
- mécanismes d'Actions ;
- autonomie technique ;
- performance ;
- diagnostic ;
- outils de développement ;
- choix de structures de données ;
- contraintes techniques observées.

---

## Ce que TECH ne doit pas définir

TECH ne doit pas devenir l'autorité sur :

- comportement métier des habitants ;
- économie ;
- relations ;
- psychologie ;
- actions conceptuelles ;
- Game Design ;
- règles de progression.

---

## Convention

Chaque document utilise un identifiant unique.

```text
TECH-001
TECH-002
TECH-003
TECH-004
...
```

Documents actuels :

```text
TECH-001 — Systems de population.md
TECH-002 — Boucle de vie minimale.md
TECH-003 — Orchestration des habitants autonomes.md
TECH-004 — Décision autonome par besoins.md
```

---

## Traçabilité

Chaque document TECH identifie lorsque possible :

```text
Spécification source
↓
Code concerné
↓
Tests concernés
↓
TECH
```

Exemple de consolidation courant :

```text
GDB-004B / GDB-005E
↓
PAT/VERB 001-002
↓
ENGINE-011 / ENGINE-012
↓
CHRONIQUES-ENGINE
↓
178 / 178
↓
TECH-004
```

---

# État actuel

```text
Documents numérotés : 4

TECH-001
→ Systems de population
→ Validé

TECH-002
→ Boucle de vie minimale
→ Validé

TECH-003
→ Orchestration des habitants autonomes
→ Validé

TECH-004
→ Décision autonome par besoins
→ Validé
```

---

# Historique

## Version 1.4

- ajout de `TECH-004 — Décision autonome par besoins` au premier point de consolidation suivant ENGINE-011 et ENGINE-012 ;
- documentation consolidée des comportements autonomes `se_reposer` et `manger` ;
- validation moteur portée à **178 / 178 tests réussis** ;
- prise en compte de MASTER-006 v1.1 : TECH peut consolider plusieurs incréments cohérents au lieu d'être généré après chaque petite validation ;
- nombre de documents numérotés porté à 4.

## Version 1.3

- ajout de `TECH-003 — Orchestration des habitants autonomes` ;
- enregistrement de la validation ENGINE-010 ;
- validation moteur portée à **146 / 146 tests réussis** pour ce lot ;
- résolution technique d'ENGINE-C06 documentée ;
- nombre de documents numérotés porté à 3.

## Version 1.2

- ajout de `TECH-002 — Boucle de vie minimale` ;
- validation ENGINE-009 enregistrée ;
- validation portée à 134 / 134 ;
- nombre de documents numérotés porté à 2.

## Version 1.1

- bibliothèque passée de Fondation à Active ;
- création de TECH-001 ;
- clarification du rôle de TECH et de la traçabilité.

## Version 1.0

- création de la bibliothèque TECH.
