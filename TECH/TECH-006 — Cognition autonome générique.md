# TECH-006 — Cognition autonome générique

> Version : 1.0  
> Statut : Validé  
> Maturité : 4  
> Bibliothèque : TECH  
> Implémentation : `CHRONIQUES-ENGINE`  
> Spécifications : `ENGINE-015`, `ENGINE-016`, `ENGINE-017`  
> Validation de référence : `291 / 291 tests réussis`

---

# 1. Objectif

Documenter l'implémentation réellement obtenue et validée du premier bloc cognitif générique de Chroniques :

```text
observer une exécution autonome réelle
↓
former et faire évoluer des Habitudes
↓
créer et évaluer des Ambitions
↓
produire des Intents cognitifs
↓
repasser par ACT
```

TECH-006 ne crée aucun comportement narratif concret. Il documente exclusivement les infrastructures validées d'ENGINE-015 à ENGINE-017.

---

# 2. Autorités

Chaîne principale :

```text
GDB-004A v1.3
↓
GDB-004D v1.3
GDB-004E v1.2
GDB-004F v1.2
↓
ACT-002-H
↓
ENGINE-015 / 016 / 017
↓
CHRONIQUES-ENGINE
↓
Tests
↓
TECH-006
```

GDB-004A conserve l'autorité sur l'ordre des familles d'Intent.

---

# 3. Observation de l'exécution autonome — ENGINE-015

ENGINE-015 a résolu une frontière technique : `IAutonomousIntentExecutor.Execute(...)` retourne historiquement `void`, alors que les futurs systèmes d'apprentissage doivent distinguer l'Intent sélectionné de l'Outcome réel.

Le moteur a ajouté :

```text
IAutonomousIntentExecutionObserver
PipelineAutonomousIntentExecutor
```

Flux validé :

```text
Intent autonome
↓
BeforeExecution
↓
PipelineRunner
├── exception → ExecutionAborted → rethrow
└── ActionInstance terminée
    ↓
    AfterExecution
```

Restent inchangés :

- `IAutonomousIntentExecutor` ;
- `AutonomousActionSystem` ;
- `PipelineRunner` ;
- ACT `Intent`.

L'observation est donc ajoutée sans créer de second pipeline ni de métadonnée cognitive dans l'Intent.

---

# 4. Habitudes — ENGINE-016

Le moteur a ajouté :

```text
HabitComponent
IHabitRule
IHabitFormationParameterResolver
IHabitStrengthPolicy
HabitSelectionRegistry
HabitIntentSource
HabitLearningObserver
HabitEvolutionSystem
```

`HabitComponent` persiste :

- les Habitudes formées ;
- leur `HabitTypeId` ;
- leur objectif d'Intent ;
- leur Signature de formation ;
- leur Force ;
- leurs Ticks de création/activation ;
- les traces de formation encore incomplètes.

Aucune logique métier ne vit dans le Component.

---

# 5. Formation d'une Habitude

Une règle `IHabitRule` injectée observe un Intent et peut produire une candidate de formation déterministe.

Le moteur groupe les répétitions par :

```text
HabitTypeId
+
IntentObjective
+
FormationSignature
```

Lorsque le nombre de répétitions exigé est atteint dans la fenêtre configurée :

```text
trace de formation
↓
HabitState persistante
```

Le moteur ne calcule aucune similarité contextuelle implicite.

Une exception technique du pipeline ne valide pas une répétition ; un Outcome métier terminé peut en revanche être observé comme une exécution réelle.

---

# 6. Sélection et activation d'une Habitude

`HabitIntentSource` :

1. lit uniquement les données persistées ;
2. exige une règle enregistrée ;
3. exige `Force > 0` ;
4. exige le Déclencheur concret ;
5. exige l'Intent traitable ;
6. sélectionne Force décroissante puis ancienneté ;
7. produit un Intent ACT normal.

La source ne mute pas le World.

`HabitSelectionRegistry` garde temporairement la provenance runtime de la sélection sans enrichir ACT `Intent`.

`HabitLearningObserver` distingue :

```text
formation
≠
activation
≠
renforcement
```

Une Habitude sélectionnée conserve son Tick d'activation même en cas d'abandon technique ultérieur du pipeline.

---

# 7. Renforcement et érosion

`IHabitStrengthPolicy` injecte les formules numériques.

Le framework impose seulement les invariants :

- Force finie ;
- Clamp `[0,100]` ;
- un renforcement ne diminue jamais la Force ;
- une érosion ne l'augmente jamais ;
- `Echec` / `Interruption` ne renforcent pas ;
- une Force ramenée à 0 est supprimée par l'évolution.

`HabitEvolutionSystem` utilise `LastActivatedAt`, ou `CreatedAt` avant la première activation, pour calculer l'inactivité.

Aucune formule universelle n'est imposée.

---

# 8. Ambitions — ENGINE-017

