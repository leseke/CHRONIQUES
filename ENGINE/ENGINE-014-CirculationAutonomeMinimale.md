# ENGINE-014 — Circulation autonome minimale

> Version : 1.1
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : MASTER-005 Phase 3, GDB-004A v1.2, GDB-005E v1.3, GDB-005F v1.2, PAT-004 v1.1, VERB-004 v1.1, ENGINE-006, ENGINE-010, ENGINE-011, ENGINE-012, ENGINE-013

---

# 1. Objectif

Définir le premier socle de circulation économique autonome entre deux habitants : une denrée déjà produite peut être transférée volontairement d'un stock alimentaire source vers un stock alimentaire destination distinct et compatible du destinataire, puis être utilisée normalement par les Actions déjà existantes.

Flux cible :

```text
entretien exécutable ?
├── oui → entretien
└── non
    ↓
transfert volontaire exécutable ?
├── oui → donner_denree
└── non
    ↓
production exécutable ?
├── oui → produire_denree
└── non → null
```

ENGINE-014 ouvre la circulation entre habitants, pas encore le commerce monétaire.

---

# 2. Scénario de référence

Le scénario d'intégration attendu est :

```text
Habitant A = producteur/donneur
Habitant B = destinataire affamé

Tick N
A n'a aucune denrée à donner
↓
A produit une denrée

Tick N+1
A possède une opportunité volontaire de transfert
↓
A donne la denrée à B
↓
B, traité ensuite dans le même Tick, voit la denrée devenue accessible
↓
B mange
```

La chaîne démontrée devient :

```text
ressource
↓
production
↓
stock A
↓
transfert volontaire
↓
stock B
↓
consommation
↓
besoin de B restauré
```

Aucune entrée joueur n'est nécessaire.

---

# 3. Extension de FoodProductComponent

Le moteur ajoute à `FoodProductComponent` une identité de produit optionnelle :

```csharp
public string? ProductKindId { get; set; }
```

Cette donnée sert uniquement aux mécaniques qui doivent comparer ou fusionner plusieurs stocks.

Contraintes ENGINE-014 :

- `Manger` et `Produire une denrée` restent compatibles avec les anciens produits dont `ProductKindId` est null ;
- `Donner une denrée` exige en revanche un `ProductKindId` non vide sur les deux stocks ;
- les deux identifiants doivent être égaux avec comparaison ordinale ;
- le premier lot exige également la même valeur `FaimRestauree` afin qu'un regroupement de portions ne change pas silencieusement la propriété alimentaire du produit.

Le champ est persisté via `FoodProductComponent` dans `WorldRepository`.

Lorsqu'il est `null`, il est omis du JSON afin de préserver la forme historique des sauvegardes de produits antérieurs à ENGINE-014.

---

# 4. FoodTransferOpportunity

Le contexte de transfert est représenté par une donnée immuable :

```csharp
public sealed record FoodTransferOpportunity(
    EntityId RecipientId,
    EntityId SourceFoodProductId,
    EntityId DestinationFoodProductId,
    int Portions);
```

Contrat :

- `Portions > 0` ;
- le destinataire concret est validé comme distinct de l'Acteur ;
- source et destination doivent désigner deux stocks distincts ;
- source et destination sont résolues au moment de l'exécution.

L'opportunité ne constitue pas un prix, un contrat commercial ni un inventaire.

---

# 5. IVoluntaryFoodTransferResolver

Le moteur introduit :

```csharp
public interface IVoluntaryFoodTransferResolver
{
    FoodTransferOpportunity? FindExecutableTransfer(
        Entity actor,
        World world,
        Tick currentTick);
}
```

Le resolver représente la frontière contextuelle définie par GDB-005F.

Il doit retourner `null` lorsqu'aucun transfert volontaire n'est actuellement exécutable.

À Acteur, World, Tick et configuration identiques, il retourne la même opportunité.

Il peut ultérieurement être alimenté par relations, contrats, marchés, organisations ou demandes sans modifier ENGINE-014.

---

# 6. VoluntaryFoodTransferIntentSource

Une nouvelle source d'Intent :

