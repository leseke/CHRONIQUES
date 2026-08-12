# TECH-005 — Production et circulation autonomes

> Version : 1.0  
> Statut : Validé  
> Maturité : 4  
> Bibliothèque : TECH  
> Implémentation : `CHRONIQUES-ENGINE`  
> Spécifications : `ENGINE-013`, `ENGINE-014`  
> Validation de référence : `291 / 291 tests réussis`

---

# 1. Objectif

Documenter l'implémentation réellement obtenue et validée du premier bloc économique autonome de Chroniques :

```text
ressource réelle
↓
production autonome
↓
stock alimentaire
↓
transfert volontaire entre habitants
↓
consommation par le destinataire
```

TECH-005 ne définit aucune règle économique nouvelle. Il consolide les implémentations validées d'ENGINE-013 et ENGINE-014.

---

# 2. Autorités

Chaîne principale :

```text
MASTER-005 Phase 3
↓
GDB-004A
GDB-005C / GDB-005E / GDB-005F
GDB-012B / GDB-012E
↓
PAT-003 Production
VERB-003 Produire une denrée
PAT-004 Transfert
VERB-004 Donner une denrée
↓
ENGINE-013 / ENGINE-014
↓
CHRONIQUES-ENGINE
↓
Tests
↓
TECH-005
```

Les contrats commerciaux avancés restent hors périmètre : prix, monnaie, vente, marché, salaire et négociation ne sont pas autorisés par ce bloc.

---

# 3. Production autonome

ENGINE-013 a ajouté :

```text
ResourceStockComponent
ProductionOperation
IProductiveActivityResolver
ProductiveActivityIntentSource
CompositeAutonomousIntentSource
ProduireDenreeDefinition
ProductionPlanner
CompositePlanner
ProductionExecutionEngine
CompositeExecutionEngine
ProductionProvenanceComponent
ProductionActionEffectApplicator
```

Le chemin réel est :

```text
aucun besoin prioritaire exécutable
+
opération productive exécutable
↓
Intent produire_denree
↓
ProductionPlanner
↓
Action ProduireDenree
↓
Outcome réussi
↓
stock d'entrée consommé
+
portions alimentaires créées
+
provenance persistée
```

L'Execution Engine valide sans muter le World. La mutation reste dans l'applicateur d'Effects.

---

# 4. Composition sans spécialiser PipelineRunner

La troisième Action réelle n'a pas provoqué de `switch` métier dans `PipelineRunner`.

Le moteur a introduit :

```text
CompositeAutonomousIntentSource
CompositePlanner
CompositeExecutionEngine
```

Ces compositeurs routent les sources, objectifs et Verbes explicitement enregistrés.

Le runner conserve son cycle générique :

```text
Intent
→ Plan
→ ActionInstance
→ Outcome
→ Effects
→ Archived
```

---

# 5. Stock et provenance

`ResourceStockComponent` représente une quantité matérielle minimale sans unité, propriété ou prix universels.

`ProductionProvenanceComponent` conserve les traces durables :

```text
OperationId
InputResourceId
ProducedAt
```

La provenance complète `World.Events` sans transformer celui-ci en EventBus.

Les deux Components sont persistés par `WorldRepository`.

---

# 6. Circulation volontaire

ENGINE-014 a ajouté :

```text
FoodProductComponent.ProductKindId
FoodTransferOpportunity
IVoluntaryFoodTransferResolver
VoluntaryFoodTransferIntentSource
DonnerDenreeDefinition
FoodTransferPlanner
FoodTransferExecutionEngine
FoodTransferActionEffectApplicator
```

Flux réel :

```text
opportunité volontaire exécutable
↓
Intent donner_denree
↓
Plan
↓
source + destination + destinataire
↓
Action DonnerDenree
↓
source -= q
+
destination += q
```

Le transfert ne restaure aucun besoin. Le destinataire doit ensuite passer par `VERB-002 — Manger`.

---

# 7. Identité et conservation

Pour transférer des portions entre deux stocks, ENGINE-014 exige notamment :

```text
donneur != destinataire
stock source != stock destination
ProductKindId source == ProductKindId destination
FaimRestauree compatible
q > 0
stock source suffisant
```

Invariant :

```text
source avant + destination avant
=
source après + destination après
```

Aucune portion n'est créée par le transfert.

---

# 8. Ordre autonome consolidé du bloc économique

À la fin d'ENGINE-014 :

```text
NeedsIntentSource
↓ sinon
VoluntaryFoodTransferIntentSource
↓ sinon
ProductiveActivityIntentSource
```

La première source non-null gagne. Aucun score universel entre entretien, échange et production n'est calculé.

Cet ordre a ensuite été prolongé par ENGINE-016/017 pour les familles cognitives sans remettre en cause le bloc économique.

---

# 9. Scénario multi-habitants validé

```text
Tick N
A produit une denrée
↓
stock A = 1

Tick N+1
A transfère volontairement la denrée à B
↓
stock A = 0
stock B = 1
↓
B, traité ensuite, mange
↓
stock B = 0
Faim B restaurée
```

Ce scénario démontre un premier flux matériel entre habitants sans intervention joueur.

---

# 10. Persistance

Sont persistés :

- `ResourceStockComponent` ;
- `ProductionProvenanceComponent` ;
- `FoodProductComponent.ProductKindId` lorsqu'il existe ;
- quantités et portions des stocks.

`ProductKindId = null` est omis du JSON afin de préserver la forme historique des produits antérieurs.

Les resolvers d'activité productive et de transfert sont des services runtime, pas des données persistées par ce lot.

---

# 11. Validation

Repères historiques :

```text
178 / 178
→ base avant production

201 / 201
→ ENGINE-013 validée

224 / 224
→ ENGINE-014 validée

291 / 291
→ suite globale actuelle au point de consolidation
```

La suite actuelle confirme que les capacités ENGINE-013/014 restent compatibles avec les lots cognitifs ultérieurs.

---

# 12. Limites conservées

TECH-005 ne documente aucune implémentation de :

- monnaie ;
- prix ;
- achat/vente ;
- troc réciproque ;
- marché ;
- salaire ;
- employeur ;
- contrat de travail ;
- inventaire universel ;
- propriété générale ;
- entreprise ;
- formule offre/demande.

---

# 13. État final

```text
ENGINE-013        ✅ Validée / M4
ENGINE-014        ✅ Validée / M4
PAT-003/VERB-003  ✅ Officiels / M4
PAT-004/VERB-004  ✅ Officiels / M4
Implémentation    ✅
Persistance       ✅
Tests globaux     ✅ 291 / 291
TECH-005          ✅
```

Le bloc constitue le premier **substrat économique matériel autonome** de Chroniques, sans constituer encore une économie commerciale complète.

---

# Historique

## Version 1.0

- création au point de consolidation suivant ENGINE-017 ;
- documentation consolidée d'ENGINE-013 et ENGINE-014 ;
- production, provenance, circulation et conservation documentées ;
- validation globale courante enregistrée à 291 / 291 ;
- frontières commerciales maintenues.