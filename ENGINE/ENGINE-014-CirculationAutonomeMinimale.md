# ENGINE-014 — Circulation autonome minimale

> Version : 1.2
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : MASTER-005 Phase 3, GDB-004A v1.2, GDB-005E v1.3, GDB-005F v1.2, PAT-004 v1.2, VERB-004 v1.2, ENGINE-006, ENGINE-010, ENGINE-011, ENGINE-012, ENGINE-013
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 224 / 224 tests réussis

---

# 1. Objectif

Définir le premier socle de circulation économique autonome entre deux habitants : une denrée déjà produite peut être transférée volontairement d'un stock alimentaire source vers un stock alimentaire destination distinct et compatible du destinataire, puis être utilisée normalement par les Actions déjà existantes.

Flux validé :

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

# 2. Scénario de référence validé

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

La chaîne démontrée est :

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
- `Donner une denrée` exige un `ProductKindId` non vide sur les deux stocks ;
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

Il retourne `null` lorsqu'aucun transfert volontaire n'est actuellement exécutable.

À Acteur, World, Tick et configuration identiques, il retourne la même opportunité.

Il peut ultérieurement être alimenté par relations, contrats, marchés, organisations ou demandes sans modifier ENGINE-014.

---

# 6. VoluntaryFoodTransferIntentSource

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

Ordre validé :

```text
1. NeedsIntentSource
2. VoluntaryFoodTransferIntentSource
3. ProductiveActivityIntentSource
```

La première source non-null gagne conformément au contrat existant.

ENGINE-014 ne crée aucun score universel entre entretien, échange et production.

---

# 8. DonnerDenreeDefinition

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

Event :

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

Routage :

```text
donner_denree → FoodTransferPlanner
```

Aucun changement structurel de `CompositePlanner` n'est nécessaire.

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

Routage :

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

Le quatrième Verbe réel s'intègre sans :

- nouveau `switch` métier dans le runner ;
- duplication du cycle de vie d'Action ;
- mutation directe depuis la source d'Intent ;
- second pipeline parallèle.

---

# 13. Persistance

Aucune nouvelle structure persistante n'est requise au-delà de `ProductKindId`, sérialisé dans `FoodProductComponent`.

Après sauvegarde/rechargement :

- l'identité du produit est conservée lorsqu'elle existe ;
- les portions des stocks source/destination sont conservées ;
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

# 16. Validation technique

La couverture ajoutée par ENGINE-014 comprend :

```text
Engine014FoodTransferTests.cs
→ 22 tests comportementaux

Engine014ActClassificationTests.cs
→ 1 test de classification ACT
```

Soit **23 nouveaux tests**.

La validation locale confirme notamment :

1. validation de `FoodTransferOpportunity` ;
2. persistance rétrocompatible de `ProductKindId` ;
3. absence d'Intent sans opportunité ;
4. ordre entretien → transfert → production ;
5. sélection des Cibles par le Planner ;
6. refus du destinataire invalide ;
7. refus de `source == destination` ;
8. refus des stocks incompatibles ou insuffisants ;
9. absence de mutation dans l'Execution Engine ;
10. conservation stricte dans l'applicateur ;
11. continuité des trois Verbes précédents ;
12. exécution de `DonnerDenree` par le pipeline composite ;
13. scénario multi-habitants production → transfert → consommation ;
14. déterminisme ;
15. classification `Échange → Transfert → DonnerDenree`.

```text
dotnet build
→ succès

dotnet test
→ 224 / 224 tests réussis
→ 0 échec
```

ENGINE-014 satisfait donc ses critères et passe à **Validée / Maturité 4**.

---

# 17. Frontière économique maintenue

L'audit ciblé reste applicable :

```text
transfert volontaire de denrée
→ autorisé et validé

prix / monnaie / vente / troc réciproque / marché
→ toujours bloqués
```

ENGINE-014 n'introduit aucun solde monétaire, coefficient de prix, négociation ou contrepartie automatique.

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

## Version 1.2

- ENGINE-014 passe à **Validée / Maturité 4** ;
- validation locale enregistrée à **224 / 224 tests réussis** ;
- PAT-004 / VERB-004 confirmés Officiels / M4 ;
- scénario autonome multi-habitants production → transfert → consommation confirmé ;
- conservation, déterminisme et compatibilité JSON validés ;
- frontière avec prix, monnaie et marché maintenue.

## Version 1.1

- alignement sur GDB-005E v1.3, GDB-005F v1.2, PAT-004 v1.1 et VERB-004 v1.1 ;
- explicitation de l'invariant `stock source ≠ stock destination` ;
- persistance JSON rétrocompatible de `ProductKindId` documentée ;
- revalidation des Cibles dans l'applicateur explicitée ;
- couverture QA portée à 23 nouveaux tests ;
- total attendu fixé à 224 avant validation locale.

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
