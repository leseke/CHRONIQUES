# ENGINE-012 — Alimentation autonome minimale

> Version : 1.1
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : GDB-004B v1.2, GDB-005E v1.1, ACT-002-I, ACT-005-A, PAT-002, VERB-002, ENGINE-006, ENGINE-010, ENGINE-011
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 178 / 178 tests réussis

---

# 1. Objectif

Définir l'implémentation minimale permettant à un habitant autonome de répondre à son besoin de nourriture par `VERB-002 — Manger`, sans inventer un système d'inventaire ni contourner le pipeline ACT.

Flux validé :

```text
NeedsComponent.Faim
+
produit alimentaire accessible
↓
Intent manger
↓
Planner
↓
PlanStep + Cible alimentaire
↓
Action Instance VERB-002
↓
Outcome
↓
consommation du produit
+
Faim restaurée
↓
World
```

---

# 2. Problèmes architecturaux réellement révélés

L'arrivée d'un deuxième Verbe réel révèle trois besoins qui n'étaient pas justifiés avec `Se reposer` seul :

1. représenter un produit alimentaire consommable ;
2. résoudre son accessibilité sans inventer immédiatement un inventaire ;
3. porter les Cibles sélectionnées par le Planner dans le Plan plutôt que de les fournir extérieurement au pipeline.

ENGINE-012 traite uniquement ces besoins.

---

# 3. FoodProductComponent

Le moteur ajoute un Component de donnée :

```csharp
public sealed class FoodProductComponent : IComponent
{
    public double FaimRestauree { get; set; }
    public int PortionsDisponibles { get; set; }
}
```

Contrat :

```text
FaimRestauree
→ valeur > 0

PortionsDisponibles
→ valeur >= 0
```

Le Component ne contient aucune logique.

Une portion disponible représente une unité minimale consommable pour ce lot.

ENGINE-012 ne définit ni masse, ni calories, ni qualité, ni expiration.

---

# 4. Accessibilité alimentaire

L'accessibilité reste une règle GDB [réf: GDB-005E].

Le moteur introduit une frontière injectable :

```csharp
public interface IAccessibleFoodResolver
{
    EntityId? FindAccessibleFood(
        Entity actor,
        World world,
        Tick currentTick);

    bool IsAccessible(
        Entity actor,
        EntityId foodId,
        World world,
        Tick currentTick);
}
```

Cette interface ne constitue pas un inventaire.

Une implémentation future pourra s'appuyer sur :

- possession ;
- stockage ;
- accès partagé ;
- contexte spatial ;
- offre explicite.

ENGINE-012 n'en choisit aucune.

Pour mêmes Actor, World, Tick et configuration, la résolution doit être déterministe.

---

# 5. Cible portée par le Plan

ACT-005-A établit que l'Intent ne porte pas de Cible concrète et que le Plan matérialise les Actions et leurs Cibles.

ENGINE-012 ajoute à `PlanStep` :

```csharp
public IReadOnlyList<CibleRef> Cibles { get; init; }
```

avec une valeur vide par défaut afin de préserver la compatibilité des constructions historiques.

Tout Plan destiné à être exécuté par le runner générique fournit exactement une Cible principale, conformément à `ActionInstance`.

---

# 6. Planification des besoins

`NeedsPlanner` prend en charge exactement les deux objectifs autonomes validés :

```text
se_reposer
manger
```

## se_reposer

Le Planner produit :

```text
VERB-001 / PAT-001
Cible principale = Acteur
```

## manger

Le Planner demande au `IAccessibleFoodResolver` une nourriture accessible.

S'il n'en existe aucune :

```text
Planification impossible
```

Il ne crée jamais une Cible fictive.

S'il existe une nourriture :

```text
VERB-002 / PAT-002
Cible principale = produit alimentaire
Cible secondaire = Acteur
```

La Cible alimentaire est choisie par le Planner et jamais encodée dans l'Intent.

---

# 7. Décision autonome multi-besoins