```csharp
public sealed class VoluntaryFoodTransferIntentSource : IAutonomousIntentSource
```

retourne :

```text
opportunité exécutable
→ Intent(actor.Id, "donner_denree", Priorite: 1)

aucune opportunité
→ null
```

Elle ne modifie jamais le World.

---

# 7. Composition des sources autonomes

`CompositeAutonomousIntentSource` reste inchangé.

Le premier ordre économique devient :

```text
1. NeedsIntentSource
2. VoluntaryFoodTransferIntentSource
3. ProductiveActivityIntentSource
```

La première source non-null gagne conformément à son contrat existant.

ENGINE-014 ne crée aucun score universel entre entretien, échange et production.

---

# 8. DonnerDenreeDefinition

La nouvelle Action Definition est :

```text
Principe = Échange
Pattern = Transfert
Verbe = DonnerDenree
```

Objectif d'Intent :

```text
donner_denree
```

Cibles :

```text
principale = stock FoodProduct destination
secondaire = stock FoodProduct source
secondaire = destinataire
```

Event minimal :

```text
produit.alimentaire.transfere
```

---

# 9. FoodTransferPlanner

Le Planner :

1. vérifie l'existence de l'Acteur ;
2. demande une opportunité au resolver ;
3. refuse de planifier si aucune opportunité n'est exécutable ;
4. crée un Plan simple portant destination, source et destinataire ;
5. ne place jamais la quantité ou les Cibles dans l'Intent.

Le transfert est routé via `CompositePlanner` existant :

```text
donner_denree → FoodTransferPlanner
```

Aucun changement structurel du compositeur n'est nécessaire.

---

# 10. FoodTransferExecutionEngine

L'Execution Engine rejette l'Action si :

- l'Acteur n'existe plus ;
- aucune opportunité exécutable n'est encore résolue ;
- le destinataire n'existe plus ;
- le destinataire est identique à l'Acteur ;
- la source et la destination désignent le même stock ;
- les Cibles du Plan ne correspondent plus à l'opportunité ;
- source ou destination n'existe plus ;
- source ou destination ne possède pas `FoodProductComponent` ;
- `Portions <= 0` ;
- la source possède moins de portions que demandé ;
- l'un des `ProductKindId` est null/vide ;
- les `ProductKindId` diffèrent ;
- les `FaimRestauree` diffèrent dans ce premier lot.

Il ne modifie jamais le World.

Il est routé via `CompositeExecutionEngine` existant :

```text
DonnerDenree → FoodTransferExecutionEngine
```

---

# 11. FoodTransferActionEffectApplicator

Après Outcome réussi :

1. retrouve l'opportunité encore applicable ;
2. revalide les Cibles de l'Action contre l'opportunité ;
3. soustrait exactement `Portions` à la source ;
4. ajoute exactement `Portions` à la destination avec contrôle d'overflow ;
5. publie `produit.alimentaire.transfere`.

Invariant de conservation :

```text
source avant + destination avant
=
source après + destination après
```

Aucun besoin du destinataire n'est modifié par le transfert lui-même.

La consommation éventuelle reste une Action `Manger` distincte.

---

# 12. PipelineRunner

`PipelineRunner` reste inchangé.

ENGINE-014 doit démontrer que le quatrième Verbe réel s'intègre sans :

- nouveau `switch` métier dans le runner ;
- duplication du cycle de vie d'Action ;
- mutation directe depuis la source d'Intent ;
- second pipeline parallèle.

---

# 13. Persistance

Aucune nouvelle structure persistante n'est requise au-delà de `ProductKindId`, déjà sérialisé dans `FoodProductComponent`.

Après sauvegarde/rechargement :

- l'identité du produit doit être conservée lorsqu'elle existe ;
- les portions des stocks source/destination doivent être conservées ;
- un ancien produit sans identité conserve une représentation JSON compatible grâce à l'omission de `ProductKindId` lorsqu'il est `null`.

Une opportunité contextuelle n'est pas nécessairement persistée par ENGINE-014 : sa source de vérité appartient au resolver compétent.

---

# 14. Non-objectifs

ENGINE-014 ne couvre pas :

