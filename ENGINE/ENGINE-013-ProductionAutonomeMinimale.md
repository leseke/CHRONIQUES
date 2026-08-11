# ENGINE-013 — Production autonome minimale

> Version : 1.1
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : MASTER-005 Phase 3, GDB-004A v1.1, GDB-005C v1.2, GDB-012B v1.1, GDB-012E v1.1, PAT-003, VERB-003, ENGINE-006, ENGINE-010, ENGINE-011, ENGINE-012
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 201 / 201 tests réussis

---

# 1. Objectif

Définir le premier socle productif autonome du World : un habitant peut exécuter `VERB-003 — Produire une denrée` lorsqu'aucun Intent d'entretien prioritaire n'est exécutable et qu'une opération productive réelle est disponible.

Flux validé :

```text
entretien exécutable ?
├── oui → Intent entretien
└── non
    ↓
opération productive exécutable ?
├── non → null
└── oui
    ↓
Intent produire_denree
↓
Planner
↓
entrée réelle + sortie alimentaire
↓
Action
↓
Outcome
↓
entrée consommée
+
sortie produite
+
provenance persistée
```

ENGINE-013 ouvre la production réelle, pas encore le marché.

---

# 2. Périmètre

Le lot ajoute uniquement ce qui devient nécessaire pour prouver une première transformation économique autonome :

- stock matériel minimal ;
- opération productive configurable ;
- résolution contextuelle d'une activité productive ;
- arbitrage ordonné entretien → production ;
- planification de VERB-003 ;
- validation d'exécution ;
- application des Effects ;
- provenance ;
- persistance ;
- intégration Scheduler → autonomie → production.

---

# 3. ResourceStockComponent

Le moteur ajoute un Component de donnée :

```csharp
public sealed class ResourceStockComponent : IComponent
{
    public double Quantity { get; set; }
}
```

Contrat :

```text
Quantity >= 0
```

Le Component ne contient aucune logique.

Il ne définit ni unité universelle, ni prix, ni propriétaire.

---

# 4. ProductionOperation

Une opération productive minimale est représentée par une donnée immuable :

```csharp
public sealed record ProductionOperation(
    string OperationId,
    EntityId InputResourceId,
    double InputQuantity,
    EntityId OutputFoodProductId,
    int OutputPortions);
```

Contrat :

- `OperationId` non vide ;
- `InputQuantity > 0` ;
- `OutputPortions > 0`.

Le lot couvre volontairement une seule entrée matérielle et une seule sortie alimentaire, conformément à VERB-003.

---

# 5. IProductiveActivityResolver

L'activité productive disponible reste une donnée/contextualisation externe au moteur métier.

```csharp
public interface IProductiveActivityResolver
{
    ProductionOperation? FindExecutableOperation(
        Entity actor,
        World world,
        Tick currentTick);
}
```

Le resolver doit retourner `null` si l'opération n'est pas actuellement exécutable.

À Acteur, World, Tick et configuration identiques, il doit retourner la même opération.

Il peut ultérieurement s'appuyer sur métier, organisation, lieu, projet ou inventaire sans modifier ENGINE-013.

---

# 6. Décision autonome

Une nouvelle source :

```csharp
public sealed class ProductiveActivityIntentSource : IAutonomousIntentSource
```

retourne :

```text
opération exécutable
→ Intent(actor.Id, "produire_denree", Priorite: 1)

aucune opération
→ null
```

Elle ne modifie jamais le World.

---

# 7. Composition ordonnée des sources d'Intent

ENGINE-013 introduit :

```csharp
public sealed class CompositeAutonomousIntentSource : IAutonomousIntentSource
```

Elle reçoit une liste ordonnée de sources et retourne le premier Intent non-null.

Pour le premier monde productif :

```text
1. NeedsIntentSource
2. ProductiveActivityIntentSource
```

Ainsi, GDB-004A est respecté sans ajouter de score artificiel entre besoins physiologiques et travail.

La composition ne consulte jamais une source suivante après qu'une source précédente a produit un Intent.

---

# 8. ProduireDenreeDefinition

La nouvelle Action Definition est :

```text
Principe = Transformation
Pattern = Production
Verbe = ProduireDenree
```

Objectif d'Intent :

