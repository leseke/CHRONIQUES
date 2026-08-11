# ENGINE-011 — Décision autonome par besoins

> Version : 1.2
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : MASTER-005, GDB-004B v1.1, ACT-002-H, ENGINE-006, ENGINE-010
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 158 / 158 tests réussis

---

# 1. Objectif

Définir la première implémentation concrète de `IAutonomousIntentSource` pour v0.4 — Le monde vivant.

ENGINE-011 traduit le premier contrat autonome rendu implémentable par GDB-004B v1.1 :

```text
Habitant autonome
+
NeedsComponent
+
seuil de fatigue configuré
↓
Intent? se_reposer
```

Ce lot fournit une décision métier réelle, mais volontairement minimale.

Il ne constitue pas une IA générale ni un arbitre complet de tous les besoins.

---

# 2. Autorité GDB

GDB-004B v1.1 établit notamment :

- une satisfaction des besoins bornée entre `0` et `100` ;
- un seuil d'activation strict ;
- l'interdiction de créer un faux Intent lorsqu'aucune réponse exécutable n'existe ;
- une urgence de base monotone ;
- des égalités déterministes ;
- le premier mapping autonome implémentable `Fatigue → se_reposer`.

ENGINE-011 n'ajoute aucune règle au-delà de ce périmètre.

---

# 3. Position architecturale

ENGINE-010 a créé la frontière :

```text
AutonomousActionSystem
↓
IAutonomousIntentSource
↓
Intent?
```

ENGINE-011 fournit la première source concrète :

```text
NeedsIntentSource
:
IAutonomousIntentSource
```

Le flux de référence devient :

```text
Scheduler.Tick
↓
AutonomousActionSystem
↓
NeedsIntentSource
↓
Intent? se_reposer
↓
IAutonomousIntentExecutor
↓
ENGINE-006
↓
World
```

---

# 4. Responsabilité

`NeedsIntentSource` décide uniquement si l'état courant de Fatigue justifie la production du nouvel objectif :

```text
se_reposer
```

Elle ne :

- modifie jamais `NeedsComponent` ;
- n'exécute aucune Action ;
- ne publie aucun Event ;
- ne fait jamais avancer le Tick ;
- ne lit pas `World.Events` ;
- ne sélectionne pas de Plan ;
- ne connaît pas `SeReposerDefinition` ;
- ne connaît pas `PipelineRunner` ;
- ne traite pas la mort, déjà filtrée par ENGINE-010.

---

# 5. Contrat minimal

Structure validée :

```csharp
public sealed class NeedsIntentSource : IAutonomousIntentSource
{
    public double FatigueActivationThreshold { get; }

    public NeedsIntentSource(double fatigueActivationThreshold);

    public Intent? CreateIntent(
        Entity actor,
        World world,
        Tick currentTick);
}
```

---

# 6. Validation du seuil

Le seuil de Fatigue est une valeur de satisfaction compatible avec GDB-004B :

```text
0 <= seuil <= 100
```

Une valeur hors de cet intervalle constitue une erreur de configuration et est rejetée à la construction.

Le seuil n'est pas une constante GDB.

L'assemblage ou les tests le fournissent explicitement.

---

# 7. Entity sans NeedsComponent

Si l'Acteur ne possède aucun `NeedsComponent` :

```text
CreateIntent
→ null
```

La source ne crée aucun Component et ne déduit aucun besoin implicite.

---

# 8. Règle de Fatigue

Le champ actuel :

```text
NeedsComponent.Fatigue
```

représente la satisfaction du besoin de repos :

```text
0
→ critique

100
→ pleinement satisfait
```

Règle :

```text
Fatigue < FatigueActivationThreshold
→ Intent se_reposer
```

Sinon :

```text
Fatigue >= FatigueActivationThreshold
→ null
```

Le cas d'égalité est donc explicitement non activé.

---

# 9. Intent produit

Lorsqu'il est produit :

```csharp
new Intent(
    actor.Id,
    "se_reposer",
    Priorite: 1)
```

L'objectif est identique à celui déjà accepté par le Planner réel d'ENGINE-006.

`Priorite = 1` ne constitue pas une hiérarchie générale des besoins.

Dans ce premier lot, la source ne produit jamais plusieurs candidats : aucune comparaison de priorités concurrentes n'est donc réalisée.

Une future politique multi-besoins devra définir séparément la relation entre urgence GDB et `Intent.Priorite` avant implémentation.

---

# 10. Autres besoins

`NeedsComponent` contient actuellement notamment :

- Faim ;
- Fatigue ;
- Sante ;
- Moral.

ENGINE-011 ne produit aucun Intent pour :

- Faim ;
- Sante ;
- Moral.

Cette absence est volontaire : le moteur ne possède pas encore de réponse exécutable documentée pour ces besoins.

Ils restent des états réels du World et continuent d'évoluer normalement.

Ils ne sont jamais considérés comme satisfaits du seul fait qu'ENGINE-011 ne sait pas encore les traiter.

---

# 11. Déterminisme

À :

```text
Entity identique
+
NeedsComponent identique
+
seuil identique
+
Tick identique
+
World pertinent identique
```

la source retourne le même `Intent` ou `null` de manière reproductible.

Aucun RNG n'est nécessaire pour ENGINE-011.

---

# 12. Absence de mutation

`CreateIntent` est une opération de décision pure vis-à-vis de l'état métier observé.

Après son invocation :

```text
NeedsComponent avant
=
NeedsComponent après
```

La satisfaction de Fatigue n'est modifiée qu'après passage éventuel de l'Intent dans le pipeline d'Actions et application des Effects correspondants.

---

# 13. Intégration avec ENGINE-010