`NeedsIntentSource` est étendue sans casser le constructeur historique de repos.

La décision nourriture n'est active que si trois conditions sont réunies :

```text
seuil de Faim configuré
+
Faim < seuil
+
resolver retourne une nourriture accessible
```

Alors le candidat :

```text
Intent manger
```

peut être produit.

Le candidat repos reste défini par ENGINE-011.

Lorsque les deux sont simultanément actionnables :

```text
satisfaction la plus basse
→ candidat retenu
```

En cas d'égalité stricte, ENGINE-012 utilise l'ordre technique stable :

```text
Faim
avant
Fatigue
```

Cet ordre sert uniquement au déterminisme et ne constitue pas une priorité narrative universelle.

---

# 8. MangerDefinition

Le moteur ajoute une Action Definition conforme à PAT-002 / VERB-002 :

```text
Principe = Entretien
Pattern = Alimentation
Verbe = Manger
```

Structure minimale :

- Inputs : Acteur + produit alimentaire ;
- Preconditions conceptuelles : produit existant, alimentaire, disponible, accessible ;
- Effects : consommation d'une portion + restauration de Faim ;
- Events : faits observables de consommation et de restauration.

Identifiants d'Events validés :

```text
produit.alimentaire.consomme
besoin.faim.restauree
```

---

# 9. Validation d'exécution

L'Execution Engine utilisé par ce lot rejette `Manger` si :

- l'Acteur n'existe plus ;
- l'Acteur ne possède aucun `NeedsComponent` ;
- la Cible principale n'existe plus ;
- la Cible ne possède aucun `FoodProductComponent` ;
- `PortionsDisponibles <= 0` ;
- la Cible n'est plus accessible selon `IAccessibleFoodResolver`.

Aucun Effect n'est appliqué après un Outcome en échec.

---

# 10. Application des Effects

ENGINE-012 introduit la frontière :

```csharp
public interface IActionEffectApplicator
{
    bool CanApply(ActionInstance instance);
    void Apply(ActionInstance instance, World world);
}
```

Un dispatcher ordonné applique exactement un applicateur compatible.

Applicateurs validés :

```text
RestActionEffectApplicator
FoodActionEffectApplicator
```

`FoodActionEffectApplicator` :

1. récupère la Cible principale alimentaire ;
2. diminue `PortionsDisponibles` de `1` ;
3. augmente `NeedsComponent.Faim` de `FaimRestauree`, borné à `100` ;
4. publie `produit.alimentaire.consomme` ;
5. publie `besoin.faim.restauree`.

---

# 11. PipelineRunner

`PipelineRunner` reçoit le Plan, construit l'Action Instance depuis les `Cibles` du `PlanStep`, exécute l'Outcome puis délègue les Effects.

Entrée générique :

```csharp
public ActionInstance Execute(Intent intent, World world);
```

Le runner :

- ne connaît pas les seuils de besoins ;
- ne résout pas la nourriture ;
- ne contient pas les règles de consommation ;
- ne contient pas de `switch` métier sur les Verbes.

L'ancienne méthode `ExecuterSeReposer` reste conservée pour compatibilité et délègue au chemin commun lorsque le Plan le permet.

---

# 12. Persistance

`FoodProductComponent` survit à `WorldRepository.Save/Load`.

`EntitySnapshot` est étendu explicitement avec :

```csharp
FoodProductComponent? FoodProduct
```

Le champ nullable est omis lorsqu'il est absent afin de préserver la forme des sauvegardes historiques ne contenant aucun produit alimentaire.

Cette extension reste cohérente avec l'approche de persistance actuelle, volontairement explicite tant que peu de Components existent.

---

# 13. Non-objectifs

ENGINE-012 ne couvre pas :

- inventaire général ;
- propriété ;
- achat ;
- échange ;
- cuisine ;
- production alimentaire ;
- déplacement vers la nourriture ;
- réservation concurrente de produits ;
- partage d'un produit ;
- digestion ;
- qualité nutritionnelle complexe ;
- Santé/Moral dérivés de l'alimentation ;
- moteur générique de tous les Effects ACT.

