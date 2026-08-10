# ENGINE — Catalogue

> Version : 1.3
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (CHRONIQUES-ENGINE), TECH, QA

---

# Objectif

Ce catalogue référence l'ensemble des documents constituant la
bibliothèque ENGINE.

ENGINE décrit l'architecture fonctionnelle et technique du moteur.

Les règles métier restent définies dans leurs bibliothèques d'autorité,
notamment CORE, GDB et ACT.

Le catalogue distingue :

- les spécifications existantes ;
- les spécifications rédigées rétroactivement ;
- les spécifications rédigées avant implémentation ;
- les documents encore planifiés.

---

# Documents existants

## ENGINE-000 — Principes d'architecture

Statut : Stable.

Définit les principes de gouvernance d'ENGINE, notamment :

- Documentation First ;
- déterminisme ;
- contrats ;
- tests ;
- séparation des responsabilités ;
- validation avant intégration.

---

## ENGINE-001 — Journal d'événements du World

Statut : Stable — v2.0.

Décrit `World.Events`.

Le journal :

- accumule les `GameEvent` observables ;
- ne constitue pas un EventBus Publish/Subscribe ;
- n'est jamais utilisé comme canal de coordination entre Systems.

---

## ENGINE-002 — Kernel

Statut : Stable.

Rédigé rétroactivement.

Documente les primitives du Kernel déjà présentes dans le moteur.

---

## ENGINE-003 — Scheduler et boucle de simulation

Statut : Stable.

Rédigé rétroactivement.

Documente :

- l'avancement du Tick ;
- l'ordre déterministe des Systems ;
- la boucle de simulation actuelle.

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

Rédigé avant implémentation puis implémenté et validé dans
`CHRONIQUES-ENGINE`.

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

Validation courante :

```text
dotnet build
→ succès

dotnet test
→ 122 / 122 tests réussis
→ 0 échec
```

La transmission matérielle incomplète définie conceptuellement par
GDB-004J reste volontairement différée tant que le moteur ne dispose
pas d'une représentation du patrimoine transmissible.

ENGINE-008 participe à la cible v0.3 :

```text
relations
mémoire
compétences
héritage minimal
```

La mémoire reste encore à spécifier séparément.

---

# Documents planifiés mais non créés

## ENGINE-007 — Resource Manager

Gestion future des ressources :

- mémoire ;
- contenu externe chargé ;
- durée de vie des ressources.

Aucun besoin d'implémentation concret ne justifie encore sa création.

Il reste donc réservé mais non spécifié conformément à MASTER-006.

---

# Consolidation de l'organisation initiale

La structure initiale envisageait notamment des documents distincts pour :

- Scheduler ;
- Simulation Loop ;
- Persistence ;
- Serialization.

L'architecture réellement implémentée a montré que certaines
responsabilités sont actuellement indissociables.

Ainsi :

```text
Simulation Loop
→ intégré à ENGINE-003
```

car `Scheduler.Tick` constitue la boucle actuellement implémentée.

Et :

```text
Serialization
→ intégrée à ENGINE-005
```

car persistance et sérialisation sont actuellement portées par le même
ensemble de contrats.

Cette consolidation reflète le code réel.

Si ces responsabilités deviennent un jour techniquement indépendantes,
elles pourront être séparées par une nouvelle spécification.

---

# État de concordance

À la version 1.3 du présent catalogue :

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
```

---

# Historique

## Version 1.3

- `ENGINE-008` passe de Proposition / Maturité 2 à
  **Validée / Maturité 4**.
- Implémentation correspondante confirmée dans `CHRONIQUES-ENGINE`.
- Build confirmé.
- **122 / 122 tests réussis.**
- Ajout des Effects de population et de `PopulationEffectApplicator`.
- `HeritageRefusalEffect` désormais traité par `HeritageSystem`.
- Correction du comportement du plancher familial et ajout des tests
  associés.
- Transmission incomplète explicitement marquée comme différée.
- Mémoire identifiée comme partie de la cible v0.3 restant à spécifier.

## Version 1.2

- `ENGINE-006` validé après implémentation et tests.
- Création d'`ENGINE-008` comme spécification préalable aux Systems de
  population.
- Dépendance GDB ajoutée au catalogue.

## Version 1.1

- Création d'`ENGINE-006` — Action Pipeline.

## Version 1.0

- Création du catalogue lors de la documentation rétroactive
  d'ENGINE-002 à ENGINE-005.
