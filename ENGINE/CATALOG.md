# ENGINE — Catalogue

> Version : 1.19
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
```

---

# Validation courante

```text
224 / 224 tests réussis
```

Le moteur relie maintenant :

```text
besoins
+
production réelle
+
circulation réelle entre habitants
+
consommation réelle
```

---

# ENGINE-014 — Circulation autonome minimale

Statut : Validée / Maturité 4.

Spécification : `ENGINE-014 v1.2`.

Autorités métier :

```text
GDB-004A v1.2
GDB-005E v1.3
GDB-005F v1.2
```

Autorités ACT validées :

```text
Échange
↓
PAT-004 Transfert v1.2 — Officiel / M4
↓
VERB-004 Donner une denrée v1.2 — Officiel / M4
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

Briques ajoutées :

- `FoodProductComponent.ProductKindId` ;
- `FoodTransferOpportunity` ;
- `IVoluntaryFoodTransferResolver` ;
- `VoluntaryFoodTransferIntentSource` ;
- `DonnerDenreeDefinition` ;
- `FoodTransferPlanner` ;
- `FoodTransferExecutionEngine` ;
- `FoodTransferActionEffectApplicator`.

---

# Invariant de transfert validé

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

# Scénario d'intégration validé

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

Le scénario fonctionne sans entrée joueur.

---

# Validation technique

ENGINE-014 ajoute :

```text
Engine014FoodTransferTests.cs
→ 22 tests

Engine014ActClassificationTests.cs
→ 1 test
```

Soit **23 nouveaux tests**.

Base précédente :

```text
201 / 201
```

Validation locale confirmée :

```text
dotnet build
→ succès

dotnet test
→ 224 / 224 tests réussis
→ 0 échec
```

---

# Frontière économique maintenue

L'audit ciblé conclut toujours :

```text
transfert volontaire de denrée
→ autorisé et validé

prix / monnaie / vente / troc réciproque / marché
→ bloqués
```

ENGINE-014 n'introduit donc aucun solde monétaire, coefficient de prix, négociation ou contrepartie automatique.

---

# ENGINE-007

ENGINE-007 reste réservé aux ressources techniques du moteur et n'a aucun lien avec les stocks économiques.

---

# Historique

## Version 1.19

- ENGINE-014 passe à **Validée / Maturité 4** ;
- PAT-004 / VERB-004 passent à **Officiel / Maturité 4** ;
- suite globale portée à **224 / 224 tests réussis** ;
- scénario multi-habitants production → transfert → consommation confirmé ;
- conservation, déterminisme et compatibilité JSON validés ;
- frontière avec prix, monnaie, vente, troc réciproque et marché maintenue ;
- aucune consolidation TECH/roadmap/README déclenchée automatiquement.

## Version 1.18

- ENGINE-014 synchronisé avec GDB-005E v1.3 / GDB-005F v1.2 ;
- invariant `stock source ≠ stock destination` propagé ;
- compatibilité JSON de `ProductKindId` enregistrée ;
- couverture QA fixée à 23 nouveaux tests ;
- total attendu fixé à 224 avant validation.

## Version 1.17

- ajout du test de classification ACT ; total attendu corrigé à 224.

## Version 1.16

- création d'ENGINE-014 en Proposition / M2.

## Version 1.15

- ENGINE-013 validée à 201 / 201.

## Versions 1.0 à 1.14

- construction progressive des fondations et de l'autonomie jusqu'à la production minimale.
