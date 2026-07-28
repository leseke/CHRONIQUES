# ENGINE-002 — Kernel

> Version : 1.0
> Statut : Stable
> Maturité : 3
> Bibliothèque : ENGINE

⸻

# 1. Objectif

Documenter rétroactivement les primitives du Kernel du moteur Chroniques
--- implémentées dès la v0.1, avant la création de la bibliothèque
ENGINE. Ce document ne précède donc pas le code : il le décrit tel qu'il
existe (MASTER-007, Maturité 3 --- « le document correspond au code
existant, identifiant pour identifiant »).

Chaque primitive implémente une primitive conceptuelle définie par CORE.
Ce document ne redéfinit aucune de ces primitives conceptuelles : il
documente uniquement leur implémentation --- classe, invariants
techniques, relations entre elles dans le code.

---

# 2. Principe

Le Kernel ne contient aucune donnée métier ni aucune règle de jeu
(ENGINE-000, section 8 --- Infrastructure indépendante). Il fournit
uniquement les primitives neutres sur lesquelles s'appuient les Systems
(v0.2) puis ACT (v0.3).

Toute primitive du Kernel est un point d'ancrage ou un conteneur ---
jamais un exécutant. Décider, exécuter une logique ou déclencher un
Event sont des responsabilités interdites au Kernel : elles appartiennent
aux Systems (CORE-003-C), qui vivent dans leur propre dossier, jamais
dans `Kernel/`.

---

# 3. Responsabilités

Le Kernel est responsable de :

- fournir une identité stable et neutre pour toute entité simulée
  (EntityId, Entity) ;
- fournir un conteneur typé sans comportement pour toute donnée simple
  (Value\<T\>) ;
- fournir une représentation d'une condition à un instant donné (State) ;
- fournir un lien qualifié entre deux Entity (Relation) ;
- fournir un ordre de simulation (Tick) et une localisation minimale
  (SpaceRef) ;
- fournir la continuité d'une Entity dans le temps (Lifecycle) ;
- assembler ces primitives sans y ajouter de sens métier (World) ;
- garantir la reproductibilité de tout tirage aléatoire
  (DeterministicRandom).

Il n'est jamais responsable :

- de décider si une Action est possible (ACT) ;
- de faire progresser un Lifecycle ou un State (les Systems, ex.
  `AgingSystem`) ;
- de donner un sens concret à une localisation (GDB-003) ;
- de la sauvegarde ou du rechargement (Persistence, ENGINE-005).

---

# 4. Architecture

## EntityId (`Kernel/EntityId.cs`)

`readonly record struct` enveloppant un `Guid`. Implémente CORE-002-C :
l'identité ne porte aucune signification métier --- elle distingue une
Entity de toutes les autres, rien de plus. `EntityId.New()` garantit
l'unicité.

## IComponent (`Kernel/IComponent.cs`)

Interface marqueur, vide. Toute donnée conceptuelle attachée à une
Entity implémente `IComponent` (CORE-003). Un Component ne contient
jamais de logique (CORE-003-C) ; un même type de Component n'existe
qu'une fois par Entity (responsabilité unique).

## Value\<T\> (`Kernel/Value.cs`)

`readonly record struct` générique, conteneur typé sans comportement
(CORE-004). Conversions implicites vers/depuis `T` pour un usage
transparent. Un State s'appuie sur une ou plusieurs Value pour porter
ses données.

## State (`Kernel/State.cs`)

Classe portant un `Name` et un dictionnaire `string → object?` alimenté
via `Set<T>(clé, Value<T>)` (CORE-005). Un State décrit une condition,
il ne provoque jamais d'action par lui-même.

## Relation (`Kernel/Relation.cs`)

Classe portant `Source` et `Target` (deux `EntityId`), un `Kind`
(string) et un `State` (CORE-006). Une Relation n'existe jamais sans les
deux Entity qu'elle relie --- elles sont fournies au constructeur, non
optionnelles.

## Tick (`Kernel/Tick.cs`)

`readonly record struct` enveloppant un `long`, avec `IComparable<Tick>`
et les opérateurs de comparaison (CORE-008). Un Tick est un rang dans la
séquence de simulation, jamais une durée réelle --- la conversion vers
un temps de jeu habité (mois, saisons, années) est définie par
`Systems.CalendrierSimule` (ENGINE-004), pas par le Kernel.

## SpaceRef (`Kernel/SpaceRef.cs`)

`readonly record struct` enveloppant un `EntityId` (CORE-009). Pour le
noyau minimal, une localisation référence simplement l'Entity qui
représente le lieu ; la hiérarchie géographique complète relève de GDB
et n'est pas encore modélisée.

## Lifecycle (`Kernel/Lifecycle.cs`)

