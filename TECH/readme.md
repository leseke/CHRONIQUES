# TECH

> Version : 1.1  
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

---

## Contenu futur

Les prochains documents TECH devront être créés lorsqu'un ensemble technique suffisamment stable nécessite une documentation d'implémentation.

Exemples possibles :

```text
TECH-002
TECH-003
TECH-004
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

Exemple actuel :

```text
TECH-001-SystemsDePopulation.md
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

La bibliothèque est désormais active.

```text
Documents numérotés : 1

TECH-001
→ Systems de population
→ Validé
```

---

# Historique

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
