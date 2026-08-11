# TECH-001 — Systems de population

> Version : 1.0  
> Statut : Validé  
> Maturité : 4  
> Bibliothèque : TECH  
> Implémentation : `CHRONIQUES-ENGINE`  
> Spécification : `ENGINE-008`

---

# 1. Objectif

Documenter l'implémentation réelle des premiers Systems de population du moteur Chroniques.

Ce document décrit :

- les classes effectivement présentes dans `CHRONIQUES-ENGINE` ;
- leurs responsabilités techniques ;
- leurs interactions ;
- les choix d'implémentation retenus ;
- les tests associés ;
- les écarts volontairement différés.

Il ne définit aucune nouvelle règle métier.

Les autorités restent :

```text
GDB-004C
→ Relations sociales

GDB-004H
→ Compétences

GDB-004J
→ Transmission

ENGINE-008
→ Architecture des Systems de population
```

TECH-001 décrit uniquement leur traduction réellement implémentée.

---

# 2. État de validation

L'implémentation documentée ici est actuellement validée par :

```text
dotnet build
→ succès

dotnet test
→ 122 / 122 tests réussis

Échecs
→ 0
```

Le lot est donc considéré techniquement stable à la date de création du présent document.

---

# 3. Périmètre

TECH-001 couvre :

```text
RelationComponent
RelationSystem

SkillComponent
SkillSystem

HeritageSystem

RelationInteractionEffect
SkillPracticeEffect
HeritageRefusalEffect

PopulationEffectApplicator
```

Ne sont pas couverts :

- mémoire des habitants ;
- émotions ;
- perception ;
- croyances ;
- réputation complète ;
- patrimoine matériel ;
- transmission matérielle complète.

---

# 4. Position dans le moteur

```text
                Scheduler
                    │
                    ▼
              Systems temporels
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
RelationSystem  SkillSystem  HeritageSystem
        ▲           ▲           ▲
        │           │           │
        └──── PopulationEffectApplicator
                        ▲
                        │
                     Effects
                        ▲
                        │
                 Action Pipeline
```

Deux flux coexistent.

## Flux temporel

```text
Scheduler
↓
Update()
↓
évolution naturelle du World
```

## Flux déclenché par une Action

```text
Action
↓
Effect
↓
PopulationEffectApplicator
↓
System responsable
↓
mutation du World
```

Ces deux flux utilisent les mêmes Systems comme sources de vérité métier.

---

# 5. RelationComponent

`RelationComponent` porte les relations sociales d'une Entity.

Il contient une collection de :

```csharp
Relation
```

Chaque Relation contient notamment :

```text
Cible
Type
Force
CreeeAu
Episodes
```

Le Component ne contient aucune logique d'évolution temporelle.

Les mutations passent par `RelationSystem`.

---

# 6. TypeRelation

Les types actuellement représentés sont :

```csharp
Familiale
Amicale
Professionnelle
Commerciale
Politique
Conflictuelle
Sentimentale
```

Ils traduisent directement la classification définie par GDB-004C.

---

# 7. Episode

Un `Episode` représente une interaction suffisamment importante pour rester attachée à une relation.

Structure conceptuelle :

```text
Tick
Description
Impact
```

Tous les échanges ne produisent pas nécessairement un Episode.

La création dépend du seuil configuré dans `RelationSystem`.

---

# 8. RelationSystem

`RelationSystem` implémente deux catégories de comportement.

## Évolution temporelle

Via :

```csharp
Update(World world, Tick currentTick)
```

Il applique :

- érosion naturelle ;
- plancher familial ;
- suppression des relations arrivées à Force 0.

---

## Interaction explicite

Via :

```csharp
EnregistrerInteraction(...)
```

Il applique :

- création éventuelle de la relation ;
- modification de la Force ;
- bornage entre 0 et 100 ;
- création éventuelle d'un Episode ;
- suppression éventuelle de la relation.

---

# 9. Paramètres de RelationSystem

Les paramètres sont injectés au constructeur.

Ils comprennent notamment :

```text
erosionParTick
plancherFamilial
seuilImportanceEpisode
capaciteEpisodes
forceInitiale
```

Les valeurs utilisées par défaut constituent des paramètres techniques actuels.

Elles ne doivent pas être interprétées comme des constantes définitives du Game Design.

---

# 10. Plancher familial

Une correction importante a été appliquée pendant l'implémentation.

Le comportement initial pouvait provoquer :

```text
Force = 5
Plancher = 10

Update
↓
Force = 10
```

Cette remontée automatique était incorrecte.

Le comportement actuel est :

## Relation au-dessus du plancher