Classe portant `CreatedAt` (Tick), `CurrentState` (State, mutable
uniquement via `Record`) et un historique `List<GameEvent>` exposé en
lecture seule (CORE-010). `Record(event, newState?)` ajoute
systématiquement l'événement à l'historique et, si `newState` est
fourni, fait progresser `CurrentState`. Le Lifecycle lui-même ne décide
jamais de progresser : c'est toujours un System (ex. `AgingSystem`,
ENGINE-004) qui appelle `Record`.

## DeterministicRandom (`Kernel/DeterministicRandom.cs`)

Enveloppe un `System.Random` initialisé avec une graine fixe
(`seed.GetHashCode()`), garantissant qu'à graine identique, la séquence
de tirages est identique (MASTER-002, Principe 10 --- déterminisme).
Expose `Next(min, max)` et `NextDouble()`.

## Entity (`Kernel/Entity.cs`)

Classe portant un `EntityId`, un `Lifecycle` (obligatoire depuis v0.2,
CORE-002-H), et un dictionnaire `Type → IComponent`. `Set<T>`,
`TryGet<T>`, `Has<T>` et `Remove<T>` gèrent l'attachement des Components
par type. `Entity.Create(createdAt?)` crée une identité fraîche avec un
Lifecycle initial dans l'état `"vivant"`. `Entity.Restore(...)` (interne,
réservé à `Persistence.WorldRepository`) reconstruit une Entity
existante sans passer par `Create`, pour préserver l'identité stable
exigée par CORE-002-C.

## World (`Kernel/World.cs`)

Classe assemblant les Entity (`Dictionary<EntityId, Entity>`), le
`Seed`, le `CurrentTick`, le `DeterministicRandom`, et le journal
d'événements (ENGINE-001). `Spawn()` crée et enregistre une nouvelle
Entity. `Advance()` fait progresser `CurrentTick` d'un rang. Le World
n'attribue lui-même aucun sens métier : c'est un conteneur, pas un
System (CORE-000-G).

---

# 5. Flux

Cycle de vie typique d'une Entity dans le Kernel, tel qu'exercé par les
tests existants :

```mermaid
flowchart LR

A[World.Spawn] --> B[Entity.Create]
B --> C[Lifecycle initial: vivant]
C --> D[Entity.Set des Components]
D --> E[World._entities]
```

Aucune étape de ce flux ne dépend d'un Tick précis ni d'une règle de
jeu : c'est un cycle purement structurel.

---

# 6. Contrat

Le Kernel garantit les invariants suivants.

## Identité

Un `EntityId` ne change jamais après création. Deux `EntityId` distincts
ne désignent jamais la même Entity.

## Lifecycle obligatoire

Toute Entity créée via `Entity.Create` ou `Entity.Restore` possède un
Lifecycle non nul, dans un état initial cohérent (`"vivant"` à la
création ; l'état persisté au rechargement).

## Unicité des Components

Un type de Component donné n'est jamais présent plus d'une fois sur une
même Entity --- `Set<T>` remplace, il n'ajoute jamais un doublon.

## Déterminisme

À graine identique, `DeterministicRandom` produit toujours la même
séquence de tirages, au sein d'une même version majeure de .NET.

## Neutralité

Aucune primitive du Kernel ne contient de logique de décision, de
donnée métier ou de référence à un concept de jeu concret (personnage,
métier, lieu nommé...).

---

# 7. Invariants

- Une Entity possède toujours exactement un `EntityId` et un
  `Lifecycle`, jamais zéro, jamais plusieurs.
- Un `Tick` ne décroît jamais au sein d'un même World.
- Un `GameEvent` enregistré dans un `Lifecycle.History` n'est jamais
  retiré ni modifié.
- Le Kernel ne dépend d'aucun autre composant du moteur (Systems,
  Persistence, ACT) --- la dépendance est toujours dans l'autre sens.

---

# 8. Validation

Le Kernel est considéré conforme si :

✓ chaque primitive correspond exactement à sa primitive conceptuelle
CORE (CORE-002 à CORE-010) ;

✓ aucune primitive ne contient de logique de décision ;

✓ `World`, `Entity` et `Lifecycle` respectent les invariants de la
section 7.

Vérifié par les tests unitaires existants, un fichier par primitive ou
groupe de primitives : `EntityTests`, `ComponentTests`, `TickTests`,
`GameEventTests`, `LifecycleTests`, `DeterministicRandomTests`, et
`WorldSerializationTests` pour le cycle sauvegarde/rechargement complet
du World (voir ENGINE-005, Persistence).

---

# 9. Historique

## Version 1.0

- Documentation rétroactive du Kernel (méthodologie MASTER-008 étendue
  --- voir MASTER-008 v1.2). Le Kernel est implémenté depuis la v0.1 du
  moteur, avant la création de la bibliothèque ENGINE ; ce document
  comble ce vide plutôt que de laisser le Kernel sans spécification
  ENGINE. Maturité fixée directement à 3 (Implémentation) : le contenu
  décrit le code existant, il ne le précède pas.
