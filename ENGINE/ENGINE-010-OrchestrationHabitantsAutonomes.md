# ENGINE-010 — Orchestration des habitants autonomes

> Version : 1.1
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : MASTER-005, GDB-004A, GDB-004B, ACT-002-H, ACT-004-A, ENGINE-003, ENGINE-006, ENGINE-009
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 146 / 146 tests réussis

---

# 1. Objectif

Définir le premier mécanisme architectural de la Phase 3 de `MASTER-005 — Le monde vivant` : permettre à un habitant explicitement considéré comme autonome d'initier une Action sans intervention du joueur, tout en réutilisant le pipeline d'Actions existant.

Le parcours validé est :

```text
Scheduler.Tick
↓
AutonomousActionSystem
↓
acteur autonome enregistré
↓
IAutonomousIntentSource
↓
Intent éventuel
↓
IAutonomousIntentExecutor
↓
ENGINE-006 Action Pipeline
↓
Outcome / Effects
↓
World
```

ENGINE-010 répond au besoin architectural conservé par le constat `ENGINE-C06`.

---

# 2. Autorités amont

## MASTER-005

La Phase 3 exige notamment des habitants autonomes qui poursuivent leur existence indépendamment du joueur.

## GDB-004A

Les habitants poursuivent leur existence même lorsque le joueur n'interagit pas avec eux.

## GDB-004B

Les besoins constituent l'un des moteurs principaux de leurs décisions.

## ACT

Une Action provient d'un `Intent` porté par un Acteur et traverse le pipeline ACT / ENGINE-006.

ENGINE-010 ne contourne jamais cette chaîne.

---

# 3. Responsabilité exacte

ENGINE-010 résout uniquement l'orchestration automatique entre :

- le Tick déterministe d'ENGINE-003 ;
- un habitant explicitement enregistré comme autonome ;
- une source d'Intent ;
- un exécuteur conforme à ENGINE-006.

Il fournit le raccordement :

```text
Scheduler
↓
Action autonome
```

sans devenir une intelligence artificielle complète.

---

# 4. Séparation des responsabilités

```text
AutonomousActionSystem
= orchestration

IAutonomousIntentSource
= proposition éventuelle d'un objectif

IAutonomousIntentExecutor
= remise de l'Intent à l'exécution ENGINE-006
```

Ces responsabilités restent séparées.

`AutonomousActionSystem` ne choisit aucune règle métier et ne connaît aucun Verbe concret.

---

# 5. Implémentation validée

Le moteur contient désormais :

```text
Simulation/Chroniques.Simulation/Autonomy/
├── IAutonomousIntentSource.cs
├── IAutonomousIntentExecutor.cs
└── AutonomousActionSystem.cs
```

Les tests associés sont portés notamment par :

```text
Tests/Chroniques.Simulation.Tests/
└── AutonomousActionSystemTests.cs
```

---

# 6. AutonomousActionSystem

`AutonomousActionSystem` implémente `ISystem`.

Il est donc exécuté par le Scheduler dans l'ordre d'enregistrement des Systems.

Il conserve une liste ordonnée d'`EntityId` explicitement enregistrés comme autonomes.

L'enregistrement est idempotent : un même Acteur n'est pas traité plusieurs fois pendant une même invocation à cause d'un double enregistrement.

---

# 7. Éligibilité minimale

Avant de demander un Intent, le System vérifie :

```text
Entity existe dans World
+
Lifecycle != mort
```

Une Entity absente est ignorée.

Une Entity morte est ignorée.

Cette vérification ne remplace ni ACT-004-A ni les Preconditions propres à une Action.

---

# 8. Source d'Intent

Contrat validé :

```csharp
public interface IAutonomousIntentSource
{
    Intent? CreateIntent(
        Entity actor,
        World world,
        Tick currentTick);
}
```

La source peut retourner un Intent ou `null`.

Elle ne doit pas :

- modifier directement le World ;
- créer directement une Action Instance ;
- appliquer directement un Effect ;
- publier directement un Event comme substitut au pipeline ;
- produire un comportement non déterministe à entrées identiques.

---

# 9. Cohérence de l'Acteur

Invariant validé :

```text
intent.Acteur == actor.Id
```

Une source ne peut pas recevoir A puis retourner silencieusement un Intent attribué à B.

Une violation provoque une erreur d'intégration explicite avant l'exécution.

---

# 10. Exécuteur d'Intent

Contrat validé :

```csharp
public interface IAutonomousIntentExecutor
{
    void Execute(Intent intent, World world);
}
```

Cette interface n'est pas un deuxième Action Pipeline.

Elle constitue uniquement la frontière entre l'orchestration autonome et un exécuteur conforme à ENGINE-006.

---

# 11. Frontière avec PipelineRunner

Le moteur ne possède actuellement qu'un `PipelineRunner` concret spécialisé autour du Verbe de démonstration « Se reposer ».

ENGINE-010 ne le généralise pas artificiellement.

Le test d'intégration utilise un adaptateur vers ce `PipelineRunner` afin de démontrer réellement :