```text
Force = 12
Plancher = 10
Érosion = 5

↓
Force = 10
```

## Relation déjà sous le plancher

```text
Force = 5
Plancher = 10

↓
Force reste 5
```

Le plancher protège contre l'érosion.

Il ne restaure jamais une relation.

---

# 11. Rupture familiale

Une interaction négative peut faire passer une relation Familiale sous son plancher.

Elle peut également atteindre :

```text
Force = 0
```

Dans ce cas :

```text
RelationComponent
↓
Relation supprimée
```

La relation familiale est donc résistante à l'érosion temporelle, mais pas invulnérable aux interactions.

---

# 12. SkillComponent

`SkillComponent` porte un dictionnaire de Compétences.

Structure conceptuelle :

```text
Nom de compétence
↓
Competence
    ├── Niveau
    └── DernierePratique
```

Le Component reste uniquement un conteneur d'état.

---

# 13. SkillSystem

`SkillSystem` possède deux responsabilités principales.

## Pratique

Via :

```csharp
Pratiquer(...)
```

La première pratique crée la Compétence si nécessaire.

Puis :

```text
pratique
↓
calcul du gain
↓
Niveau augmenté
↓
DernierePratique mise à jour
```

---

## Inactivité

Via :

```csharp
Update(...)
```

Le System vérifie la durée écoulée depuis la dernière pratique.

Avant le seuil :

```text
aucun déclin
```

Après le seuil :

```text
déclin appliqué
```

---

# 14. Progression des Compétences

Le gain respecte :

```text
Niveau faible
→ gain plus élevé

Niveau élevé
→ gain plus faible
```

Le Niveau reste borné :

```text
0 <= Niveau <= 100
```

À proximité de 100, le gain devient nul ou négligeable selon la formule actuelle.

La propriété importante est la décroissance du gain marginal, pas la forme mathématique exacte.

---

# 15. HeritageSystem

`HeritageSystem` constitue actuellement la source de vérité de la logique minimale d'héritage.

Il ne possède pas de Component dédié.

Il utilise :

```text
Lifecycle
+
RelationComponent
```

---

# 16. Détection de la mort

La détection ne repose pas sur `World.Events`.

Le System inspecte directement :

```text
Lifecycle.CurrentState.Name
```

et recherche :

```text
"mort"
```

Le flux est donc :

```text
AgingSystem
↓
Lifecycle modifié
↓
HeritageSystem.Update
↓
détection
```

Cela garantit que `World.Events` reste uniquement un journal d'observabilité.

---

# 17. Unicité du traitement

`HeritageSystem` conserve les identifiants des Entities déjà traitées.

Une Entity morte ne peut donc provoquer qu'une seule tentative de transmission.

Conceptuellement :

```text
Entity morte
↓
déjà traitée ?
    ├── oui → ignorer
    └── non → traiter puis mémoriser
```

---

# 18. Désignation de l'héritier

La sélection est déterministe.

Ordre :

```text
Relations Familiales disponibles ?
↓
oui → priorité aux Familiales

Puis :

Force la plus élevée
↓
égalité
↓
relation la plus ancienne
```

Si aucune relation Familiale n'existe, les autres relations peuvent être considérées conformément à la spécification actuelle.

---

# 19. Absence de successeur

Si aucun héritier valide ne peut être obtenu :

```text
heritage.absence-successeur
```

est publié dans le journal du World.

Cet événement sert uniquement à l'observabilité.

---

# 20. Transmission minimale

Lorsqu'un héritier est désigné :

```text
heritage.transmission
```

est publié.

À ce stade, cette transmission ne représente pas encore un déplacement réel de patrimoine.

Elle matérialise uniquement le fait qu'une transmission devrait avoir lieu entre :

```text
défunt
↓
héritier
```

---

# 21. Refus d'héritage

Le refus utilise désormais un chemin unique.

```text
HeritageRefusalEffect
↓
PopulationEffectApplicator
↓
HeritageSystem.RefuserHeritage
↓
heritage.refus
```

Le premier prototype traitait directement le refus dans le resolver.

Cette responsabilité a été déplacée vers `HeritageSystem`.

Le resolver ne contient donc plus la logique métier du refus.

---

# 22. Effects de population

Les Effects actuellement définis sont :

```text
RelationInteractionEffect
SkillPracticeEffect
HeritageRefusalEffect
```

Ils représentent uniquement des données.

Ils ne mutent pas eux-mêmes le World.

---

# 23. PopulationEffectApplicator

`PopulationEffectApplicator` constitue le resolver spécialisé actuellement utilisé pour les Effects de population.

Il reçoit :

```text
IEffect
```