`NeedsIntentSource` est injectée directement dans :

```text
AutonomousActionSystem
```

sans modification de celui-ci.

ENGINE-011 confirme ainsi que la frontière créée par ENGINE-010 permet réellement l'ajout progressif de politiques métier distinctes.

---

# 14. Intégration avec ENGINE-006

Le test d'intégration de référence démontre :

```text
Fatigue sous seuil
↓
NeedsIntentSource
↓
Intent se_reposer
↓
AutonomousActionSystem
↓
PipelineRunner
↓
Action Archived
↓
Outcome réussi
↓
Fatigue restaurée
↓
GameEvent observable
```

ENGINE-011 ne généralise pas `PipelineRunner`.

---

# 15. Validation multi-Tick

La couverture QA valide également l'intégration temporelle réelle avec `NeedsDecaySystem` lorsque celui-ci est enregistré avant `AutonomousActionSystem`.

Scénario de seuil :

```text
Fatigue initiale = 62
Déclin = 1 / Tick
Seuil = 60

Tick 1 → 61 → aucune Action
Tick 2 → 60 → aucune Action
Tick 3 → 59 → Intent se_reposer → Fatigue 79
```

Ce scénario confirme que l'égalité au seuil ne déclenche pas d'Intent et que le franchissement strict intervient après l'évolution du besoin lorsque l'ordre des Systems est :

```text
NeedsDecaySystem
↓
AutonomousActionSystem
```

Un second scénario valide vingt Ticks sans entrée joueur avec déclin de Fatigue et repos autonomes répétés.

Cette preuve confirme une régulation autonome minimale dans le temps ; elle ne crée aucune règle nouvelle de fréquence d'Action et ne transforme pas `1 Tick` en durée universelle d'une Action.

---

# 16. Frontière avec les futures politiques

ENGINE-011 ne couvre pas :

- arbitrage entre plusieurs besoins ;
- priorité dynamique multi-besoins ;
- personnalité ;
- habitudes ;
- ambitions ;
- opportunités PNJ ;
- mémoire individuelle ;
- Mémoire du Monde ;
- anticipation de plusieurs Actions ;
- planification long terme.

Ces sujets nécessiteront leurs propres règles amont avant code.

---

# 17. Invariants

- Une Fatigue égale au seuil ne déclenche rien.
- Une Fatigue strictement inférieure au seuil produit `se_reposer`.
- Une Fatigue supérieure au seuil ne déclenche rien.
- Une Entity sans `NeedsComponent` ne reçoit aucun Intent de cette source.
- La source ne modifie aucun Component.
- La source ne publie aucun Event.
- La source n'avance pas le Tick.
- La source n'utilise aucun hasard.
- L'Acteur de l'Intent est toujours l'Entity reçue.
- Aucun Intent n'est inventé pour Faim, Sante ou Moral dans ce lot.
- L'ordre des Systems reste une donnée explicite du comportement déterministe.

---

# 18. Contrat QA

La couverture validée vérifie notamment :

1. seuil inférieur à `0` rejeté ;
2. seuil supérieur à `100` rejeté ;
3. Entity sans `NeedsComponent` → `null` ;
4. Fatigue supérieure au seuil → `null` ;
5. Fatigue égale au seuil → `null` ;
6. Fatigue inférieure au seuil → Intent `se_reposer` ;
7. l'Intent référence le bon Acteur ;
8. la source ne modifie pas `NeedsComponent` ;
9. mêmes entrées → même décision ;
10. intégration réelle ENGINE-010 → ENGINE-006 → World ;
11. un besoin non actionnable ne produit pas de faux Intent ;
12. le franchissement du seuil sur plusieurs Ticks déclenche le repos au moment exact attendu ;
13. vingt Ticks sans entrée joueur produisent une régulation autonome déterministe de la Fatigue.

---

# 19. Validation

Validation technique communiquée par le porteur du projet le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 158 / 158 tests réussis
→ 0 échec
```

Les critères ENGINE-011 restent satisfaits et le document conserve la Maturité 4 conformément à MASTER-004.

Cette validation étendue couvre désormais la première décision autonome réelle `Fatigue → se_reposer` ainsi que son comportement multi-Tick minimal. Elle ne vaut pas validation d'une politique multi-besoins.

---

# 20. Traçabilité

```text
MASTER-005 Phase 3
↓
GDB-004B v1.1
↓
ENGINE-010
↓
ENGINE-011
↓
CHRONIQUES-ENGINE
↓
Tests
```

La consolidation TECH/roadmap/README est volontairement différée jusqu'à un point de clôture fonctionnel significatif.

---

# 21. Historique

## Version 1.2

- validation globale étendue à **158 / 158 tests réussis** ;
- ajout de la preuve multi-Tick `NeedsDecaySystem → AutonomousActionSystem` ;
- validation du franchissement strict du seuil après décroissance ;
- validation d'une régulation de Fatigue sur vingt Ticks sans entrée joueur ;
- aucune consolidation transverse déclenchée, le jalon fonctionnel global n'étant pas encore atteint.

## Version 1.1

- implémentation `NeedsIntentSource` confirmée ;
- validation locale communiquée : **156 / 156 tests réussis** ;
- ENGINE-011 passe à **Validée / Maturité 4** ;
- aucune extension aux besoins non actionnables ;
- consolidation transverse différée jusqu'au prochain jalon significatif.

## Version 1.0

- création de la première spécification de décision autonome métier ;
- traduction du contrat `Fatigue → se_reposer` de GDB-004B v1.1 ;
- seuil de Fatigue laissé configurable ;
- frontière stricte avec les futurs arbitrages multi-besoins et couches psychologiques.

---

Fin du document