Le dispatcher d'Effects est une extension minimale pour deux Verbes réels, pas un interprète universel de `ConsequenceTemplate`.

---

# 14. Invariants

- L'Intent `manger` ne contient aucune Cible.
- Le Planner sélectionne la nourriture.
- Une nourriture inexistante, épuisée ou inaccessible ne peut pas être consommée.
- Une réussite `Manger` consomme exactement une portion dans ce lot.
- Une réussite restaure Faim selon la valeur du produit.
- Aucun produit n'est créé gratuitement par la décision ou le Planner.
- Le runner n'encode aucune règle de besoin.
- Le runner n'encode aucune règle alimentaire.
- L'ordre de décision Faim/Fatigue est déterministe.
- `FoodProductComponent` est persisté.
- Aucun changement n'introduit la règle `1 Action = 1 Tick`.

---

# 15. Contrat QA validé

La validation couvre :

1. `FoodProductComponent` sauvegardé/rechargé ;
2. `PlanStep` portant Cible principale et Cible secondaire ;
3. `se_reposer` planifié avec l'Acteur comme Cible principale ;
4. `manger` planifié avec la nourriture comme Cible principale ;
5. aucun Intent `manger` sans nourriture accessible ;
6. Faim sous seuil + nourriture accessible → Intent `manger` ;
7. Fatigue et Faim actionnables → satisfaction la plus basse retenue ;
8. égalité Faim/Fatigue → résultat stable défini ;
9. nourriture absente → aucune mutation indue ;
10. nourriture épuisée → aucun succès ;
11. nourriture inaccessible → aucun succès ;
12. réussite → une portion consommée ;
13. réussite → Faim restaurée et bornée à `100` ;
14. Events de consommation et restauration publiés ;
15. pipeline générique exécutant encore `Se reposer` ;
16. pipeline générique exécutant `Manger` ;
17. mêmes entrées → même nourriture sélectionnée et même résultat.

---

# 16. Validation

Validation technique communiquée par le porteur du projet le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 178 / 178 tests réussis
→ 0 échec
```

Les critères de sortie sont satisfaits :

- l'implémentation existe ;
- la suite antérieure reste verte ;
- VERB-001 reste fonctionnel ;
- VERB-002 fonctionne de bout en bout ;
- l'alimentation consomme une ressource réelle ;
- aucun inventaire ou système de propriété implicite n'a été créé ;
- aucun produit alimentaire n'est matérialisé gratuitement.

ENGINE-012 passe donc à **Validée / Maturité 4**.

---

# 17. Traçabilité

```text
GDB-004B v1.2
+
GDB-005E v1.1
↓
PAT-002
↓
VERB-002
↓
ENGINE-012
↓
CHRONIQUES-ENGINE
↓
178 / 178 tests
```

La consolidation TECH/roadmap/README reste volontairement différée jusqu'à décision explicite de clôture du jalon fonctionnel.

---

# HISTORIQUE

## Version 1.1

- ENGINE-012 passe à **Validée / Maturité 4** ;
- validation locale : **178 / 178 tests réussis** ;
- `Faim → manger` validé de bout en bout ;
- arbitrage déterministe Faim/Fatigue confirmé ;
- Cibles dans le Plan et pipeline multi-Verbes validés ;
- consommation réelle et persistance alimentaire confirmées ;
- aucune consolidation transverse déclenchée automatiquement.

## Version 1.0

- création d'ENGINE-012 ;
- définition de `FoodProductComponent` ;
- frontière injectable `IAccessibleFoodResolver` ;
- ajout des Cibles au `PlanStep` ;
- extension minimale de `NeedsIntentSource` à Faim ;
- définition de `MangerDefinition` ;
- séparation du runner et de l'application métier des Effects ;
- persistance du produit alimentaire ;
- contrat QA de la première alimentation autonome.

---

Fin du document
