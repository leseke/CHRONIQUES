# TECH-004 — Décision autonome par besoins

> Version : 1.0  
> Statut : Validé  
> Maturité : 4  
> Bibliothèque : TECH  
> Implémentation : `CHRONIQUES-ENGINE`  
> Spécifications : `ENGINE-011`, `ENGINE-012`

---

# 1. Objectif

Documenter l'implémentation réelle et validée du premier bloc de décision autonome par besoins dans `CHRONIQUES-ENGINE`.

TECH-004 consolide deux incréments devenus une seule capacité technique cohérente :

```text
Fatigue
→ se_reposer

Faim + nourriture accessible
→ manger
```

Il décrit uniquement le moteur obtenu après validation **178 / 178 tests réussis**.

Il ne définit aucune nouvelle règle métier.

---

# 2. Autorités

Les spécifications ENGINE sont :

```text
ENGINE-011 — Décision autonome par besoins
ENGINE-012 — Alimentation autonome minimale
```

Les autorités amont principales sont :

```text
MASTER-005 Phase 3
GDB-004B v1.2
GDB-005E v1.1
ACT-002-I
ACT-005-A
PAT-001 / VERB-001
PAT-002 / VERB-002
ENGINE-006
ENGINE-010
```

TECH-004 documente leur traduction technique réellement obtenue.

---

# 3. État de validation

Validation confirmée le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 178 / 178 tests réussis
→ 0 échec
```

Repères de progression :

```text
146 / 146
→ orchestration autonome ENGINE-010

158 / 158
→ décision repos multi-Tick ENGINE-011

161 / 161
→ première chaîne ACT canonique PAT-001 / VERB-001

