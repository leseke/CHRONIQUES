# TECH-003 — Orchestration des habitants autonomes

> Version : 1.0  
> Statut : Validé  
> Maturité : 4  
> Bibliothèque : TECH  
> Implémentation : `CHRONIQUES-ENGINE`  
> Spécification : `ENGINE-010`

---

# 1. Objectif

Documenter l'implémentation réelle et validée du premier mécanisme d'autonomie des habitants dans `CHRONIQUES-ENGINE`.

TECH-003 décrit uniquement ce qui existe réellement dans le moteur après validation.

Il ne définit aucune nouvelle règle métier.

---

# 2. Autorité

La spécification architecturale est :

```text
ENGINE-010
```

Les autorités amont principales restent :

```text
MASTER-005
GDB-004A
GDB-004B
ACT-002-H
ACT-004-A
ENGINE-003
ENGINE-006
```

TECH-003 décrit leur traduction technique effectivement obtenue.

---

# 3. État de validation

Validation confirmée le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 146 / 146 tests réussis
→ 0 échec
```

Le lot ENGINE-010 ajoute 12 tests à la base précédemment validée à 134 / 134.

---

# 4. Périmètre technique

L'implémentation couverte comprend :

```text
IAutonomousIntentSource
IAutonomousIntentExecutor
AutonomousActionSystem
AutonomousActionSystemTests
```

Le test d'intégration utilise également le `PipelineRunner` déjà présent afin de démontrer le raccordement avec ENGINE-006.

---

# 5. Position dans le moteur

```text
Scheduler
│
└── AutonomousActionSystem
        │
        ├── Acteurs enregistrés
        │
        ├── IAutonomousIntentSource
        │       ↓
        │      Intent?
        │
        └── IAutonomousIntentExecutor
                ↓
            ENGINE-006
                ↓
              World
```

Le System d'autonomie est un `ISystem` ordinaire.

Il ne modifie pas le Scheduler.

---

# 6. IAutonomousIntentSource

La source d'Intent possède le contrat :

```csharp
Intent? CreateIntent(
    Entity actor,
    World world,
    Tick currentTick);
```

Elle peut :

- observer l'Acteur ;
- observer le World ;
- utiliser le Tick courant ;
- retourner un Intent ;
- retourner `null`.

Elle ne doit pas :

- modifier directement le World ;
- créer une Action Instance ;
- appliquer un Effect ;
- publier un Event comme substitut au pipeline.

Aucune implémentation de politique métier universelle n'est fournie par TECH-003.

---

# 7. IAutonomousIntentExecutor

La frontière d'exécution possède le contrat :

```csharp
void Execute(Intent intent, World world);
```

Elle permet à `AutonomousActionSystem` de rester indépendant :

- du Planner concret ;
- de l'Execution Engine concret ;
- des Verbes ;
- des Effects particuliers.

Cette interface ne constitue pas un second pipeline d'Actions.

---

# 8. AutonomousActionSystem

Le System conserve une liste ordonnée d'`EntityId` enregistrés comme autonomes.

L'enregistrement est idempotent.

Conceptuellement :

```text
RegisterActor(A)
RegisterActor(A)
↓
A n'est présent qu'une fois
```

Cette propriété empêche un double traitement accidentel pendant un même `Update`.

---

# 9. Traitement d'un Acteur

Pour chaque Acteur enregistré :

```text
Entity existe ?
├── non → ignorer
└── oui
    ↓
Lifecycle = mort ?
├── oui → ignorer
└── non
    ↓
CreateIntent(...)
    ↓
Intent null ?
├── oui → continuer
└── non
    ↓
intent.Acteur == actor.Id ?
├── non → erreur d'intégration
└── oui
    ↓
