# TECH

> Version : 1.3  
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

## Contenu futur

Les prochains documents TECH seront créés lorsqu'un ensemble technique suffisamment stable nécessite une documentation d'implémentation.

```text
TECH-004
TECH-005
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
...
```

Exemples actuels :

```text
TECH-001 — Systems de population.md
TECH-002 — Boucle de vie minimale.md
TECH-003 — Orchestration des habitants autonomes.md
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

Exemple courant :

```text
MASTER-005 Phase 3
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

# État actuel

```text
Documents numérotés : 3

TECH-001
→ Systems de population
→ Validé

TECH-002
→ Boucle de vie minimale
→ Validé

TECH-003
→ Orchestration des habitants autonomes
→ Validé
```

---

# Historique

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
