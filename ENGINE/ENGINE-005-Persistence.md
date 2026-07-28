# ENGINE-005 — Persistence et Serialization

> Version : 1.0
> Statut : Stable
> Maturité : 3
> Bibliothèque : ENGINE

⸻

# 1. Objectif

Documenter rétroactivement la sauvegarde et le rechargement d'un `World`
--- implémentés depuis la v0.1 (World vide) puis étendus en v0.2 (Entity
avec Components et Lifecycle), avant la création de la bibliothèque
ENGINE (MASTER-007, Maturité 3).

---

# 2. Principe

Un `World` se sérialise intégralement en JSON, puis se reconstruit à
l'identique à partir de ce JSON --- condition du critère de sortie v0.1
de MASTER-005 : « un World vide se sauvegarde et se recharge à
l'identique. »

La représentation sérialisable (`WorldSnapshot`, `EntitySnapshot`) est
explicite plutôt que polymorphe : un champ nullable par type de
Component, pas un mécanisme générique. `System.Text.Json` ne sérialise
pas nativement un `Dictionary<Type, IComponent>` sans convertisseur
dédié ; tant que le nombre de Components reste petit, l'approche
explicite est plus simple et plus lisible (MASTER-006 : pas
d'anticipation sans motif réel).

---

# 3. Responsabilités

`WorldRepository` est responsable de :

- construire une représentation sérialisable complète d'un `World`
  (`Save`) ;
- reconstruire un `World` fonctionnellement identique à partir de cette
  représentation (`Load`).

Il n'est jamais responsable :

- de décider quels Components existent --- toute extension du modèle de
  données exige d'étendre explicitement `EntitySnapshot` ;
- de préserver l'historique complet des Events d'un Lifecycle --- limite
  assumée (voir section 7).

---

# 4. Architecture

## EntitySnapshot (`Persistence/WorldSnapshot.cs`)

`record` portant `Id` (Guid), `LifecycleCreatedAt` (long),
`LifecycleState` (string), et un champ nullable par Component métier
concret existant : `NeedsComponent?`, `AgeComponent?`. Ajouter un nouveau
Component à ce modèle de données exige d'ajouter un nouveau champ ici,
explicitement.

## WorldSnapshot (`Persistence/WorldSnapshot.cs`)

`record` portant `Seed` (long), `CurrentTick` (long), `Entities`
(`IReadOnlyList<EntitySnapshot>`), `Events`
(`IReadOnlyList<GameEvent>`).

## WorldRepository (`Persistence/WorldRepository.cs`)

Classe statique. `Save(world)` : parcourt `world.Entities`, extrait
`NeedsComponent` et `AgeComponent` de chacune si présents, construit un
`EntitySnapshot` par Entity et un `WorldSnapshot` global, puis sérialise
en JSON indenté (`JsonSerializerOptions { WriteIndented = true }`).

`Load(json)` : désérialise le JSON en `WorldSnapshot` (lève
`InvalidOperationException` si le JSON ne contient pas de snapshot
exploitable), reconstruit le `World` via `World.Restore` (interne,
réservé à la persistance), reconstruit chaque `Entity` via
`Entity.Restore` (également interne --- ce mécanisme ne devient jamais
une API publique de création d'Entity), réattache les Components
présents, réintroduit chaque Entity dans le World via
`World.Reintroduce`, puis réinjecte les Events via
`World.ReplayEvents` (sans passer par `Publish`, pour ne pas les
compter comme nouvellement publiés).

---

# 5. Flux

```mermaid
flowchart LR

A[World.Entities] --> B[EntitySnapshot par Entity]
B --> C[WorldSnapshot]
C --> D[JSON indenté]
D --> E[JsonSerializer.Deserialize]
E --> F[World.Restore]
F --> G[Entity.Restore + Set des Components]
G --> H[World.Reintroduce]
H --> I[World.ReplayEvents]
```

---

# 6. Contrat

`WorldRepository` garantit les invariants suivants.

## Identité stable

Un `EntityId` survit au cycle Save/Load à l'identique --- jamais
régénéré (CORE-002-C, section 3).

## Fidélité du Lifecycle courant

L'instant de création (`CreatedAt`) et l'état courant du Lifecycle
survivent au cycle Save/Load à l'identique.

## Fidélité des Components

Chaque `NeedsComponent` et `AgeComponent` attaché avant Save est
réattaché après Load, avec les mêmes valeurs.

## Fidélité des Events

Le journal d'événements (ENGINE-001) survit au cycle Save/Load dans le
même ordre, sans être recompté comme nouvellement publié.

---

# 7. Invariants

- `Load(Save(world))` produit un World fonctionnellement identique à
  `world` pour tout ce que ce document couvre (identité, Lifecycle
  courant, Components listés, Events, Seed, CurrentTick).
- Un JSON qui ne contient pas de `WorldSnapshot` exploitable ne produit
  jamais un World partiellement reconstruit --- `Load` lève une
  exception avant toute reconstruction.

## Limite assumée

**L'historique complet du Lifecycle n'est pas persisté** --- seuls
`CreatedAt` et l'état courant (`LifecycleState`) survivent au
rechargement. Un personnage rechargé sait qu'il est vivant, en
vieillesse, ou mort, mais la séquence complète des `GameEvent` qui l'ont
mené à cet état n'est pas reconstruite. Documentée explicitement dans le
code (`WorldSnapshot.cs`, `Entity.Restore`) --- à traiter par une future
extension quand un besoin réel l'exigera (MASTER-006), pas avant.

---

# 8. Validation

`WorldRepository` est considéré conforme si :

✓ un World vide se sauvegarde et se recharge à l'identique (critère de
sortie v0.1, MASTER-005) ;

✓ l'état du Lifecycle et les Components (`NeedsComponent`,
`AgeComponent`) survivent au cycle Save/Load ;

✓ les Events survivent au cycle Save/Load, dans l'ordre.

Vérifié par `WorldSerializationTests`, notamment le round-trip complet
de l'état Lifecycle et d'`AgeComponent` après une mort (ajouté lors du
lot cycle de vie, v0.2).

---

# 9. Historique

## Version 1.0

- Documentation rétroactive de la Persistence et Serialization
  (méthodologie MASTER-008 étendue --- voir MASTER-008 v1.2).
  Implémentées depuis la v0.1 (World vide) et étendues en v0.2 (Entity
  avec Components et Lifecycle), avant la création de la bibliothèque
  ENGINE.