puis détermine quel System en est responsable.

Dispatch actuel :

```text
RelationInteractionEffect
↓
RelationSystem.EnregistrerInteraction
```

```text
SkillPracticeEffect
↓
SkillSystem.Pratiquer
```

```text
HeritageRefusalEffect
↓
HeritageSystem.RefuserHeritage
```

---

# 24. Découplage avec ENGINE-006

Le pipeline d'Actions ne connaît pas les Systems de population.

Il produit des Effects.

```text
ENGINE-006
↓
Effect
```

Puis :

```text
TECH-001 / ENGINE-008
↓
resolver
↓
System
```

Ajouter une nouvelle logique de population ne doit donc pas obliger `PipelineRunner` à connaître chaque System concret.

---

# 25. World.Events

`World.Events` est utilisé comme journal de faits observables.

Exemples actuels :

```text
vie.mort
heritage.transmission
heritage.absence-successeur
heritage.refus
```

Aucun System couvert par TECH-001 ne doit lire cette collection afin de décider de son comportement.

---

# 26. Transmission incomplète

La transmission incomplète n'est pas implémentée.

Elle nécessiterait notamment :

```text
PatrimoineComponent ou équivalent
Assets
Propriété
Règles de transmission
Redistribution
```

Ces structures n'existent pas encore.

L'implémentation est donc volontairement différée.

---

# 27. Tests RelationSystem

Les tests couvrent notamment :

```text
érosion naturelle
plancher familial
descente jusqu'au plancher
absence de remontée sous le plancher
rupture familiale
création de relation
suppression à Force 0
création d'Episode
absence d'Episode
éviction de l'Episode le plus ancien
RelationInteractionEffect
```

---

# 28. Tests SkillSystem

Les tests couvrent notamment :

```text
première pratique
gain maximal initial
gain décroissant
Niveau proche de 100
absence de déclin avant seuil
déclin après seuil
SkillPracticeEffect
```

---

# 29. Tests HeritageSystem

Les tests couvrent notamment :

```text
priorité familiale
tie-break par ancienneté
transmission observable
absence de successeur
absence de RelationComponent
non-retraitement
refus
héritier invalide
défunt invalide
HeritageRefusalEffect
```

---

# 30. Validation finale

État de la branche ayant servi à créer TECH-001 :

```text
dotnet build
✅ succès
```

```text
dotnet test

Total : 122
Réussis : 122
Échecs : 0
```

Cette validation constitue la référence initiale de TECH-001.

Toute modification ultérieure des Systems concernés devra conserver ou mettre à jour les tests associés.

---

# 31. Limites connues

Les limites actuelles sont volontaires.

## Relations

Pas encore de :

- réputation complète ;
- mémoire psychologique ;
- propagation sociale ;
- perception individuelle.

## Compétences

Pas encore de :

- spécialisation avancée ;
- transmission culturelle ;
- enseignement structuré.

## Héritage

Pas encore de :

- patrimoine matériel ;
- partage des biens ;
- testament ;
- fiscalité ;
- conflits successoraux ;
- transmission incomplète réelle.

---

# 32. Évolutions futures

Les évolutions devront suivre :

```text
GDB
↓
ENGINE
↓
Code
↓
Tests
↓
TECH
```

TECH-001 ne doit jamais devenir l'endroit où une règle métier future est inventée.

---

# 33. Correspondance documentaire

```text
GDB-004C
↓
ENGINE-008
↓
RelationComponent
RelationSystem
↓
TECH-001
```

```text
GDB-004H
↓
ENGINE-008
↓
SkillComponent
SkillSystem
↓
TECH-001
```

```text
GDB-004J
↓
ENGINE-008
↓
HeritageSystem
↓
TECH-001
```

---

# 34. Statut

```text
Spécification ENGINE
✅

Implémentation
✅

Build
✅

Tests
✅ 122 / 122

Documentation TECH
✅
```

Le lot **Relations / Compétences / Héritage minimal** est donc considéré documenté dans son état actuel.

---

# Historique

## Version 1.0

- création du premier document numéroté de la bibliothèque TECH ;
- documentation de l'implémentation d'ENGINE-008 ;
- documentation de `RelationComponent` et `RelationSystem` ;
- documentation de `SkillComponent` et `SkillSystem` ;
- documentation de `HeritageSystem` ;
- documentation de `PopulationEffectApplicator` ;
- documentation des trois Effects de population ;
- intégration du correctif du plancher familial ;
- intégration de la centralisation du refus dans `HeritageSystem` ;
- transmission incomplète explicitement différée ;
- état de validation initial : **122 / 122 tests réussis**.
