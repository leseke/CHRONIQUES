# ENGINE — Catalogue

> Version : 1.18
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
ENGINE-014  Circulation autonome minimale            Proposition / M2
```

---

# État validé avant ENGINE-014

```text
201 / 201 tests réussis
```

Le moteur sait déjà relier :

```text
besoins
+
production réelle
+
consommation réelle
```

---

# ENGINE-014 — Circulation autonome minimale

Statut : Proposition / Maturité 2.

Spécification courante : `ENGINE-014 v1.1`.

Autorités métier :

```text
GDB-004A v1.2
GDB-005E v1.3
GDB-005F v1.2
```

Autorités ACT :

```text
Échange
↓
PAT-004 Transfert v1.1 — Proposition / M2
↓
VERB-004 Donner une denrée v1.1 — Proposition / M2
```

Ordre autonome minimal :

```text
1. entretien actionnable
2. transfert volontaire exécutable
3. production exécutable
4. aucun Intent
```

Flux moteur :

```text
CompositeAutonomousIntentSource
↓
Intent
↓
CompositePlanner
↓
PipelineRunner inchangé
↓
CompositeExecutionEngine
↓
IActionEffectApplicator
↓
World
```

Nouvelles briques :

- `FoodProductComponent.ProductKindId` ;
- `FoodTransferOpportunity` ;
- `IVoluntaryFoodTransferResolver` ;
- `VoluntaryFoodTransferIntentSource` ;
- `DonnerDenreeDefinition` ;
- `FoodTransferPlanner` ;
- `FoodTransferExecutionEngine` ;
- `FoodTransferActionEffectApplicator`.

---

# Invariant de transfert

```text
source P -= q
destination P += q
```

avec :

- `q > 0` ;
- donneur ≠ destinataire ;
- stock source ≠ stock destination ;
- identité `ProductKindId` non vide et identique ;
- représentation alimentaire compatible ;
- source suffisamment disponible ;
- conservation exacte des portions ;
- aucun besoin restauré directement ;
- aucun prix ou paiement implicite.

L'Execution Engine ne mute pas le World.

L'applicateur revalide l'opportunité et les Cibles avant mutation puis applique le transfert avec contrôle d'overflow.

---

# Persistance

`ProductKindId` est persisté avec `FoodProductComponent`.

Lorsqu'il est `null`, le champ est omis du JSON afin de conserver la compatibilité de forme avec les anciens produits.

---

# Scénario d'intégration cible

```text
Tick N
A produit une denrée
↓
stock A = 1

Tick N+1
A donne la denrée à B
↓
stock A = 0
stock B = 1
↓
B, traité ensuite, mange
↓
stock B = 0
Faim B ↑
```

Le scénario doit fonctionner sans entrée joueur.

---

# Couverture QA pré-validation

```text
Engine014FoodTransferTests.cs
→ 22 tests

Engine014ActClassificationTests.cs
→ 1 test
```

Nouveaux tests : **23**.

Base précédente :

```text
201 / 201
```

Total attendu :

```text
224 / 224
```

Aucun passage M4 ne sera enregistré avant confirmation locale.

---

# Frontière économique maintenue

L'audit ciblé conclut :

```text
transfert volontaire de denrée
→ autorisé

prix / monnaie / vente / troc réciproque / marché
→ bloqués
```

ENGINE-014 n'introduit donc aucun solde monétaire, coefficient de prix, négociation ou contrepartie automatique.

---

# ENGINE-007

ENGINE-007 reste réservé aux ressources techniques du moteur et n'a aucun lien avec les stocks économiques.

---

# Historique

## Version 1.18

- ENGINE-014 synchronisé avec GDB-005E v1.3 / GDB-005F v1.2 ;
- PAT-004 / VERB-004 v1.1 enregistrés ;
- invariant `stock source ≠ stock destination` propagé ;
- compatibilité JSON de `ProductKindId` enregistrée ;
- couverture QA fixée à 23 nouveaux tests ;
- total attendu fixé à **224 / 224** ;
- aucun passage M4 anticipé.

## Version 1.17

- ajout du test de classification ACT ; total attendu corrigé à 224.

## Version 1.16

- création d'ENGINE-014 en Proposition / M2.

## Version 1.15

- ENGINE-013 validée à 201 / 201.

## Versions 1.0 à 1.14

- construction progressive des fondations et de l'autonomie jusqu'à la production minimale.
