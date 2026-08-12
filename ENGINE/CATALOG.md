# ENGINE — Catalogue

> Version : 1.20
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
ENGINE-015  Observation de l'exécution autonome      Proposition / M2
```

---

# Validation courante

Base localement validée avant ENGINE-015 :

```text
224 / 224 tests réussis
```

Le moteur sait déjà relier besoins, production, circulation et consommation sans entrée joueur.

---

# Arbitrage GDB courant

Depuis la synchronisation GDB-004A v1.3 :

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

ENGINE-014 reste valide : GDB-004A v1.3 conserve intégralement ses trois premières familles et ajoute les familles cognitives après la production.

---

# ENGINE-014 — Circulation autonome minimale

Statut : Validée / M4.

Validation :

```text
224 / 224
```

Chaîne validée :

```text
ressource
↓
production par A
↓
stock A
↓
transfert volontaire A → B
↓
stock B
↓
consommation par B
```

La frontière commerciale reste inchangée : prix, monnaie, vente, troc réciproque et marché ne sont pas implémentés.

---

# ENGINE-015 — Observation de l'exécution autonome

Statut : Proposition / Maturité 2.

Spécification : `ENGINE-015 v1.0`.

Autorités :

```text
GDB-004A v1.3
GDB-004E v1.2
GDB-004F v1.2
ACT-002-H
ENGINE-006
ENGINE-010 à ENGINE-014
```

Problème traité :

```text
AutonomousActionSystem
↓
IAutonomousIntentExecutor.Execute(...)
↓
void
```

Le contrat historique masque l'Action et son Outcome aux futurs systèmes d'apprentissage.

ENGINE-015 ajoute sans casser ce contrat :

- `IAutonomousIntentExecutionObserver` ;
- `PipelineAutonomousIntentExecutor`.

Flux :

```text
Intent autonome
↓
BeforeExecution
↓
PipelineRunner.Execute
├── exception → ExecutionAborted → rethrow
└── Action terminée
    ↓
    AfterExecution
```

Invariants :

- `IAutonomousIntentExecutor` inchangé ;
- `AutonomousActionSystem` inchangé ;
- `PipelineRunner` inchangé ;
- ACT `Intent` inchangé ;
- contexte pré-Effects observable ;
- Action archivée + Outcome post-Effects observables ;
- échec métier normal observé par `AfterExecution` ;
- exception technique observée par `ExecutionAborted` puis relancée ;
- aucun comportement d'Habitude ou d'Ambition inventé.

---

# Couverture QA ENGINE-015

Nouveau fichier :

```text
Engine015AutonomousExecutionObservationTests.cs
→ 9 tests
```

Base :

```text
224 / 224
```

Total attendu avant validation locale :

```text
233 / 233
```

Aucun passage M4 ne sera enregistré avant confirmation locale.

---

# Frontière avec les Habitudes

ENGINE-015 prépare GDB-004E mais ne crée pas encore :

- `HabitComponent` ;
- Déclencheur concret ;
- Signature de formation concrète ;
- formation ;
- renforcement ;
- érosion.

Il permet uniquement à un futur système autorisé de distinguer le contexte avant Action du résultat réel après Action.

---

# ENGINE-007

ENGINE-007 reste réservé aux ressources techniques du moteur et n'a aucun lien avec les ressources économiques ou les Habitudes.

---

# HISTORIQUE

## Version 1.20

- création et enregistrement d'ENGINE-015 en Proposition / M2 ;
- ajout de la frontière d'observation avant/après/abandon autour du pipeline autonome ;
- 9 tests ajoutés, total attendu **233 / 233** ;
- aucune modification des contrats historiques d'ENGINE-010 ou d'ACT ;
- aucun passage M4 anticipé.

## Version 1.19

- ENGINE-014 validée / M4 ;
- suite portée à 224 / 224 ;
- PAT-004 / VERB-004 validés ;
- circulation autonome entre habitants confirmée.

## Versions 1.16 à 1.18

- création, QA et synchronisation d'ENGINE-014.

## Version 1.15

- ENGINE-013 validée à 201 / 201.

## Versions 1.0 à 1.14

- construction progressive des fondations et de l'autonomie jusqu'à la production minimale.

---

Fin du document
