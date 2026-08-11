# ENGINE — Catalogue

> Version : 1.16
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (`CHRONIQUES-ENGINE`), TECH, QA

---

# Objectif

Ce catalogue est la source canonique pour la bibliothèque ENGINE.

ENGINE décrit l'architecture fonctionnelle et technique attendue du moteur. Les règles métier restent définies dans leurs bibliothèques d'autorité, notamment CORE, GDB et ACT.

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

# Bloc validé jusqu'à ENGINE-013

La simulation autonome possède déjà :

```text
entretien
+
production réelle
+
consommation réelle
```

Validation courante avant ENGINE-014 :

```text
201 / 201 tests réussis
```

ENGINE-013 démontre qu'un habitant peut produire une denrée à partir d'une ressource réelle puis la consommer ultérieurement.

---

# ENGINE-014 — Circulation autonome minimale

Statut : Proposition.  
Maturité : 2.

Autorités métier :

```text
GDB-004A v1.2
GDB-005E v1.2
GDB-005F v1.1
```

Autorités ACT proposées :

```text
Échange
↓
PAT-004 Transfert
↓
VERB-004 Donner une denrée
```

Flux cible :

```text
NeedsIntentSource
↓ si aucun entretien exécutable
VoluntaryFoodTransferIntentSource
↓ si aucune opportunité
ProductiveActivityIntentSource
↓
Intent éventuel
↓
CompositePlanner
↓
PipelineRunner inchangé
↓
CompositeExecutionEngine
↓
Effects
↓
World
```

ENGINE-014 introduit notamment :

- `FoodProductComponent.ProductKindId` ;
- `FoodTransferOpportunity` ;
- `IVoluntaryFoodTransferResolver` ;
- `VoluntaryFoodTransferIntentSource` ;
- `DonnerDenreeDefinition` ;
- `FoodTransferPlanner` ;
- `FoodTransferExecutionEngine` ;
- `FoodTransferActionEffectApplicator`.

Les compositeurs et le `PipelineRunner` restent structurellement inchangés.

---

# Conservation du transfert

VERB-004 vise :

```text
source P -= q
destination P += q
```

Contraintes du premier lot :

- `q > 0` ;
- donneur et destinataire distincts ;
- source et destination distinctes ;
- source suffisamment disponible ;
- `ProductKindId` non vide et identique ;
- même valeur `FaimRestauree` pour éviter une fusion de représentations incompatibles ;
- aucun besoin modifié directement ;
- aucun prix ou paiement créé.

---

# Scénario d'intégration cible

```text
Tick N
Habitant A
↓
produire_denree
↓
stock alimentaire A = 1

Tick N+1
A traité avant B
↓
A → donner_denree → B
↓
stock A = 0
stock B = 1
↓
B est affamé
↓
B → manger
↓
stock B = 0
Faim B ↑
```

Le scénario doit fonctionner sans entrée joueur.

---

# Couverture QA en attente de validation locale

`Engine014FoodTransferTests.cs` ajoute **22 `[Fact]`**.

Base validée avant ce lot :

```text
201 / 201
```

Total attendu après validation :

```text
223 tests
```

Aucun passage M4 n'est enregistré avant résultat local confirmé.

---

# Frontière avec l'économie commerciale

L'audit `AUDIT-CIRCULATION-ECONOMIQUE-Minimale.md` conclut :

```text
transfert volontaire de denrée
→ autorisé

prix / monnaie / vente / troc réciproque / marché
→ toujours bloqués
```

ENGINE-014 ne doit donc introduire aucun coefficient de prix, solde monétaire ou négociation implicite.

---

# ENGINE-007 — Resource Manager

ENGINE-007 reste réservé aux ressources techniques du moteur et n'a aucun lien avec les stocks économiques de ce lot.

---

# Convention de nommage

Le catalogue canonique unique est :

```text
ENGINE/CATALOG.md
```

---

# Historique

## Version 1.16

- création d'ENGINE-014 — Circulation autonome minimale en Proposition / Maturité 2 ;
- ouverture de PAT-004 / VERB-004 ;
- identité de produit transférable ajoutée ;
- opportunité volontaire injectable ;
- ordre autonome `entretien → transfert → production` ;
- transfert conservatif entre deux habitants ;
- 22 nouveaux tests ajoutés, total attendu 223 ;
- scénario cible production → transfert → consommation ;
- prix, monnaie et marché maintenus hors périmètre ;
- aucune consolidation TECH/roadmap/README avant validation.

## Version 1.15

- ENGINE-013 validée / Maturité 4 ;
- suite portée à 201 / 201.

## Versions 1.0 à 1.14

- création et consolidation progressive des fondations moteur jusqu'à la production autonome minimale.
