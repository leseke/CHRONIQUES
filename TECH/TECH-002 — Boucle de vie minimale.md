# TECH-002 — Boucle de vie minimale

> Version : 1.0  
> Statut : Validé  
> Maturité : 4  
> Bibliothèque : TECH  
> Implémentation : `CHRONIQUES-ENGINE`  
> Spécification : `ENGINE-009`

---

# 1. Objectif

Documenter l'implémentation réelle de la boucle de vie minimale validée dans `CHRONIQUES-ENGINE`.

TECH-002 décrit la couche d'orchestration permettant de relier :

```text
personnage actif
↓
Action joueur
↓
Scheduler / Systems
↓
vieillissement
↓
mort
↓
HeritageSystem
↓
continuité avec l'héritier
```

Ce document ne définit aucune nouvelle règle métier.

La source d'autorité architecturale reste :

```text
ENGINE-009
```

Les règles de relations, compétences et héritage restent définies par leurs documents GDB et par ENGINE-008.

---

# 2. État de validation

L'implémentation documentée ici a été validée le 11 août 2026.

```text
dotnet build
→ succès

dotnet test
→ 134 / 134 tests réussis

Échecs
→ 0
```

La validation comprend :

- les tests historiques du moteur ;
- les tests unitaires de `LifeSession` ;
- les invariants QA d'ENGINE-009 ;
- le test d'intégration de continuité v0.3.

---

# 3. Périmètre

TECH-002 couvre principalement :

```text
Simulation/Chroniques.Simulation/Session/LifeSession.cs
Tests/Chroniques.Simulation.Tests/LifeSessionTests.cs
```

Il décrit aussi les interactions de cette couche avec :

```text
World
Scheduler
Lifecycle
World.Events
AgingSystem
HeritageSystem
Action Pipeline
```

TECH-002 ne documente pas à nouveau l'implémentation interne des Systems de population déjà couverte par TECH-001.

---

# 4. Position dans le moteur

L'implémentation ajoute une couche `Session` au-dessus du World et du Scheduler.

```text
Application / joueur
        │
        ├── Action Pipeline
        │        ↓
        │      World
        │
        └── LifeSession
                 ↓
             Scheduler
                 ↓
              Systems
                 ↓
               World
                 ↓
          résultat observable
                 ↓
            LifeSession
```

`LifeSession` est une couche d'orchestration.

Elle n'est pas un `ISystem`.

---

# 5. LifeSessionState

L'implémentation contient :

```csharp
public enum LifeSessionState
{
    Active,
    EndedWithoutSuccessor
}
```

Deux états suffisent au périmètre actuel.

## Active

La session possède un personnage contrôlé valide et peut faire progresser le temps.

## EndedWithoutSuccessor

La continuité du personnage contrôlé n'a pas pu être assurée après sa mort.

Aucun état narratif supplémentaire n'est inventé dans TECH-002.

---

# 6. Données portées par LifeSession

`LifeSession` conserve :

```text
World
Scheduler
ActiveCharacterId
State
```

La propriété :

```csharp
public EntityId ActiveCharacterId { get; private set; }
```

représente l'Entity actuellement contrôlée.

Le constructeur refuse un identifiant absent du World.

Cette validation empêche la création d'une session dont le personnage actif n'existe pas.

---

# 7. AdvanceTime

La méthode publique centrale est :

```csharp
AdvanceTime()
```

Son flux réel est :

```text
vérifier que la session est Active
↓
mémoriser le personnage actif avant le Tick
↓
Scheduler.Tick(World)
↓
synchroniser la session après le Tick
```

Un appel actif provoque exactement une progression du Scheduler.

Lorsque la session est terminée :

```text
AdvanceTime
→ aucun Tick supplémentaire
```

---

# 8. Séparation avec les Actions

`LifeSession.AdvanceTime()` ne déclenche aucune Action joueur ou PNJ.

