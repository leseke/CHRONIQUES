# ENGINE — Catalogue

> Version : 1.22
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (`CHRONIQUES-ENGINE`), TECH, QA

---

# Objectif

Ce catalogue est la source canonique pour la bibliothèque ENGINE.

ENGINE décrit l'architecture attendue du moteur. Les règles métier restent définies dans leurs autorités amont.

---

# Documents existants

```text
ENGINE-000  Principes d'architecture                  Stable
ENGINE-001  Journal d'événements du World            Stable
ENGINE-002  Kernel                                   Stable
ENGINE-003  Scheduler et boucle de simulation        Stable
ENGINE-004  Systems de simulation                    Stable
ENGINE-005  Persistence et Serialization             Stable
ENGINE-006  Action Pipeline                          Validée / M4
ENGINE-007  Resource Manager                         Réservé / non créé
ENGINE-008  Systems de population                    Validée / M4
ENGINE-009  Boucle de vie minimale                   Validée / M4
ENGINE-010  Orchestration habitants autonomes        Validée / M4
ENGINE-011  Décision autonome par besoins            Validée / M4
ENGINE-012  Alimentation autonome minimale           Validée / M4
ENGINE-013  Production autonome minimale             Validée / M4
ENGINE-014  Circulation autonome minimale            Validée / M4
ENGINE-015  Observation de l'exécution autonome      Validée / M4
ENGINE-016  Habitudes génériques minimales           Proposition / M2
```

---

# Validation courante

Base localement validée avant ENGINE-016 :

```text
233 / 233 tests réussis
```

---

# Arbitrage GDB courant

```text
besoins physiologiques actionnables
↓
transfert volontaire exécutable
↓
activité productive exécutable
↓
Habitudes actives
↓
Ambitions candidates
↓
aucun Intent
```

GDB-004A v1.3 reste l'autorité sur cet ordre. Force et Intensité restent internes à leurs familles.

---

# ENGINE-015 — Observation autonome

Statut : Validée / M4.

Validation :

```text
233 / 233
```

ENGINE-015 fournit l'observation pré/post exécution nécessaire aux systèmes d'apprentissage sans modifier `IAutonomousIntentExecutor`, `AutonomousActionSystem`, `PipelineRunner` ou ACT `Intent`.

---

# ENGINE-016 — Habitudes génériques minimales

Statut : Proposition / Maturité 2.

Spécification : `ENGINE-016 v1.1`.

Autorités :

```text
GDB-004A v1.3
GDB-004D v1.3
GDB-004E v1.2
ACT-002-H
ENGINE-010
ENGINE-015
```

Le lot introduit un framework générique, pas une Habitude métier canonique.

Briques candidates :

```text
HabitComponent
IHabitRule
IHabitFormationParameterResolver
IHabitStrengthPolicy
HabitSelectionRegistry
HabitIntentSource
HabitLearningObserver
HabitEvolutionSystem
```

Persistance étendue :

```text
EntitySnapshot
WorldRepository
```

Flux cible :

```text
Intent exécuté
↓
répétition + Signature déterministe
↓
formation d'une Habitude
↓
Déclencheur concret
↓
HabitIntentSource
↓
Intent
↓
ACT
↓
Outcome
↓
activation / renforcement
```

Invariants :

- aucune règle concrète par défaut ;
- aucune métadonnée d'Habitude ajoutée à ACT Intent ;
- source d'Intent sans mutation du World ;
- sélection Force puis ancienneté ;
- échec métier : formation/activation possibles, pas de renforcement ;
- exception technique : pas de formation/renforcement, activation déjà produite conservée ;
- renforcement monotone non décroissant ;
- érosion monotone non croissante ;
- Force bornée `[0,100]` ;
- suppression à Force 0 ;
- aucun nouveau Pattern ou Verbe ACT.

---

# Couverture QA ENGINE-016

```text
Engine016HabitTests.cs
→ 24 tests

Engine016HabitInvariantTests.cs
→ 3 tests
```

Nouveaux tests : **27**.

Base :

```text
233 / 233
```

Total attendu avant validation locale :

```text
260 / 260
```

Aucun passage M4 ne sera enregistré avant confirmation locale.

---

# Frontière restante

ENGINE-016 ne fournit encore :

- aucune Habitude concrète ;
- aucune perturbation par événement significatif ;
- aucun mapping Trait/Habitude concret ;
- aucune Ambition ;
- aucune fairness inter-familles.

---

# ENGINE-007

ENGINE-007 reste réservé aux ressources techniques du moteur.

---

# HISTORIQUE

## Version 1.22

- création et enregistrement d'ENGINE-016 en Proposition / M2 ;
- framework générique d'Habitudes implémenté ;
- persistance des Habitudes et traces ajoutée ;
- formation, sélection, activation, renforcement et érosion couverts ;
- 27 tests ajoutés ;
- total attendu fixé à **260 / 260** ;
- aucune Habitude métier ni nouveau Verbe ACT introduits.

## Version 1.21

- ENGINE-015 validée / M4 à 233 / 233.

## Version 1.20

- création d'ENGINE-015.

## Versions 1.0 à 1.19

- construction progressive des fondations et de l'autonomie jusqu'à la circulation économique minimale.

---

Fin du document