Le moteur a ajouté :

```text
AmbitionComponent
AmbitionState
AmbitionCreationCandidate
AmbitionEvaluation
IAmbitionRule
AmbitionEvolutionSystem
AmbitionIntentSource
```

Une Ambition persistante porte notamment :

```text
AmbitionTypeId
InstanceKey
ObjectivePayload
IntentObjective
Intensity
Progress
IsAbandoned
CreatedAt
```

`ObjectivePayload` reste opaque pour le moteur générique. Seule la règle du Type concret peut l'interpréter.

---

# 9. Création et évaluation des Ambitions

`IAmbitionRule` fournit :

- les candidates de création ;
- l'évaluation du Progrès ;
- la décision d'abandon ;
- la traitabilité de l'Intent.

`AmbitionEvolutionSystem` :

1. interroge les règles dans l'ordre d'enregistrement ;
2. ajoute les nouvelles instances valides non dupliquées ;
3. évalue les Ambitions ayant encore une règle ;
4. borne le Progrès dans `[0,100]` ;
5. persiste l'abandon explicite ;
6. retire les Ambitions dont l'Intensité est tombée à 0.

Une Ambition à `Progress = 100` est accomplie et reste persistée, mais cesse d'être candidate.

---

# 10. Sélection d'une Ambition

`AmbitionIntentSource` filtre :

```text
règle présente
+
Intensity > 0
+
Progress < 100
+
non abandonnée
+
Intent traitable
```

Puis applique l'ordre GDB-004F :

```text
Intensité la plus élevée
↓ égalité
Progrès le plus élevé
↓ égalité
CreatedAt le plus ancien
↓ égalité totale
ordre persistant du Component
```

La source ne mute pas le World et retourne un Intent ACT ordinaire.

---

# 11. Composition complète des familles autonomes

À la fin d'ENGINE-017, la composition compatible est :

```text
NeedsIntentSource
↓ sinon
VoluntaryFoodTransferIntentSource
↓ sinon
ProductiveActivityIntentSource
↓ sinon
HabitIntentSource
↓ sinon
AmbitionIntentSource
↓ sinon
aucun Intent
```

`CompositeAutonomousIntentSource` conserve la règle « première source non-null ».

Aucun score universel n'est introduit entre besoins, économie, Habitudes et Ambitions.

---

# 12. Persistance cognitive

`WorldRepository` persiste désormais :

```text
HabitComponent
AmbitionComponent
```

comme champs optionnels d'`EntitySnapshot`.

Les règles, policies, resolvers et registres de sélection sont des services runtime et ne sont pas sérialisés.

Cette séparation permet au World de conserver l'état cognitif sans figer les algorithmes de décision dans les sauvegardes.

---

# 13. Ce que le moteur ne fait pas encore

TECH-006 ne documente aucune implémentation de :

- Habitude canonique « travail », « repos du soir », « loisir », etc. ;
- Type concret d'Ambition « richesse », « carrière », « logement », etc. ;
- `PersonalityComponent` ;
- mapping Trait/Habitude ;
- mapping Trait/Ambition ;
- perturbation générique des Habitudes par Event ;
- formule universelle d'évolution de l'Intensité ;
- fairness inter-familles ;
- Opportunité PNJ universelle ;
- score psychologique global.

---

# 14. Validation

Repères :

```text
224 / 224
→ base avant observation cognitive

233 / 233
→ ENGINE-015 validée

260 / 260
→ ENGINE-016 validée

291 / 291
→ ENGINE-017 validée
```

La suite globale actuelle démontre la compatibilité du bloc cognitif avec les systèmes antérieurs.

---

# 15. Scénarios prouvés

Le moteur démontre notamment :

```text
Intent répété
↓
formation d'une Habitude
↓
Habitude persistante
↓
Déclencheur
↓
Intent produit par l'Habitude
↓
Action réelle
```

et :

```text
Tick
↓
règle d'Ambition
↓
création + Progrès
↓
Ambition candidate
↓
Intent produit par l'Ambition
↓
Action réelle
```

Les règles utilisées pour la QA sont factices et n'acquièrent aucun statut métier.

---

# 16. État final

```text
ENGINE-015        ✅ Validée / M4
ENGINE-016        ✅ Validée / M4
ENGINE-017        ✅ Validée / M4
Implémentation    ✅
Persistance       ✅
Tests globaux     ✅ 291 / 291
TECH-006          ✅
```

Le bloc constitue le premier **socle cognitif autonome générique** de Chroniques.

---

# Historique

## Version 1.0

- création au point de consolidation suivant ENGINE-017 ;
- documentation consolidée d'ENGINE-015, ENGINE-016 et ENGINE-017 ;
- observation d'exécution, Habitudes et Ambitions documentées ;
- validation globale enregistrée à 291 / 291 ;
- absence de comportements narratifs concrets explicitement maintenue.