178 / 178
→ alimentation autonome + arbitrage multi-besoins ENGINE-012
```

---

# 4. Position dans le moteur

Le bloc validé s'insère dans l'orchestration de TECH-003 :

```text
Scheduler.Tick
↓
AutonomousActionSystem
↓
NeedsIntentSource
↓
Intent?
↓
IAutonomousIntentExecutor
↓
NeedsPlanner
↓
PlanStep + Cibles
↓
PipelineRunner
↓
NeedsExecutionEngine
↓
Outcome
↓
ActionEffectDispatcher
↓
World
```

`AutonomousActionSystem` reste indépendant des règles métier concrètes.

---

# 5. NeedsIntentSource

`NeedsIntentSource` constitue la première politique métier concrète de `IAutonomousIntentSource`.

Elle peut fonctionner en mode historique repos-only ou avec les deux besoins validés.

## Repos

```text
Fatigue < seuil configuré
↓
Intent "se_reposer"
```

Si `Fatigue >= seuil`, aucun candidat repos n'est produit.

## Nourriture

Le candidat nourriture exige :

```text
Faim < seuil configuré
+
IAccessibleFoodResolver retourne une nourriture accessible
↓
Intent "manger"
```

Une Faim basse sans nourriture accessible ne produit aucun faux Intent.

---

# 6. Arbitrage déterministe

Lorsque repos et nourriture sont simultanément actionnables :

```text
satisfaction la plus basse
→ besoin retenu
```

En cas d'égalité stricte :

```text
Faim
avant
Fatigue
```

Cet ordre est un tie-break technique stable.

Il n'introduit aucune hiérarchie narrative générale entre les besoins.

Aucun hasard non déterministe n'intervient dans l'arbitrage.

---

# 7. FoodProductComponent

Le moteur représente une nourriture consommable par :

```csharp
public sealed class FoodProductComponent : IComponent
{
    public double FaimRestauree { get; set; }
    public int PortionsDisponibles { get; set; }
}
```

Le Component reste data-only.

Il ne définit :

- ni inventaire ;
- ni propriété ;
- ni qualité nutritionnelle complexe ;
- ni expiration ;
- ni digestion.

`FaimRestauree` constitue une valeur de tuning du produit.

`PortionsDisponibles` représente la disponibilité consommable minimale du lot.

---

# 8. IAccessibleFoodResolver

L'accès à la nourriture est isolé derrière :

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

Cette interface évite de créer prématurément un système d'inventaire.

Elle permet à une future représentation de l'accès de s'appuyer sur :

- possession ;
- stockage ;
- accès partagé ;
- contexte spatial ;
- disponibilité explicite.

Pour mêmes entrées et même configuration, la résolution doit rester déterministe.

---

# 9. Cibles dans PlanStep

L'arrivée de `Manger` a révélé une dette réelle du pipeline historique : le Planner choisissait conceptuellement les Actions, mais `PlanStep` ne portait pas leurs Cibles.

Le type possède désormais :

```csharp
public IReadOnlyList<CibleRef> Cibles { get; init; }
```

avec une valeur vide par défaut pour préserver la compatibilité des constructions historiques.

Le chemin générique exécutable exige toutefois une Cible principale valide.

Cette évolution permet au Planner de matérialiser la Cible sans la placer dans l'Intent.

---

# 10. NeedsPlanner

`NeedsPlanner` reconnaît exactement les deux objectifs validés :

```text
se_reposer
manger
```

## Plan de repos

```text
VERB-001 / PAT-001
Cible principale = Acteur
```

## Plan alimentaire

Le Planner résout d'abord une nourriture accessible via `IAccessibleFoodResolver`.

Puis il construit :

```text
VERB-002 / PAT-002
Cible principale = produit alimentaire
Cible secondaire = Acteur
```

Si aucune nourriture accessible n'existe, le Planner ne matérialise aucune Cible fictive.

---

# 11. MangerDefinition

Le moteur contient une Action Definition correspondant à la chaîne canonique :

```text
Principe : Entretien
↓
Pattern : Alimentation
↓
Verbe : Manger
```

Elle expose notamment les faits observables :

```text
produit.alimentaire.consomme
besoin.faim.restauree
```

La valeur de restauration n'est pas fixée par ACT ; elle provient du produit ciblé.

---

# 12. NeedsExecutionEngine

`NeedsExecutionEngine` valide l'exécution des deux Verbes officiels du bloc.

Pour `Manger`, il refuse notamment l'exécution si :

- l'Acteur n'existe plus ;
- l'Acteur ne porte pas `NeedsComponent` ;
- la Cible principale n'existe plus ;
- la Cible n'est pas alimentaire ;
- aucune portion n'est disponible ;
- la nourriture n'est plus accessible.

Un Outcome en échec n'applique aucun Effect.

---

# 13. Application des Effects

Le `PipelineRunner` n'applique plus lui-même les règles métier de chaque Verbe.

Le bloc introduit :

```text
IActionEffectApplicator
ActionEffectDispatcher
RestActionEffectApplicator
FoodActionEffectApplicator
```

## Repos

`RestActionEffectApplicator` restaure la Fatigue puis publie le fait correspondant.

## Alimentation

`FoodActionEffectApplicator` :

```text
portion disponible - 1
+
Faim + FaimRestauree
bornée à 100
+
publication des deux Events
```

La consommation et la restauration n'interviennent qu'après Outcome réussi.

---

# 14. PipelineRunner générique du bloc

`PipelineRunner` possède désormais une entrée commune :

```csharp
ActionInstance Execute(Intent intent, World world);
```

Le runner :

1. demande un Plan au Planner ;
2. utilise les Cibles du `PlanStep` ;
3. construit l'`ActionInstance` ;
4. fait progresser son cycle de vie ;
5. demande l'Outcome à l'Execution Engine ;
6. délègue les Effects en cas de réussite ;
7. archive l'Action.

Il ne connaît :

- ni seuil de Faim ;
- ni seuil de Fatigue ;
- ni règle alimentaire ;
- ni algorithme d'accessibilité ;
- ni règle `1 Action = 1 Tick`.

L'ancienne API `ExecuterSeReposer` reste compatible avec les tests et usages historiques.

---

# 15. Persistance alimentaire

`FoodProductComponent` est intégré à la persistance explicite existante :

```text
WorldRepository.Save
↓
EntitySnapshot.FoodProduct
↓
JSON
↓
WorldRepository.Load
↓
FoodProductComponent restauré
```

Le champ est nullable afin de préserver les Entities historiques qui ne représentent pas un produit alimentaire.

Lorsqu'il est absent, il n'a pas besoin de modifier la forme logique d'une sauvegarde historique.

---

# 16. Boucle autonome obtenue

Le bloc complet permet désormais :

```text
NeedsDecaySystem
↓
besoin sous seuil
↓
NeedsIntentSource
↓
choix déterministe du besoin actionnable
↓
AutonomousActionSystem
↓
Intent
↓
NeedsPlanner
↓
Action réelle
↓
Effects
↓
besoin restauré / ressource consommée
```

La régulation de Fatigue a été validée sur plusieurs Ticks.

L'alimentation ajoute pour la première fois une décision autonome dépendant d'une ressource réelle du World.

---

# 17. Couverture QA consolidée

La suite **178 / 178** couvre notamment :

```text
seuil strict de Fatigue
seuil strict de Faim
absence de faux Intent
arbitrage Faim/Fatigue
tie-break déterministe
régulation multi-Tick du repos
traçabilité ACT repos
traçabilité ACT alimentation
Cibles portées par le Plan
nourriture absente
nourriture épuisée
nourriture inaccessible
consommation d'une portion
restauration de Faim bornée
publication des Events
persistance du produit alimentaire
compatibilité de VERB-001
exécution de VERB-002
intégration Scheduler → autonomie → pipeline → World
```

---

# 18. Limites conservées

Le bloc validé ne contient pas :

- inventaire général ;
- propriété ;
- achat ;
- commerce autonome ;
- cuisine ;
- production alimentaire ;
- déplacement vers une ressource ;
- travail autonome ;
- Santé/Moral dérivés de l'alimentation ;
- personnalité pondérée ;
- habitudes pondérées ;
- ambitions pondérées ;
- Mémoire du Monde ;
- IA générale de PNJ.

Ces absences restent volontaires.

---

# 19. Traçabilité

```text
MASTER-005 Phase 3
↓
GDB-004B v1.2
+
GDB-005E v1.1
↓
PAT-001 / VERB-001
PAT-002 / VERB-002
↓
ENGINE-011
ENGINE-012
↓
NeedsIntentSource.cs
FoodProductComponent.cs
IAccessibleFoodResolver.cs
NeedsPlanner.cs
NeedsExecutionEngine.cs
MangerDefinition.cs
ActionEffectDispatcher.cs
PipelineRunner.cs
WorldRepository.cs
↓
NeedsIntentSourceTests.cs
ActionTaxonomyTests.cs
ENGINE-012 QA tests
↓
178 / 178 tests
↓
TECH-004
```

---

# 20. État final du bloc

```text
GDB              ✅
ACT               ✅ PAT/VERB 001-002 concernés
ENGINE-011        ✅ Validée / M4
ENGINE-012        ✅ Validée / M4
Implémentation    ✅
Build             ✅
Tests             ✅ 178 / 178
TECH              ✅ TECH-004
```

Cette consolidation valide une **politique autonome minimale par besoins**.

Elle ne clôt pas la Phase 3 ni la version v0.4.

---

# 21. Historique

## Version 1.0

- création de TECH-004 au premier point de consolidation documentaire suivant ENGINE-011 et ENGINE-012 ;
- consolidation du repos et de l'alimentation comme bloc technique unique ;
- documentation de `NeedsIntentSource`, `FoodProductComponent`, `IAccessibleFoodResolver`, `NeedsPlanner`, `NeedsExecutionEngine`, des applicateurs d'Effects et du runner multi-Verbes ;
- validation moteur enregistrée à **178 / 178 tests réussis** ;
- maintien explicite des limites : pas d'inventaire général, pas de travail autonome, pas d'économie autonome complète, pas de psychologie pondérée.