L'Action Pipeline reste indépendant :

```text
Intent
↓
Planner
↓
Plan
↓
Action Instance
↓
Execution Engine
↓
Outcome
↓
Effects
```

Le test d'intégration v0.3 appelle explicitement le pipeline avant de faire progresser la session.

L'implémentation ne crée donc pas la règle :

```text
1 Action = 1 Tick
```

---

# 9. Source de vérité de la mort

Après le Tick, `LifeSession` récupère l'Entity qui était active avant la progression.

La mort est constatée par :

```text
Lifecycle.CurrentState.Name == "mort"
```

`World.Events` n'est pas utilisé comme source de vérité de l'état de vie.

Cette responsabilité reste conforme à ENGINE-009 et à l'architecture existante du moteur.

---

# 10. Passage à l'héritier

Lorsque le personnage actif est mort, `LifeSession` ne sélectionne aucun héritier elle-même.

Elle recherche uniquement le résultat observable déjà produit pendant le Tick courant :

```text
heritage.transmission
source = personnage décédé
target = héritier
```

La recherche est bornée au :

```text
Tick courant
+
Source correspondant au personnage actif avant le Tick
```

Cela empêche la réutilisation d'une transmission ancienne.

Si la cible existe dans le World :

```text
ActiveCharacterId = target
State = Active
```

---

# 11. Cible de transmission invalide

Une transmission observable ne suffit pas à elle seule.

L'Entity cible doit exister réellement dans le World.

Si :

```text
heritage.transmission
→ target inexistante
```

alors la cible ne devient jamais le personnage actif.

La session se termine lorsqu'aucune continuité valide n'est disponible pour le décès traité.

---

# 12. Absence de successeur

Lorsque `HeritageSystem` produit :

```text
heritage.absence-successeur
```

pour le personnage décédé au Tick courant, `LifeSession` passe à :

```text
EndedWithoutSuccessor
```

Elle ne crée pas artificiellement une Entity de remplacement.

---

# 13. World.Events

`LifeSession` lit `World.Events` depuis l'extérieur des Systems.

Cette lecture sert exclusivement à observer le résultat déjà produit par la simulation.

Le flux est :

```text
Systems
↓
mutations du World
+
GameEvent observable
↓
fin du Scheduler.Tick
↓
LifeSession inspecte le résultat
```

Il ne s'agit pas d'un EventBus.

Aucun System n'est déclenché par cette lecture.

---

# 14. Ordre déterministe

Pour la continuité mort → héritage, l'ordre attendu du Scheduler reste :

```text
AgingSystem
↓
HeritageSystem
```

`AgingSystem` peut faire passer le `Lifecycle` à `mort`.

`HeritageSystem`, exécuté ensuite, constate cet état et produit la transmission ou l'absence de successeur.

`LifeSession` ne synchronise le contrôle qu'après la fin complète du Tick.

---

# 15. Absence de logique métier dans LifeSession

Les tests verrouillent explicitement que `LifeSession` :

- ne désigne pas elle-même un héritier ;
- ne modifie pas les relations pour créer une continuité ;
- ne déclenche aucune Action automatiquement ;
- ne réutilise pas une transmission d'un ancien Tick ;
- n'accepte pas une cible absente du World.

La sélection de l'héritier reste entièrement portée par `HeritageSystem`.

---

# 16. Test d'intégration v0.3

Le test de référence est :

```text
ParcoursV03_ActionPuisVieillissementMortEtHeritage_AssureLaContinuite
```

Il assemble réellement plusieurs briques auparavant testées séparément.

Le scénario est :

```text
World créé
↓
Personnage A actif à 79 ans
↓
Action « se_reposer » via ENGINE-006
↓
Outcome réussi
↓
Effect de fatigue appliqué
↓
LifeSession créée
↓
Scheduler avec AgingSystem puis HeritageSystem
↓
progression de 12 mois simulés
↓
A atteint 80 ans
↓
Lifecycle = mort
↓
HeritageSystem produit heritage.transmission(A → B)
↓
LifeSession bascule sur B
↓
State = Active
```