```text
Scheduler
↓
AutonomousActionSystem
↓
Intent "se_reposer"
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

Cette preuve valide le raccordement architectural sans prétendre résoudre le futur catalogue complet de Verbes.

---

# 12. Exécution pendant un Tick

Lors d'un `Update` :

```text
pour chaque Acteur enregistré
↓
existence ?
↓
vivant ?
↓
demander Intent
↓
null ? continuer
↓
vérifier l'Acteur de l'Intent
↓
transmettre à l'exécuteur
```

Le System ne fait jamais avancer lui-même le Tick.

Le Scheduler reste l'autorité temporelle.

---

# 13. Ordre déterministe

Les habitants sont évalués dans leur ordre d'enregistrement.

À :

```text
World identique
Seed identique
Tick identique
Acteurs identiques
ordre identique
source identique
exécuteur identique
```

la séquence d'Intents et le résultat observable doivent rester identiques.

Cet invariant est couvert par les tests.

---

# 14. Frontière avec LifeSession

`LifeSession` reste responsable du personnage contrôlé par le joueur.

`AutonomousActionSystem` reste indépendant de `LifeSession`.

Il ne lit jamais `ActiveCharacterId`.

La couche applicative est responsable de ne pas enregistrer comme autonome une Entity qu'elle souhaite réserver au contrôle joueur.

---

# 15. Frontière avec GDB-004B

GDB-004B indique que les besoins influencent les décisions.

Cependant, aucune autorité amont ne fixe encore :

- un score universel de décision ;
- des seuils numériques définitifs ;
- un mapping complet `besoin → Intent` ;
- l'arbitrage complet entre besoins, ambitions, habitudes et opportunités.

ENGINE-010 n'invente donc aucune de ces règles.

La politique de décision concrète constitue un lot futur distinct.

---

# 16. Frontière avec Habitudes et Ambitions

ENGINE-010 n'implémente ni GDB-004E ni GDB-004F.

Ces systèmes pourront alimenter une future `IAutonomousIntentSource` sans modifier la responsabilité d'orchestration validée ici.

---

# 17. Frontière avec la Mémoire du Monde

La Mémoire du Monde n'est pas nécessaire pour prouver la première Action autonome.

ENGINE-010 ne dépend donc pas de cette brique.

Elle reste un chantier distinct de v0.4.

---

# 18. Ce que ENGINE-010 ne définit pas

ENGINE-010 ne définit pas :

- une IA générale ;
- une psychologie complète ;
- des émotions ;
- des croyances ;
- une mémoire individuelle ;
- la Mémoire du Monde ;
- les Habitudes ;
- les Ambitions ;
- les métiers ;
- l'économie autonome ;
- un catalogue complet de Verbes ;
- une formule universelle de choix ;
- une règle `1 Action = 1 Tick`.

---

# 19. Contrat QA validé

La couverture ENGINE-010 vérifie notamment :

- un Acteur enregistré vivant est interrogé ;
- un Acteur non enregistré n'est jamais interrogé ;
- une Entity absente est ignorée ;
- une Entity morte est ignorée ;
- `null` n'exécute rien ;
- un Intent valide est exécuté exactement une fois ;
- un Intent attribué à un autre Acteur est rejeté ;
- plusieurs Acteurs respectent l'ordre d'enregistrement ;
- un double enregistrement reste idempotent ;
- la séquence d'Intents reste déterministe ;
- le System n'avance jamais lui-même le Tick ;
- un test d'intégration traverse réellement le Pipeline d'Actions existant.

---

# 20. Validation technique

Validation confirmée par le porteur du projet le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 146 / 146 tests réussis
→ 0 échec
```

Le lot ajoute 12 tests à la base précédemment validée à 134 / 134.

---

# 21. Résolution d'ENGINE-C06

ENGINE-C06 avait été volontairement différé jusqu'à la Phase 3 de MASTER-005 afin d'éviter d'inventer prématurément l'orchestration des habitants autonomes.

La condition de réouverture a été atteinte après validation de v0.3.

ENGINE-010 fournit maintenant la réponse architecturale, l'implémentation existe, le raccordement réel avec ENGINE-006 est testé et la suite complète est validée.

Le constat peut donc être considéré :

```text
ENGINE-C06
→ Clos
```

La fermeture concerne exclusivement la lacune d'orchestration Scheduler / Actions autonomes.

Elle ne signifie pas que la politique de décision des PNJ est terminée.

---

# 22. Critères de validation

ENGINE-010 est Validée / Maturité 4 car :

- la spécification a précédé le code ;
- l'implémentation respecte les frontières prévues ;
- aucun Verbe concret n'est connu du System d'autonomie ;
- aucun algorithme métier de décision n'a été inventé ;
- l'ordre d'action est déterministe ;
- le Scheduler reste l'autorité sur le Tick ;
- l'intégration avec ENGINE-006 est démontrée ;
- la suite complète passe à 146 / 146.

---

# 23. Prochaine frontière

La prochaine brique de v0.4 ne doit pas être choisie par commodité technique.

Elle doit être ouverte depuis une règle amont suffisamment précise.

Candidats naturels à auditer :

```text
politique minimale de décision des habitants
Mémoire du Monde
événements dynamiques
économie autonome minimale
```

La priorité doit être déterminée par le plus petit besoin concret nécessaire au critère de sortie de MASTER-005 Phase 3.

---

# 24. Historique

## Version 1.1

- ENGINE-010 passe à **Validée / Maturité 4** ;
- implémentation `AutonomousActionSystem` confirmée ;
- contrats `IAutonomousIntentSource` et `IAutonomousIntentExecutor` confirmés ;
- 12 tests ENGINE-010 validés ;
- suite globale portée à **146 / 146 tests réussis** ;
- intégration Scheduler → autonomie → ENGINE-006 → World confirmée ;
- ENGINE-C06 considéré clos ;
- frontière maintenue avec la future politique de décision métier.

## Version 1.0

- création d'ENGINE-010 comme première spécification ENGINE de v0.4 ;
- réouverture ciblée d'ENGINE-C06 à l'entrée en Phase 3 ;
- séparation entre orchestration autonome, décision métier et exécution d'Action ;
- absence volontaire de politique concrète de décision.