```text
produire_denree
```

Cibles :

```text
principale = sortie FoodProduct
secondaire = entrée ResourceStock
```

Events minimaux :

```text
production.entree.consommee
production.denree.creee
```

---

# 9. ProductionPlanner

Le Planner :

1. vérifie l'existence de l'Acteur ;
2. demande une opération au resolver ;
3. refuse de planifier si aucune opération n'est exécutable ;
4. crée un Plan simple portant les Cibles de l'opération ;
5. ne place jamais l'opération ou les Cibles dans l'Intent.

---

# 10. Composition de Planners

Pour éviter de remplacer `NeedsPlanner`, ENGINE-013 introduit une composition minimale :

```csharp
CompositePlanner
```

Elle associe explicitement des objectifs d'Intent à des `IPlanner`.

Exemple :

```text
se_reposer      → NeedsPlanner
manger          → NeedsPlanner
produire_denree → ProductionPlanner
```

Aucun objectif absent de la table n'est inventé.

---

# 11. ProductionExecutionEngine

L'Execution Engine de production rejette l'Action si :

- l'Acteur n'existe plus ;
- aucune opération productive exécutable n'est encore résolue ;
- les Cibles du Plan ne correspondent plus à cette opération ;
- l'entrée n'existe plus ;
- l'entrée ne possède pas `ResourceStockComponent` ;
- sa quantité est insuffisante ;
- la sortie n'existe plus ;
- la sortie ne possède pas `FoodProductComponent`.

Il ne modifie jamais le World.

---

# 12. Composition d'Execution Engines

ENGINE-013 introduit :

```csharp
CompositeExecutionEngine
```

Il route une `ActionInstance` vers un `IExecutionEngine` selon son Verbe déclaré.

Pour ce lot :

```text
SeReposer      → NeedsExecutionEngine
Manger         → NeedsExecutionEngine
ProduireDenree → ProductionExecutionEngine
```

Une définition non enregistrée produit un Outcome d'échec ; aucun moteur n'est choisi implicitement.

---

# 13. Provenance

Le moteur ajoute une donnée persistante :

```csharp
public sealed record ProductionTrace(
    string OperationId,
    EntityId InputResourceId,
    Tick ProducedAt);

public sealed class ProductionProvenanceComponent : IComponent
{
    public List<ProductionTrace> Traces { get; set; }
}
```

Chaque réussite ajoute exactement une trace à la sortie alimentaire.

La provenance ne remplace pas `World.Events` : elle constitue l'état durable de causalité associé au produit.

---

# 14. ProductionActionEffectApplicator

Après Outcome réussi :

1. retrouve l'opération encore applicable ;
2. soustrait exactement `InputQuantity` au stock d'entrée ;
3. ajoute exactement `OutputPortions` au produit alimentaire ;
4. ajoute une `ProductionTrace` ;
5. publie `production.entree.consommee` ;
6. publie `production.denree.creee`.

Aucune quantité ne peut devenir négative.

---

# 15. PipelineRunner

`PipelineRunner` reste inchangé dans sa responsabilité :

- reçoit un `IPlanner` ;
- reçoit un `IExecutionEngine` ;
- reçoit des `IActionEffectApplicator` ;
- ne connaît aucune règle productive particulière.

La troisième Action réelle est intégrée par composition/injection, pas par un nouveau `switch` dans le runner.

---

# 16. Persistance

`ResourceStockComponent` et `ProductionProvenanceComponent` survivent à `WorldRepository.Save/Load`.

`FoodProductComponent` reste la sortie alimentaire déjà persistée depuis ENGINE-012.

---

# 17. Intégration multi-Tick validée

Le scénario de référence démontre :

```text
Acteur affamé
+
aucune nourriture disponible
+
opération productive disponible
↓
Tick N
NeedsIntentSource → null pour manger
ProductiveActivityIntentSource → produire_denree
↓
production crée des portions
↓
Tick N+1
NeedsIntentSource → manger
↓
portion consommée
+
Faim restaurée
```

Ce scénario relie autonomie, production et consommation sans intervention du joueur.

---

# 18. Non-objectifs

ENGINE-013 ne couvre pas :

