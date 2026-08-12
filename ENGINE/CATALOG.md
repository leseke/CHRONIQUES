# ENGINE — Catalogue

> Version : 1.24
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
ENGINE-017  Ambitions génériques minimales           Proposition / M2
```

---

# Validation courante

Base localement validée avant ENGINE-017 :

```text
260 / 260 tests réussis
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

# ENGINE-016 — Habitudes génériques minimales

Statut : Validée / M4.

Validation :

```text
260 / 260
```

Le moteur sait désormais former, persister, sélectionner, activer, renforcer et éroder des Habitudes génériques à partir de règles injectées, sans Habitude métier canonique ni nouveau Verbe ACT.

---

# ENGINE-017 — Ambitions génériques minimales

Statut : Proposition / Maturité 2.

Spécification : `ENGINE-017 v1.1`.

Autorités :

```text
GDB-004A v1.3
GDB-004D v1.3
GDB-004F v1.2
ACT-002-H
ENGINE-010
ENGINE-016
```

Briques candidates :

```text
AmbitionComponent
AmbitionState
AmbitionCreationCandidate
AmbitionEvaluation
IAmbitionRule
AmbitionEvolutionSystem
AmbitionIntentSource
```

Persistance étendue :

```text
EntitySnapshot
WorldRepository
```

Flux candidat :

```text
règle d'Ambition injectée
↓
création déterministe
↓
Ambition persistante
↓
évaluation du Progrès
↓
Ambition candidate
↓
Intensité → Progrès → ancienneté
↓
AmbitionIntentSource
↓
Intent
↓
ACT
```

Invariants :

- aucun Type d'Ambition concret par défaut ;
- Objectif porté par payload opaque ;
- identité technique `AmbitionTypeId + InstanceKey` ;
- aucune duplication ;
- Progrès et Intensité bornés `[0,100]` ;
- Intensité 0 supprimée par l'évolution ;
- accomplissement et abandon non candidats ;
- règle absente ou Intent non traitable : aucun faux Intent ;
- sélection Intensité → Progrès → ancienneté ;
- source d'Intent sans mutation du World ;
- aucun PersonalityComponent, Opportunité PNJ, nouveau Pattern ou Verbe ACT.

---

# Couverture QA ENGINE-017

```text
Engine017AmbitionTests.cs
→ 25 tests

Engine017AmbitionInvariantTests.cs
→ 6 tests
```

Nouveaux tests : **31**.

Base :

```text
260 / 260
```

Total attendu avant validation locale :

```text
291 / 291
```

Aucun passage M4 ne sera enregistré avant confirmation locale.

---

# Frontières restantes

Le moteur ne fournit encore :

- aucun Type concret d'Ambition ;
- aucun PersonalityComponent ;
- aucun mapping Trait/Ambition concret ;
- aucune formule universelle d'évolution de l'Intensité ;
- aucune Opportunité PNJ générique ;
- aucune fairness inter-familles.

Les frontières commerciales de prix, monnaie, vente, troc réciproque et marché restent également inchangées.

---

# ENGINE-007

ENGINE-007 reste réservé aux ressources techniques du moteur.

---

# HISTORIQUE

## Version 1.24

- création et enregistrement d'ENGINE-017 en Proposition / M2 ;
- framework générique d'Ambitions implémenté ;
- création, Progrès, accomplissement, abandon, sélection et persistance couverts ;
- 31 tests ajoutés ;
- total attendu fixé à **291 / 291** ;
- aucun Type concret, Trait, Opportunité PNJ ou nouveau Verbe ACT introduit.

## Version 1.23

- ENGINE-016 validée / M4 à 260 / 260 ;
- framework générique d'Habitudes fermé.

## Version 1.22

- création d'ENGINE-016.

## Version 1.21

- ENGINE-015 validée / M4 à 233 / 233.

## Version 1.20

- création d'ENGINE-015.

## Versions 1.0 à 1.19

- construction progressive des fondations et de l'autonomie jusqu'à la circulation économique minimale.

---

Fin du document
