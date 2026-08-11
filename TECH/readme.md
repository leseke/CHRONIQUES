# TECH

> Version : 1.2  
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

Le workflow de référence est :

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
Implémentation
↓
Tests
↓
TECH
```

Les responsabilités sont donc distinctes.

### GDB

Définit les règles de simulation.

### ACT

Définit les contrats relatifs aux actions.

### ENGINE

Définit l'architecture attendue du moteur.

### CHRONIQUES-ENGINE

Contient l'implémentation exécutable.

### TECH

Documente l'implémentation réellement obtenue et validée.

---

## Objectifs

TECH permet de :

- documenter l'architecture réellement implémentée ;
- conserver la traçabilité entre spécification et code ;
- expliquer les choix techniques ;
- documenter les corrections importantes ;
- faciliter la maintenance ;
- faciliter les audits ;
- documenter les limites connues ;
- conserver l'état de validation des composants.

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

Statut :

```text
Validé
```

Documente l'implémentation de :

- `RelationComponent` ;
- `RelationSystem` ;
- `SkillComponent` ;
- `SkillSystem` ;
- `HeritageSystem` ;
- `RelationInteractionEffect` ;
- `SkillPracticeEffect` ;
- `HeritageRefusalEffect` ;
- `PopulationEffectApplicator`.

Spécification d'origine :

```text
ENGINE-008
```

État de validation initial :

```text
dotnet build
→ succès

dotnet test
→ 122 / 122 réussis
```

### TECH-002 — Boucle de vie minimale

Statut :

```text
Validé
```

Documente l'implémentation de :

- `LifeSession` ;
- `LifeSessionState` ;
- orchestration de `Scheduler.Tick(World)` ;
- détection de la mort via `Lifecycle` ;
- lecture observable de `heritage.transmission` ;
- passage du contrôle à l'héritier ;
- terminaison sans successeur ;
- invariants QA et déterminisme de la séquence de contrôle ;
- test d'intégration de continuité v0.3.

Spécification d'origine :

```text
ENGINE-009
```

État de validation initial :

```text
dotnet build
→ succès

dotnet test
→ 134 / 134 réussis
```

---

## Contenu futur

Les prochains documents TECH devront être créés lorsqu'un ensemble technique suffisamment stable nécessite une documentation d'implémentation.

Exemples possibles :

```text
TECH-003
TECH-004
TECH-005
```

Leur sujet n'est pas réservé à l'avance.

Le numéro suivant est attribué uniquement lorsqu'un besoin concret apparaît.

---

## Ce que TECH peut documenter

TECH peut notamment couvrir :

- architecture logicielle réelle ;
- structure des projets ;
- implémentations des Systems ;
- persistance ;
- sérialisation ;
- mécanismes d'Actions ;
- performance ;
- diagnostic ;
- outils de développement ;
- choix de structures de données ;
- contraintes techniques observées.

---

## Ce que TECH ne doit pas définir

TECH ne doit pas devenir l'autorité sur :

- comportement des habitants ;
- économie ;
- relations ;
- psychologie ;
- actions conceptuelles ;
- Game Design ;
- règles de progression.

Ces responsabilités appartiennent aux bibliothèques amont.

---

## Convention

Chaque document utilise un identifiant unique.

```text
TECH-001
TECH-002
TECH-003
...
```

Le nom doit décrire l'implémentation couverte.

Exemples actuels :

```text
TECH-001 — Systems de population.md
TECH-002 — Boucle de vie minimale.md
```

---

## Traçabilité

Chaque document TECH doit, lorsque possible, identifier :

```text
Spécification source
↓
Code concerné
↓
Tests concernés
```

Exemple :

```text
ENGINE-009
↓
LifeSession.cs
↓
LifeSessionTests.cs
↓
TECH-002
```

---

## Dépendances

TECH dépend principalement de :

- MASTER ;
- CORE ;
- GDB ;
- ACT ;
- ENGINE ;
- code réellement présent dans `CHRONIQUES-ENGINE` ;
- résultats de tests.

TECH ne remplace aucune de ces sources.

---

# État actuel

La bibliothèque est active.

```text
Documents numérotés : 2

TECH-001
→ Systems de population
→ Validé

TECH-002
→ Boucle de vie minimale
→ Validé
```

---

# Historique

## Version 1.2

- ajout de `TECH-002 — Boucle de vie minimale` ;
- enregistrement de la validation ENGINE-009 ;
- état de validation du moteur porté à **134 / 134 tests réussis** pour le lot ENGINE-009 ;
- nombre de documents numérotés porté à 2.

## Version 1.1

- bibliothèque passée de Fondation à Active ;
- création du premier document numéroté ;
- ajout de `TECH-001 — Systems de population` ;
- clarification du rôle de TECH par rapport à ENGINE ;
- ajout de la traçabilité spécification → code → tests → TECH ;
- suppression de la mention selon laquelle aucun document TECH n'existe.

## Version 1.0

- création avec en-tête conforme à MASTER-004 ;
- clarification initiale du périmètre ;
- bibliothèque créée avant l'existence de toute implémentation TECH documentée.