- choix de métier ;
- carrière ;
- employeur ;
- contrat de travail ;
- horaires ;
- salaire ;
- monnaie ;
- prix ;
- marché ;
- vente ;
- offre et demande ;
- entreprise ;
- transport ;
- inventaire général ;
- concurrence entre producteurs ;
- rendement par compétence ;
- outils ;
- création déterministe de nouvelles Entity de produit.

---

# 19. Invariants

- L'entretien actionnable précède la production dans le premier arbitrage autonome.
- Une activité productive absente ne produit aucun faux Intent.
- L'Intent productif ne contient ni opération ni Cibles.
- Le Planner sélectionne l'opération et matérialise les Cibles.
- Une réussite consomme exactement l'entrée configurée.
- Une réussite produit exactement les portions configurées.
- Aucun stock ne devient négatif.
- Chaque production réussie ajoute une provenance persistante.
- Le runner reste agnostique des Verbes.
- Aucun prix, salaire ou métier implicite n'est créé.
- Aucune règle `1 Action = 1 Tick` n'est introduite.

---

# 20. Contrat QA

Le fichier `Engine013ProductionTests.cs` contient **23 tests `[Fact]`** couvrant notamment :

1. validation des données `ProductionOperation` ;
2. persistance de `ResourceStockComponent` ;
3. persistance de `ProductionProvenanceComponent` ;
4. source productive sans opération → null ;
5. source productive avec opération → `produire_denree` ;
6. composition des sources : besoin prioritaire avant production ;
7. composition des sources : production quand besoins ne produisent rien ;
8. Planner sélectionne les Cibles depuis l'opération ;
9. Planner refuse l'absence d'opération ;
10. Execution Engine refuse une entrée absente ;
11. refuse un stock insuffisant ;
12. refuse une sortie alimentaire invalide ;
13. réussite sans mutation dans l'Execution Engine ;
14. applicateur consomme exactement l'entrée ;
15. applicateur ajoute exactement les portions ;
16. provenance ajoutée ;
17. Events publiés ;
18. pipeline composite continue d'exécuter Repos et Manger ;
19. pipeline composite exécute ProduireDenree ;
20. scénario multi-Tick production → manger sans entrée joueur ;
21. mêmes entrées/configuration → même séquence ;
22. persistance et composition sont vérifiées par des cas distincts supplémentaires ;
23. la suite historique complète reste verte.

Base avant ce lot : `178 / 178`.

Validation locale finale :

```text
dotnet build
→ succès

dotnet test
→ 201 / 201 tests réussis
→ 0 échec
```

---

# 21. Critères de validation

Les critères sont satisfaits :

- le build réussit ;
- les tests historiques restent verts ;
- les tests ENGINE-013 sont verts ;
- PAT-003 / VERB-003 sont correctement tracés ;
- une production autonome réelle modifie les stocks ;
- sa provenance survit au reload ;
- le scénario production → consommation fonctionne sans joueur ;
- aucun mécanisme commercial non spécifié n'est introduit.

ENGINE-013 est donc **Validée / Maturité 4**.

---

# 22. Traçabilité

```text
MASTER-005 Phase 3
↓
GDB-004A / GDB-005C / GDB-012B / GDB-012E
↓
PAT-003
↓
VERB-003
↓
ENGINE-013
↓
CHRONIQUES-ENGINE
↓
Tests
↓
201 / 201
```

---

# HISTORIQUE

## Version 1.1

- ENGINE-013 passe à **Validée / Maturité 4** ;
- validation locale enregistrée à **201 / 201 tests réussis** ;
- correction du comptage : le fichier ENGINE-013 contient 23 nouveaux tests, et non 22 ;
- scénario autonome production au Tick N → consommation au Tick N+1 confirmé ;
- persistance des stocks et de la provenance confirmée ;
- compatibilité des Verbes Repos et Manger maintenue ;
- économie commerciale laissée hors périmètre.

## Version 1.0

- création d'ENGINE-013 ;
- spécification du stock matériel minimal ;
- opération productive injectable ;
- composition ordonnée des sources d'Intent ;
- composition des Planners et Execution Engines ;
- production d'une denrée à partir d'une entrée réelle ;
- provenance persistante ;
- scénario autonome production → consommation.

---

Fin du document
