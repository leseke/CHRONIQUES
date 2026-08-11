# ENGINE-011 — Décision autonome par besoins

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : MASTER-005, GDB-004B v1.1, ACT-002-H, ENGINE-006, ENGINE-010

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

Structure attendue :

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

Le nom exact peut évoluer si la responsabilité reste identique.

---

# 6. Validation du seuil

Le seuil de Fatigue est une valeur de satisfaction compatible avec GDB-004B :

```text
0 <= seuil <= 100
```

Une valeur hors de cet intervalle constitue une erreur de configuration et doit être rejetée à la construction.

Le seuil n'est pas une constante GDB.

L'assemblage ou les tests doivent donc le fournir explicitement.

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

la source doit retourner :

```text
même Intent
```

ou :

```text
null dans les deux cas
```

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

`NeedsIntentSource` doit pouvoir être injectée directement dans :

```text
AutonomousActionSystem
```

sans modification de celui-ci.

ENGINE-011 valide ainsi que la frontière créée par ENGINE-010 permet réellement l'ajout progressif de politiques métier distinctes.

---

# 14. Intégration avec ENGINE-006

Le test d'intégration de référence doit démontrer :

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

Le test peut utiliser l'adaptateur d'exécution déjà employé pour ENGINE-010.

ENGINE-011 ne généralise pas `PipelineRunner`.

---

# 15. Frontière avec les futures politiques

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

# 16. Invariants

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

---

# 17. Contrat QA

Les tests doivent vérifier au minimum :

1. seuil inférieur à `0` rejeté ;
2. seuil supérieur à `100` rejeté ;
3. Entity sans `NeedsComponent` → `null` ;
4. Fatigue supérieure au seuil → `null` ;
5. Fatigue égale au seuil → `null` ;
6. Fatigue inférieure au seuil → Intent `se_reposer` ;
7. l'Intent référence le bon Acteur ;
8. la source ne modifie pas `NeedsComponent` ;
9. mêmes entrées → même décision ;
10. intégration réelle ENGINE-010 → ENGINE-006 → World.

---

# 18. Critères de validation

ENGINE-011 pourra passer en Validée / Maturité 4 lorsque :

- l'implémentation existe dans `CHRONIQUES-ENGINE` ;
- le build réussit ;
- tous les tests existants restent verts ;
- les tests ENGINE-011 sont verts ;
- l'intégration réelle jusqu'au pipeline d'Actions est démontrée ;
- aucun comportement hors GDB-004B v1.1 n'est introduit.

---

# 19. Traçabilité

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
↓
TECH futur après validation
```

---

# 20. Historique

## Version 1.0

- création de la première spécification de décision autonome métier ;
- traduction du contrat `Fatigue → se_reposer` de GDB-004B v1.1 ;
- seuil de Fatigue laissé configurable ;
- frontière stricte avec les futurs arbitrages multi-besoins et couches psychologiques.

---

Fin du document
