# ENGINE — Catalogue

> Version : 1.23
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
ENGINE-016  Habitudes génériques minimales           Validée / M4
```

---

# Validation courante

```text
260 / 260 tests réussis
```

Le moteur sait désormais relier :

```text
besoins
+
production
+
circulation entre habitants
+
consommation
+
observation fiable Intent → Action → Outcome
+
formation et évolution génériques d'Habitudes
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

Statut : **Validée / Maturité 4**.

Spécification : `ENGINE-016 v1.2`.

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

Briques validées :

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

Flux validé :

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
↓
érosion éventuelle en cas d'inactivité
```

Invariants confirmés :

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

# Validation technique ENGINE-016

```text
Engine016HabitTests.cs
→ 24 tests

Engine016HabitInvariantTests.cs
→ 3 tests
```

Soit **27 nouveaux tests**.

Base précédente :

```text
233 / 233
```

Validation locale confirmée :

```text
dotnet build
→ succès

dotnet test
→ 260 / 260 tests réussis
→ 0 échec
```

Les 233 tests historiques restent verts et le scénario complet `répétition → formation → Habitude → Intent → Action` est validé.

---

# Frontière restante

ENGINE-016 ne fournit encore :

- aucune Habitude concrète canonique ;
- aucune perturbation par événement significatif ;
- aucun mapping Trait/Habitude concret ;
- aucune Ambition ;
- aucune fairness inter-familles.

Le prochain lot cognitif doit donc rester soumis aux règles concrètes GDB correspondantes avant toute spécialisation métier.

---

# ENGINE-007

ENGINE-007 reste réservé aux ressources techniques du moteur.

---

# HISTORIQUE

## Version 1.23

- ENGINE-016 passe à **Validée / Maturité 4** ;
- suite globale portée à **260 / 260 tests réussis** ;
- 27 tests ENGINE-016 validés ;
- persistance, formation, arbitrage, activation, renforcement, érosion et réutilisation des Habitudes confirmés ;
- aucune Habitude métier canonique ni nouveau Pattern/Verbe ACT introduits ;
- aucune consolidation TECH/roadmap/README déclenchée automatiquement.

## Version 1.22

- création et enregistrement d'ENGINE-016 en Proposition / M2 ;
- framework générique d'Habitudes implémenté ;
- persistance des Habitudes et traces ajoutée ;
- 27 tests ajoutés ;
- total attendu fixé à 260 / 260.

## Version 1.21

- ENGINE-015 validée / M4 à 233 / 233.

## Version 1.20

- création d'ENGINE-015.

## Versions 1.0 à 1.19

- construction progressive des fondations et de l'autonomie jusqu'à la circulation économique minimale.

---

Fin du document