- monnaie ;
- prix ;
- achat ;
- vente ;
- troc réciproque ;
- négociation ;
- salaire ;
- taxe ;
- marché ;
- commerce ;
- entreprise ;
- inventaire universel ;
- propriété générale ;
- effet relationnel automatique ;
- motivation psychologique du don.

---

# 15. Invariants

- L'entretien actionnable précède le transfert volontaire.
- Le transfert volontaire précède la production dans le premier ordre minimal.
- Une opportunité absente ne produit aucun faux Intent.
- L'Intent ne contient ni destinataire, ni Cibles, ni quantité.
- Le Planner matérialise les Cibles depuis l'opportunité.
- Donneur et destinataire sont distincts.
- Stock source et stock destination sont distincts.
- Source et destination portent la même identité de produit non vide.
- Une réussite conserve exactement le nombre total de portions.
- Aucun stock ne devient négatif.
- Le transfert ne restaure aucun besoin directement.
- Le runner reste agnostique des Verbes.
- Aucun prix ou paiement implicite n'est créé.

---

# 16. Contrat QA

La couverture ajoutée par ENGINE-014 comprend :

```text
Engine014FoodTransferTests.cs
→ 22 tests comportementaux

Engine014ActClassificationTests.cs
→ 1 test de classification ACT
```

Soit **23 nouveaux tests**.

Ils vérifient notamment :

1. validation de `FoodTransferOpportunity` ;
2. persistance de `ProductKindId` ;
3. source de transfert sans opportunité → null ;
4. source avec opportunité → `donner_denree` ;
5. composition : entretien avant transfert ;
6. composition : transfert avant production ;
7. Planner sélectionne destination/source/destinataire ;
8. Planner refuse l'absence d'opportunité ;
9. Execution Engine refuse un destinataire absent ;
10. refuse un destinataire identique au donneur ;
11. refuse `source == destination` ;
12. refuse une source insuffisante ;
13. refuse une identité de produit absente ou différente ;
14. refuse une représentation alimentaire incompatible ;
15. réussite sans mutation dans l'Execution Engine ;
16. applicateur transfère exactement la quantité ;
17. conservation stricte de la somme des portions ;
18. Event publié ;
19. pipeline composite continue d'exécuter les trois Verbes précédents ;
20. pipeline composite exécute DonnerDenree ;
21. scénario multi-habitants production → transfert → consommation sans joueur ;
22. déterminisme à état/opportunité identiques ;
23. classification `Échange → Transfert → DonnerDenree`.

---

# 17. Critères de validation

ENGINE-014 pourra passer en Validée / Maturité 4 lorsque :

- le build réussit ;
- les tests historiques restent verts ;
- les 23 nouveaux tests ENGINE-014 sont verts ;
- PAT-004 / VERB-004 sont correctement tracés ;
- une suite globale de **224 / 224** est confirmée localement à partir de la base 201 / 201 ;
- la conservation du transfert est démontrée ;
- le scénario producteur → destinataire → consommation fonctionne sans joueur ;
- aucun mécanisme de prix ou paiement non spécifié n'est introduit.

---

# 18. Traçabilité

```text
MASTER-005 Phase 3
↓
GDB-004A / GDB-005E / GDB-005F
↓
PAT-004
↓
VERB-004
↓
ENGINE-014
↓
CHRONIQUES-ENGINE
↓
Tests
```

---

# HISTORIQUE

## Version 1.1

- alignement sur GDB-005E v1.3, GDB-005F v1.2, PAT-004 v1.1 et VERB-004 v1.1 ;
- explicitation de l'invariant `stock source ≠ stock destination` ;
- persistance JSON rétrocompatible de `ProductKindId` documentée ;
- revalidation des Cibles dans l'applicateur explicitée ;
- couverture QA portée à **23 nouveaux tests** ;
- total attendu fixé à **224 tests** avant validation locale.

## Version 1.0

- création d'ENGINE-014 ;
- identité de produit transférable ;
- opportunité volontaire injectable ;
- quatrième source d'Intent concrète ;
- ordre `entretien → transfert → production` ;
- transfert conservatif entre deux stocks alimentaires ;
- scénario multi-habitants production → circulation → consommation.

---

Fin du document