Execute(intent, world)
```

---

# 10. Ordre déterministe

Les Acteurs sont évalués dans l'ordre de leur enregistrement.

Le System n'utilise pas une collection dont l'ordre d'itération serait implicitement instable comme source de l'ordre d'action.

Les tests verrouillent cette propriété.

---

# 11. Autorité temporelle

`AutonomousActionSystem.Update` ne fait jamais avancer le World.

```text
Scheduler.Tick
→ World.Advance
→ Systems.Update
```

reste l'unique flux temporel.

Un appel direct à `AutonomousActionSystem.Update` laisse donc `World.CurrentTick` inchangé.

---

# 12. Frontière avec Lifecycle

Une Entity dont :

```text
Lifecycle.CurrentState.Name == "mort"
```

n'est pas interrogée par la source d'Intent et n'agit pas.

Cette vérification est minimale et ne remplace pas les contrats d'éligibilité ACT plus généraux.

---

# 13. Intégration avec ENGINE-006

Le test d'intégration réel utilise le Verbe déjà exécutable « Se reposer ».

Flux observé :

```text
Scheduler.Tick
↓
AutonomousActionSystem
↓
Intent "se_reposer"
↓
adaptateur IAutonomousIntentExecutor
↓
PipelineRunner
↓
ActionInstance
↓
Outcome
↓
Effect
↓
NeedsComponent modifié
↓
GameEvent observable
```

Le test vérifie notamment :

```text
ActionState.Archived
OutcomeForme.Reussite
Fatigue > valeur initiale
besoin.fatigue.restauree présent dans World.Events
```

---

# 14. Ce que l'implémentation ne fait pas

Le code validé ne contient pas :

- d'IA générale de PNJ ;
- de score universel de besoins ;
- de mapping complet `besoin → Intent` ;
- d'Habitudes ;
- d'Ambitions ;
- de Mémoire du Monde ;
- d'économie autonome ;
- de catalogue complet de Verbes ;
- de règle `1 Action = 1 Tick`.

Ces absences sont volontaires et conformes à ENGINE-010.

---

# 15. Couverture QA

Les 12 tests ajoutés vérifient notamment :

```text
Acteur vivant enregistré → interrogé
Acteur non enregistré → ignoré
Acteur absent → ignoré
Acteur mort → ignoré
Intent null → aucune exécution
Intent valide → une exécution
mauvais Acteur dans Intent → rejet
ordre d'enregistrement → conservé
double enregistrement → idempotent
déterminisme → conservé
Update direct → aucun avancement du Tick
Scheduler → autonomie → PipelineRunner → World → validé
```

---

# 16. Résolution technique d'ENGINE-C06

ENGINE-C06 décrivait la lacune de raccordement entre le Scheduler et le pipeline d'Actions pour des habitants autonomes.

Cette lacune est maintenant couverte par :

```text
ENGINE-010
↓
AutonomousActionSystem
↓
IAutonomousIntentSource
↓
IAutonomousIntentExecutor
↓
ENGINE-006
↓
Tests
↓
146 / 146
```

La lacune d'orchestration est donc techniquement résolue.

La politique de décision des habitants reste un sujet distinct.

---

# 17. Traçabilité

```text
MASTER-005 Phase 3
↓
GDB-004A / GDB-004B
↓
ACT Intent / Acteur
↓
ENGINE-010
↓
AutonomousActionSystem.cs
IAutonomousIntentSource.cs
IAutonomousIntentExecutor.cs
↓
AutonomousActionSystemTests.cs
↓
146 / 146 tests
↓
TECH-003
```

---

# 18. État final du lot

```text
Spécification    ✅
Implémentation   ✅
Build            ✅
Tests            ✅ 146 / 146
Validation       ✅
TECH             ✅
```

ENGINE-010 est donc documenté comme un lot techniquement stable.

---

# 19. Historique

## Version 1.0

- création de TECH-003 après validation ENGINE-010 ;
- documentation de `AutonomousActionSystem` ;
- documentation des deux frontières d'injection ;
- intégration réelle avec ENGINE-006 documentée ;
- validation initiale enregistrée à **146 / 146 tests réussis** ;
- résolution technique d'ENGINE-C06 enregistrée ;
- limites avec la future politique de décision maintenues explicitement.