Ce test démontre l'assemblage architectural minimal de la continuité v0.3.

Il ne prétend pas représenter toute la variété future des choix, des âges, des parcours ou du contenu narratif.

---

# 17. Couverture QA spécifique

Les tests `LifeSessionTests` couvrent notamment :

```text
personnage actif inexistant
progression d'exactement un Tick
personnage vivant conservé
mort sans successeur
mort avec transmission
transmission ancienne ignorée
cible inexistante refusée
session terminée figée
absence de sélection d'héritier par LifeSession
absence d'Action automatique
déterminisme de la séquence de contrôle
parcours d'intégration v0.3
```

La suite globale validée contient :

```text
134 tests
134 réussis
0 échec
```

---

# 18. Déterminisme

Un test spécifique construit deux simulations équivalentes avec :

```text
même seed
même état fonctionnel
mêmes Systems
même ordre
mêmes entrées
```

Il compare la séquence logique de personnages actifs :

```text
A
...
A
B
```

Les identifiants GUID créés dans deux Worlds distincts n'ont pas besoin d'être identiques ; c'est la séquence fonctionnelle de contrôle qui est comparée.

---

# 19. Frontière avec v0.4

TECH-002 n'introduit aucun comportement autonome des habitants.

Restent hors de cette implémentation :

- PNJ autonomes ;
- décision automatique ;
- orchestration automatique des Actions de PNJ ;
- Mémoire du Monde ;
- économie autonome ;
- cognition avancée ;
- perception ;
- croyances ;
- émotions.

Ces sujets appartiennent à la phase du monde vivant et nécessiteront leurs propres spécifications avant implémentation.

---

# 20. Traçabilité

Chaîne principale :

```text
PROD — v0.3 Une vie entière
↓
ENGINE-009 — Boucle de vie minimale
↓
CHRONIQUES-ENGINE
↓
Simulation/Chroniques.Simulation/Session/LifeSession.cs
↓
Tests/Chroniques.Simulation.Tests/LifeSessionTests.cs
↓
134 / 134 tests réussis
↓
TECH-002
```

Dépendances techniques importantes :

```text
ENGINE-003
→ Scheduler

ENGINE-006
→ Action Pipeline

ENGINE-008 / TECH-001
→ HeritageSystem et population
```

---

# 21. Limites connues

L'implémentation actuelle ne possède pas :

- de création narrative complète de personnage dans `LifeSession` ;
- de relation automatique entre durée d'Action et Tick ;
- de gestion de contrôle multi-personnage ;
- de logique de refus modifiant automatiquement le contrôle joueur ;
- de patrimoine matériel transmis ;
- de moteur d'autonomie PNJ.

Ces absences sont conformes au périmètre d'ENGINE-009.

---

# 22. Conclusion

La couche de session minimale est désormais implémentée et validée.

Elle fournit au moteur un premier point d'orchestration permettant de démontrer :

```text
Action
+
Temps
+
Vieillissement
+
Mort
+
Héritage
+
Continuité du contrôle
```

sans déplacer les responsabilités des Systems existants.

L'état technique de référence est :

```text
ENGINE-009
→ Validée / Maturité 4

CHRONIQUES-ENGINE
→ build réussi
→ 134 / 134 tests réussis

TECH-002
→ Validé / Maturité 4
```

---

# 23. Historique

## Version 1.0

- création de TECH-002 après validation d'ENGINE-009 ;
- documentation de `LifeSession` et `LifeSessionState` ;
- documentation de la synchronisation mort → héritier ;
- enregistrement du test d'intégration v0.3 ;
- enregistrement des invariants QA complémentaires ;
- état de validation initial : **134 / 134 tests réussis**.
