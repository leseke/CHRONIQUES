# PROPOSITION — Engagement joueur et modèle psychologique des PNJ

> Version : 2.0  
> Statut : Proposition  
> Type : Proposition de conception  
> Domaine : Game Design / Simulation / Comportement / Engagement  
> Projet : Chroniques

---

# 1. Objet du document

Ce document propose deux évolutions complémentaires de Chroniques :

1. renforcer l'engagement du joueur en s'inspirant de certaines boucles de progression observées dans des jeux à forte rétention, notamment sur Roblox, sans reprendre leurs mécanismes de gambling ou de rétention artificielle ;
2. approfondir le comportement des habitants afin qu'ils agissent selon leur propre perception du monde, leur personnalité, leurs expériences, leurs ambitions et leur histoire.

Ces deux propositions doivent rester distinctes.

La première répond à la question :

> Pourquoi le joueur a-t-il naturellement envie de poursuivre son histoire ?

La seconde répond à la question :

> Pourquoi un habitant choisit-il cette décision plutôt qu'une autre ?

Elles partagent néanmoins un même principe :

> les conséquences produites par la simulation doivent créer de nouvelles possibilités.

---

# 2. Compatibilité avec l'architecture actuelle

Cette proposition ne nécessite aucune remise en cause des fondations actuelles.

Elle s'appuie notamment sur :

- GDB-004 — Les habitants ;
- GDB-006 — L'expérience émotionnelle du joueur ;
- GDB-008 — Temps, générations et évolution ;
- GDB-009 — Structures sociales et valeurs ;
- ACT-002 — Intent, Plan, Action, Outcome et exécution ;
- ACT-004 à ACT-010 — acteurs, cibles, conditions, conséquences, composition et événements ;
- ENGINE-002 — Kernel ;
- ENGINE-003 — Scheduler ;
- ENGINE-004 — Systems ;
- ENGINE-006 — Action Pipeline ;
- le moteur `CHRONIQUES-ENGINE` actuellement implémenté.

Elle constitue donc principalement une **extension du Game Design et de la Simulation**, et non la création d'une nouvelle infrastructure fondamentale.

---

# PARTIE I — ENGAGEMENT JOUEUR

# 3. Principe directeur

GDB-006B établit déjà un principe fondamental :

> Chroniques ne cherche pas à retenir le joueur.  
> Il cherche à lui donner envie de revenir.

Cette proposition ne modifie pas ce principe.

Elle cherche uniquement à renforcer les mécanismes permettant d'obtenir naturellement ce résultat.

Le modèle observé dans certains jeux Roblox peut être résumé ainsi :

```text
Action
↓
Récompense
↓
Progression visible
↓
Statut / reconnaissance
↓
Prochaine possibilité
↓
Nouvelle action
```

Chroniques ne doit pas copier la récompense artificielle.

Il peut en revanche reprendre :

- la lisibilité de la progression ;
- l'anticipation ;
- la présence d'un prochain objectif possible ;
- la reconnaissance sociale ;
- les boucles courtes, moyennes et longues ;
- l'impression constante que l'histoire peut encore évoluer.

---

# 4. Ce que Chroniques ne doit pas reproduire

La proposition exclut explicitement :

- lootboxes ;
- quasi-victoires artificielles ;
- probabilités volontairement opaques ;
- frustration conçue pour déclencher un achat ;
- FOMO ;
- récompenses quotidiennes obligatoires ;
- fausse rareté ;
- pay-to-win ;
- progression artificiellement accélérée ;
- obligation de connexion ;
- inflation infinie des nombres.

Ces pratiques entreraient directement en contradiction avec GDB-006B, GDB-006C et GDB-006J.

Le principe reste :

> Le plaisir, la curiosité et l'histoire personnelle doivent être les moteurs du retour au jeu.

---

# 5. Transposition dans Chroniques

La boucle classique :

```text
Je joue
↓
Je gagne
↓
Je débloque
↓
Je veux davantage
```

devient :

```text
Je prends une décision
↓
Le monde évolue
↓
Ma situation change
↓
De nouvelles possibilités apparaissent
↓
Je veux découvrir leurs conséquences
```

La récompense principale n'est donc pas :

```text
+500 XP
```

mais :

```text
Ma situation m'autorise désormais quelque chose
qui était auparavant impossible, improbable ou inutile.
```

---

# 6. Boucle d'engagement cible

```text
DÉCOUVERTE
    ↓
DÉCISION
    ↓
ACTION
    ↓
OUTCOME
    ↓
CONSÉQUENCES
    ↓
WORLD MODIFIÉ
    ↓
PROGRESSION PERÇUE
    ↓
NOUVELLES POSSIBILITÉS
    ↓
ANTICIPATION
    ↓
NOUVELLE DÉCISION
```

Cette boucle complète naturellement ACT.

ACT reste responsable de :

```text
Intent
↓
Plan
↓
Action
↓
Outcome
↓
Effects
↓
Events
↓
World Update
```

L'engagement du joueur apparaît ensuite dans la manière dont les changements du World deviennent compréhensibles et significatifs.

---

# 7. Trois échelles d'engagement

Chroniques doit maintenir simultanément plusieurs horizons.

## Boucle courte

Durée :

quelques secondes à quelques minutes.

Exemple :

```text
Chercher un travail
↓
Postuler
↓
Être recruté
↓
Premier revenu
```

Le joueur constate immédiatement que sa décision a produit quelque chose.

---

## Boucle moyenne

Durée :

plusieurs dizaines de minutes ou plusieurs sessions.

```text
Premier emploi
↓
Expérience
↓
Compétence
↓
Promotion
↓
Revenus supérieurs
↓
Nouvelles possibilités économiques
```

---

## Boucle longue

Durée :

une vie ou plusieurs générations.

```text
Départ
↓
Carrière
↓
Relations
↓
Famille
↓
Patrimoine
↓
Influence
↓
Transmission
↓
Héritier
```

Cette troisième boucle est particulièrement compatible avec GDB-008 et la vision générationnelle de Chroniques.

---

# 8. Progression perçue

GDB-006C précise déjà :

> La progression doit être ressentie avant d'être mesurée.

La proposition renforce ce principe.

Le joueur doit pouvoir comprendre comment sa situation a évolué sans réduire cette évolution à un niveau numérique unique.

Exemples possibles :

## Économie

```text
Précarité
↓
Stabilité
↓
Confort
↓
Patrimoine
↓
Fortune
```

## Influence sociale

```text
Inconnu
↓
Connu localement
↓
Respecté
↓
Influent
↓
Personnalité majeure
```

## Famille

```text
Individu
↓
Couple
↓
Famille
↓
Lignée
↓
Dynastie
```

Ces catégories doivent être des **lectures de l'état réel de la simulation**, jamais des niveaux arbitraires qui remplaceraient celle-ci.

---

# 9. Progression par ouverture

GDB-006C indique également :

> Une bonne progression ouvre de nouvelles possibilités plutôt qu'elle ne rend les anciennes obsolètes.

Ce principe devient central.

Exemple :

```text
Premier revenu stable
        ↓
┌───────┼─────────┬─────────┐
↓       ↓         ↓         ↓
Louer  Épargner  Investir  Consommer
```

Puis :

```text
Patrimoine suffisant
        ↓
┌──────────┼──────────┐
↓          ↓          ↓
Acheter  Entreprendre  Transmettre
```

La progression augmente donc principalement :

> l'espace des décisions disponibles.

---

# 10. La prochaine possibilité

Le joueur ne doit pas nécessairement recevoir une liste de quêtes.

Il doit cependant pouvoir comprendre qu'une situation crée des possibilités.

Exemple :

```text
Situation

Métier stable
Revenus réguliers
Bonne réputation locale
Relation durable
```

Le World peut désormais permettre :

```text
→ changer de carrière
→ demander une promotion
→ acheter un logement
→ créer une activité
→ fonder une famille
→ entrer dans une organisation
```

Ces possibilités existent parce que l'état du monde les autorise.

Elles ne sont pas créées artificiellement pour occuper le joueur.

---

# 11. Statut social systémique

GDB-004I définit déjà la réputation comme :

> la perception qu'ont les autres d'un individu à partir des faits qu'ils connaissent.

La proposition ne doit donc pas créer une nouvelle jauge globale de prestige.

Elle doit exploiter ce système existant.

Exemple :

```text
Le personnage s'enrichit
↓
Certaines personnes l'observent
↓
Leur perception évolue
↓
Sa réputation locale évolue
↓
Leurs comportements peuvent changer
```

Conséquences possibles :

- admiration ;
- jalousie ;
- confiance ;
- méfiance ;
- demandes d'aide ;
- propositions commerciales ;
- alliances ;
- tentatives d'exploitation ;
- criminalité.

Le statut devient intéressant parce qu'il **transforme les relations et les possibilités**.

---

# 12. Progression générationnelle

La transmission prévue par GDB-004J et GDB-008 permet à Chroniques d'aller au-delà d'une progression limitée au personnage actuel.

```text
Vie A
↓
Décisions
↓
Conséquences
↓
Transmission
↓
Vie B
```

Peuvent notamment survivre ou évoluer :

- patrimoine ;
- relations familiales ;
- réputation ;
- ennemis ;
- culture ;
- connaissances ;
- héritages ;
- conséquences historiques.

La mort devient alors :

> une transformation de la progression plutôt qu'une suppression complète de celle-ci.

---

# 13. Incertitude systémique

Le modèle Roblox peut utiliser le hasard pour provoquer l'anticipation.

Chroniques dispose déjà d'une alternative plus cohérente :

> l'incertitude créée par l'interaction des systèmes.

Exemple :

```text
Créer une entreprise
```

peut produire :

```text
succès
association
concurrence
innovation
dette
faillite
conflit
fortune
influence
```

L'incertitude ne provient donc pas nécessairement d'une roulette cachée.

Elle provient de :

- l'état du World ;
- les autres habitants ;
- l'économie ;
- les relations ;
- les événements ;
- les décisions précédentes.

Lorsque du hasard est nécessaire, il reste soumis au RNG déterministe existant dans le Kernel.

---

# 14. Échec productif

GDB-006J établit déjà :

> L'échec a aussi une valeur.

La proposition renforce cette orientation.

```text
Échec
↓
Situation modifiée
↓
Nouveaux problèmes
↓
Nouvelles possibilités
```

Exemple :

```text
Entreprise
↓
Faillite
↓
Dette
↓
Tensions familiales
↓
Déménagement
↓
Nouvelle profession
```

L'objectif n'est donc pas de garantir le succès.

L'objectif est de garantir :

> que les conséquences intéressantes ne s'arrêtent pas avec l'échec.

---

# 15. Progression horizontale

Les différentes vies doivent pouvoir être incomparables.

```text
Médecin
≠
Entrepreneur
≠
Criminel
≠
Parent
≠
Artiste
≠
Politicien
```

Aucune trajectoire ne doit nécessairement être considérée comme supérieure aux autres.

La découverte d'une nouvelle manière de vivre peut elle-même constituer une récompense.

---

# 16. Formule finale d'engagement

La transposition retenue devient :

```text
ACTION SIGNIFICATIVE
        ↓
CONSÉQUENCE
        ↓
WORLD TRANSFORMÉ
        ↓
CHANGEMENT PERCEPTIBLE
        ↓
NOUVELLES POSSIBILITÉS
        ↓
CURIOSITÉ / ANTICIPATION
        ↓
NOUVELLE DÉCISION
```

Chroniques ne doit pas chercher à rendre :

```text
la prochaine récompense
```

irrésistible.

Il doit chercher à rendre :

```text
la prochaine conséquence
```

intéressante à découvrir.

---

# PARTIE II — MODÈLE PSYCHOLOGIQUE DES HABITANTS

# 17. Position par rapport à GDB-004

Cette proposition ne remplace pas GDB-004.

Elle cherche à relier et approfondir plusieurs concepts qui y existent déjà :

```text
GDB-004B  Besoins
GDB-004C  Relations
GDB-004D  Personnalité
GDB-004E  Habitudes
GDB-004F  Ambitions
GDB-004G  Connaissances
GDB-004H  Compétences
GDB-004I  Réputation
GDB-004J  Transmission
```

Le modèle psychologique proposé constitue donc avant tout :

> une architecture comportementale permettant à ces concepts de produire des décisions autonomes.

---

# 18. Principe directeur

Un habitant ne doit pas fonctionner selon :

```text
WORLD OBJECTIF
↓
RÈGLE
↓
ACTION
```

Il doit fonctionner selon :

```text
WORLD
↓
INFORMATION ACCESSIBLE
↓
REPRÉSENTATION PERSONNELLE
↓
DÉCISION
```

Le personnage ne réagit donc pas nécessairement à ce qui est vrai.

Il réagit à :

> ce qu'il sait, croit, ressent et considère important.

---

# 19. Modèle cible révisé

Compte tenu des concepts déjà présents dans GDB-004 et ACT, le modèle proposé devient :

```text
WORLD
↓
Perception
↓
Attention
↓
Interprétation
↓
État émotionnel
↓
Connaissances / Mémoire
↓
Croyances
↓
Personnalité
↓
Valeurs
↓
Besoins
↓
Ambitions / Motivations
↓
Objectifs
↓
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
↓
Events
↓
World Update
```

La partie :

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
```

est déjà définie par ACT et traduite concrètement dans ENGINE-006.

La proposition psychologique se concentre donc essentiellement **avant Intent**.

---

# 20. Perception

Un habitant ne dispose jamais automatiquement de l'état complet du World.

Il connaît uniquement ce qu'il peut raisonnablement obtenir par :

- observation ;
- communication ;
- expérience ;
- relation ;
- connaissance transmise ;
- information disponible.

Exemple :

```text
WORLD :
Pierre est ruiné.

Habitant :
Pierre possède encore sa grande maison.

Perception :
Pierre semble riche.
```

Le comportement peut donc être cohérent sans être basé sur la vérité complète.

---

# 21. Attention

Un habitant ne traite pas tout ce qu'il pourrait percevoir.

L'attention sélectionne certains éléments.

Cette sélection peut être influencée par :

- besoins ;
- personnalité ;
- ambitions ;
- habitudes ;
- relations ;
- danger ;
- intérêt actuel.

Même situation :

```text
Une foule
```

peut produire :

```text
Marchand   → remarque les clients potentiels
Garde      → remarque les armes
Voleur     → remarque les objets précieux
Parent     → remarque son enfant
```

---

# 22. Interprétation

L'information perçue n'a pas automatiquement une signification unique.

Exemple :

```text
Une personne ne répond pas.
```

Habitant A :

```text
"Elle ne m'a pas entendu."
```

Habitant B :

```text
"Elle me méprise."
```

Habitant C :

```text
"Elle cache quelque chose."
```

Cette étape permet notamment à la personnalité et aux expériences passées d'avoir une influence réelle.

---

# 23. État émotionnel

GDB-004 ne possède actuellement pas de document consacré spécifiquement aux émotions internes des habitants.

Cette proposition introduit donc ce concept avec prudence.

Une interprétation peut produire ou modifier :

- joie ;
- peur ;
- colère ;
- honte ;
- jalousie ;
- fierté ;
- tristesse ;
- admiration ;
- gratitude.

L'émotion :

- influence la décision ;
- influence l'importance d'un souvenir ;
- peut influencer une relation ;
- ne produit jamais directement une Action.

Elle reste un facteur de décision parmi plusieurs autres.

---

# 24. Mémoire et connaissances

GDB-004G définit déjà les connaissances.

Le modèle proposé distingue cependant deux notions :

## Connaissance

Information considérée comme disponible pour l'habitant.

## Mémoire personnelle

Trace d'une expérience vécue.

Exemple :

```text
Connaissance :
"Cette personne est commerçante."

Mémoire :
"Cette personne m'a aidé lorsque j'étais en difficulté."
```

La mémoire personnelle peut influencer :

- relations ;
- interprétations ;
- confiance ;
- ambitions ;
- décisions futures.

La création d'un système de mémoire dédié devra être vérifiée contre GDB-004G, GDB-004C et GDB-027 afin d'éviter toute duplication documentaire.

---

# 25. Croyances

La réputation définie par GDB-004I démontre déjà un principe important :

> une perception n'est pas une vérité.

Le modèle psychologique généralise ce principe au personnage lui-même.

Une croyance représente :

> une proposition que l'habitant considère suffisamment vraisemblable pour influencer ses décisions.

Elle peut être :

- correcte ;
- fausse ;
- partielle ;
- obsolète ;
- incertaine.

Exemple :

```text
Croyance :
Paul m'a volé.

WORLD :
Paul est innocent.
```

L'habitant peut malgré tout développer :

```text
méfiance
↓
hostilité
↓
Intent
```

---

# 26. Personnalité

GDB-004D reste la référence officielle.

La personnalité doit influencer notamment :

- attention ;
- interprétation ;
- réaction émotionnelle ;
- préférence entre plusieurs décisions.

Elle ne doit pas devenir un ensemble de scripts.

Exemple :

```text
Insulte
```

Personnalité impulsive :

```text
colère
↓
confrontation
```

Personnalité prudente :

```text
colère
↓
évitement
```

Personnalité calculatrice :

```text
mémoire
↓
réponse différée
```

---

# 27. Valeurs

Les valeurs collectives sont déjà couvertes par GDB-009E.

La proposition distingue cependant :

```text
Valeurs de la société
```

et :

```text
adhésion personnelle de l'habitant à ces valeurs.
```

Un individu peut :

- adopter pleinement une valeur culturelle ;
- la suivre partiellement ;
- la rejeter ;
- entrer en conflit avec elle.

Cela permet de conserver GDB-009E comme autorité sur les valeurs sociales tout en laissant le modèle des habitants représenter l'adhésion individuelle.

---

# 28. Besoins

GDB-004B définit déjà les besoins.

Le moteur actuel implémente également un premier `NeedsComponent` ainsi qu'un `NeedsDecaySystem`.

Les besoins constituent donc une entrée déjà concrète de la future prise de décision.

Ils peuvent influencer :

- attention ;
- priorité des Intent ;
- abandon d'un objectif ;
- changement d'habitude.

Exemple :

```text
Ambition :
devenir riche

mais

Faim critique
```

peut temporairement produire :

```text
Intent prioritaire :
chercher de la nourriture
```

---

# 29. Habitudes

GDB-004E définit déjà explicitement les habitudes.

Elles constituent une optimisation naturelle du modèle cognitif.

Une routine connue peut suivre :

```text
Contexte familier
↓
Habitude
↓
Action connue
```

sans nécessiter une planification complexe complète.

Lorsqu'une habitude devient impossible :

```text
Habitude
↓
Échec / contrainte
↓
Nouvel Intent ou réévaluation
```

Cela favorise à la fois :

- crédibilité ;
- performance ;
- émergence lorsque la routine est perturbée.

---

# 30. Ambitions et motivations

GDB-004F constitue déjà la référence officielle sur les ambitions.

Il précise que celles-ci naissent de :

- personnalité ;
- besoins ;
- expériences ;
- culture ;
- opportunités ;
- relations.

Le modèle proposé ne doit donc pas créer un nouveau système redondant de Motivation remplaçant les Ambitions.

La distinction proposée est :

```text
Motivation
= force immédiate ou générale

Ambition
= direction relativement durable de l'existence
```

Exemple :

```text
Motivation :
sécurité

Ambition :
construire une vie stable

Objectif :
acheter un logement
```

Si cette distinction ne produit aucun bénéfice concret lors de la spécification future, le terme `Motivation` devra être supprimé au profit de `Ambition`.

---

# 31. Objectifs

Un objectif traduit une Ambition en état futur identifiable.

Exemple :

```text
Ambition :
réussir professionnellement

↓

Objectif :
obtenir un poste de direction

↓

Intent :
faire progresser ma carrière
```

L'Intent reste ensuite conforme à ACT :

> il exprime ce que l'acteur veut accomplir, jamais comment.

---

# 32. Passage vers ACT

La frontière doit rester stricte.

```text
PSYCHOLOGIE / SIMULATION
↓
produit un Intent
```

Puis :

```text
ACT / ENGINE-006
↓
Planner
↓
Plan
↓
Action Definition
↓
Action Instance
↓
Execution Engine
↓
Outcome
↓
Effects
↓
Events
↓
World Update
```

La psychologie :

- ne crée pas directement d'Action Instance ;
- ne modifie pas directement le World ;
- ne contourne jamais le Planner ;
- ne produit pas directement d'Outcome.

---

# 33. Retour des conséquences

Le retour vers le modèle psychologique ne doit pas utiliser `ENGINE-001` comme mécanisme Publish/Subscribe.

Dans l'architecture actuelle :

> `ENGINE-001` est le journal d'événements du World, destiné à l'observabilité.

Les Systems ne doivent pas réagir directement à `World.Events`.

Ils observent l'état du World au Tick approprié.

Le cycle proposé devient donc :

```text
Action Pipeline
↓
Effects
↓
World Update
↓
État du World
↓
Tick suivant
↓
Systems de perception / cognition
↓
Nouvelle représentation
↓
Nouvel Intent éventuel
```

Les `GameEvent` peuvent néanmoins conserver une trace observable des faits importants.

Ils ne constituent pas le canal de communication cognitive.

---

# 34. Compatibilité avec le Scheduler

Le Scheduler actuel exécute les Systems dans un ordre d'enregistrement déterministe.

La future cognition devra donc prendre la forme de Systems spécialisés ou d'un ensemble équivalent compatible avec ENGINE-003 et ENGINE-004.

Exemple conceptuel futur :

```text
Needs System
↓
Perception System
↓
Cognition System
↓
Intent Generation
↓
Action Pipeline
```

L'ordre exact ne doit pas être fixé dans cette proposition.

Il devra être spécifié avant implémentation conformément à ENGINE-000.

---

# PARTIE III — INTERACTION DES DEUX PROPOSITIONS

# 35. Principe de séparation

Le modèle d'engagement du joueur et le modèle psychologique des habitants ne doivent jamais dépendre directement l'un de l'autre.

Ils se rencontrent uniquement par l'état du World.

```text
                      WORLD
                    /       \
                   /         \
                  ▼           ▼
        EXPÉRIENCE JOUEUR   HABITANTS
```

---

# 36. Exemple combiné

Le joueur acquiert une propriété importante.

## ACT / Simulation

```text
Intent
↓
Plan
↓
Action
↓
Outcome
↓
Effects
↓
World Update
```

---

## Expérience joueur

La nouvelle situation peut produire :

```text
Patrimoine supérieur
↓
Progression perceptible
↓
Nouvelles possibilités

→ louer
→ vendre
→ transmettre
→ investir
```

---

## Habitants

Chaque habitant concerné peut ensuite, selon ce qu'il perçoit, produire une interprétation différente.

Habitant A :

```text
Perçoit la réussite
↓
Admiration
↓
Réputation positive
```

Habitant B :

```text
Perçoit la réussite
↓
Jalousie
↓
Ambition concurrente
```

Habitant C :

```text
Perçoit la nouvelle propriété
↓
Identifie une opportunité économique
↓
Nouvel Intent
```

Un même changement du World produit donc :

- de nouvelles possibilités pour le joueur ;
- de nouveaux comportements chez les habitants.

---

# 37. Boucle émergente complète

```text
JOUEUR / HABITANT
        ↓
      INTENT
        ↓
      PLANNER
        ↓
       PLAN
        ↓
      ACTION
        ↓
     OUTCOME
        ↓
      EFFECTS
        ↓
       WORLD
        ↓
 ┌──────┴────────┐
 ↓               ↓
JOUEUR         HABITANTS
 ↓               ↓
Progression    Perception
 ↓               ↓
Possibilités   Interprétation
 ↓               ↓
Décision       Ambitions / Intent
 └──────┬────────┘
        ↓
      ACT
```

La simulation s'auto-alimente.

---

# 38. Ce que la proposition change réellement

Elle ne demande pas de remplacer :

- CORE ;
- GDB-004 ;
- GDB-006 ;
- ACT ;
- ENGINE ;
- le Kernel ;
- le Scheduler ;
- l'Action Pipeline.

Elle propose principalement de :

## Côté joueur

mieux exploiter :

- GDB-006B — Motivation ;
- GDB-006C — Progression ;
- GDB-006J — Satisfaction ;
- GDB-004I — Réputation ;
- GDB-008 — générations.

## Côté habitants

relier plus précisément :

- besoins ;
- relations ;
- personnalité ;
- habitudes ;
- ambitions ;
- connaissances ;
- réputation ;
- valeurs ;
- perception future ;
- croyances futures ;
- émotions futures.

---

# 39. Nouveaux concepts réellement candidats

Après confrontation avec les documents existants, les concepts véritablement nouveaux ou insuffisamment spécifiés sont principalement :

## Habitants

- Perception individuelle ;
- Attention ;
- Interprétation ;
- État émotionnel ;
- Mémoire personnelle ;
- Croyances individuelles ;
- Objectifs intermédiaires.

## Expérience joueur

Aucun nouveau moteur fondamental n'est nécessaire.

Les principes proposés sont déjà largement compatibles avec GDB-006.

Le travail futur devrait surtout préciser leur application dans les systèmes concrets.

---

# 40. Concepts qu'il ne faut pas dupliquer

La proposition ne doit pas recréer :

- `Personality` → GDB-004D existe ;
- `Habits` → GDB-004E existe ;
- `Ambitions` → GDB-004F existe ;
- `Knowledge` → GDB-004G existe ;
- `Reputation` → GDB-004I existe ;
- `Values` collectives → GDB-009E existe ;
- `Intent / Plan / Action / Outcome` → ACT existe ;
- Action Pipeline → ENGINE-006 existe ;
- EventBus Subscribe/Handler → n'est **pas** l'architecture officielle actuelle.

---

# 41. Risque principal — performance

Le modèle psychologique complet serait coûteux s'il était exécuté intégralement pour chaque habitant à chaque Tick.

La proposition devra donc ultérieurement prévoir plusieurs niveaux de simulation.

Conceptuellement :

```text
Habitant important / proche
↓
Cognition détaillée
```

```text
Habitant distant
↓
Cognition simplifiée
```

```text
Population hors zone active
↓
Simulation agrégée
```

Cette optimisation ne doit toutefois être spécifiée que lorsqu'un besoin mesuré apparaît.

Elle ne doit pas être implémentée prématurément.

---

# 42. Ordre de développement recommandé

L'ordre doit respecter la feuille de route actuelle : d'abord une vie complète, puis la profondeur.

## Étape A — utiliser ce qui existe

Le moteur dispose déjà de :

- Entity ;
- Components ;
- besoins ;
- âge ;
- Lifecycle ;
- Scheduler ;
- Systems ;
- Intent ;
- Planner ;
- Plan ;
- Action Pipeline ;
- Outcome ;
- Persistence.

Ces briques doivent être stabilisées avant d'ajouter la cognition complète.

---

## Étape B — autonomie minimale

Construire une première chaîne :

```text
Besoin
↓
Intent
↓
Planner
↓
Action
↓
Outcome
```

Exemple :

```text
Faim faible
↓
Intent : se nourrir
↓
Plan
↓
Action
```

---

## Étape C — personnalité et ambitions existantes

Connecter progressivement :

- personnalité ;
- habitudes ;
- ambitions.

---

## Étape D — perception et mémoire

Ajouter seulement ensuite :

- perception ;
- mémoire personnelle ;
- information partielle.

---

## Étape E — profondeur psychologique

Ajouter :

- émotion ;
- croyances ;
- valeurs individuelles ;
- interprétation ;
- attention.

---

# 43. Proposition pour l'organisation documentaire

Cette proposition ne doit pas devenir immédiatement un document ENGINE.

Les sujets appartiennent d'abord au Game Design.

La démarche recommandée est :

```text
PROPOSITION
↓
Validation
↓
Analyse de couverture documentaire
↓
Modification / création des GDB nécessaires
↓
Contrats ACT si nécessaire
↓
ENGINE seulement si une infrastructure technique nouvelle est requise
↓
Implémentation
↓
Tests
↓
TECH
```

Cela respecte ENGINE-000 et évite de transformer une idée de gameplay en infrastructure prématurée.

---

# 44. Proposition — engagement joueur

La proposition d'engagement est considérée cohérente avec la documentation actuelle si elle respecte les invariants suivants :

- aucune mécanique de rétention artificielle ;
- aucune obligation de connexion ;
- aucune récompense conçue uniquement pour provoquer une répétition ;
- progression ressentie plutôt que simplement chiffrée ;
- nouvelles possibilités plutôt qu'obsolescence des anciennes ;
- échec susceptible de créer une nouvelle histoire ;
- statut produit par la simulation ;
- progression générationnelle possible.

Elle constitue donc principalement une **extension et une mise en pratique de GDB-006**, pas un nouveau système indépendant.

---

# 45. Proposition — psychologie des habitants

Le modèle psychologique est considéré cohérent avec Chroniques s'il respecte :

- l'autonomie des habitants de GDB-004 ;
- les besoins existants ;
- la personnalité existante ;
- les habitudes existantes ;
- les ambitions existantes ;
- les connaissances existantes ;
- la réputation comme perception, non vérité ;
- les valeurs sociales existantes ;
- ACT comme unique chemin conceptuel de l'Intent à l'Outcome ;
- ENGINE-006 comme traduction du pipeline ACT ;
- le Scheduler comme orchestrateur déterministe ;
- `World.Events` comme journal d'observabilité et non comme bus de réaction entre Systems.

---

# 46. Vision combinée proposée

Le modèle global devient :

```text
                             WORLD
                               │
                               ▼
                      ÉTAT DE SIMULATION
                         /           \
                        /             \
                       ▼               ▼
                 EXPÉRIENCE         HABITANT
                   JOUEUR              │
                     │             Perception
                     │                 ↓
             Progression          Attention
                     │                 ↓
             Possibilités        Interprétation
                     │                 ↓
             Anticipation         Émotion
                     │                 ↓
                 Décision      Mémoire / Connaissance
                     │                 ↓
                     │            Croyances
                     │                 ↓
                     │           Personnalité
                     │                 ↓
                     │             Valeurs
                     │                 ↓
                     │             Besoins
                     │                 ↓
                     │           Ambitions
                     │                 ↓
                     │            Objectifs
                     │                 ↓
                     └──────────────► Intent
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
                                      ↓
                                     World
```

---

# 47. Principe directeur final

La combinaison des deux propositions peut être résumée ainsi :

> **Le joueur doit vouloir découvrir ce que ses choix feront au monde, tandis que les habitants doivent posséder leurs propres raisons de transformer ce même monde.**

Le résultat recherché n'est donc pas :

```text
plus de récompenses
```

ni simplement :

```text
plus d'IA
```

mais :

```text
davantage de conséquences significatives
+
davantage d'acteurs capables d'en créer
+
davantage de possibilités qui en émergent
```

---

# 48. Décision proposée

Avant toute implémentation supplémentaire :

1. conserver le présent document au statut **Proposition** ;
2. ne créer aucun `EngagementEngine` ;
3. ne recréer aucun EventBus Publish/Subscribe ;
4. considérer GDB-006 comme l'autorité principale sur l'engagement joueur ;
5. considérer GDB-004 comme l'autorité principale sur la psychologie et l'autonomie des habitants ;
6. identifier précisément les lacunes documentaires de GDB-004 concernant Perception, Attention, Interprétation, Émotions, Mémoire personnelle et Croyances ;
7. compléter ensuite les spécifications avant toute implémentation, conformément à ENGINE-000.

---

# Historique

## Version 2.0

- remplacement du terme `Audit` par `Proposition` ;
- mise à jour à partir de l'état réel des dépôts `CHRONIQUES` et `CHRONIQUES-ENGINE` ;
- alignement du modèle d'engagement sur GDB-006B, GDB-006C et GDB-006J ;
- suppression de l'idée d'un `EngagementEngine` dédié ;
- alignement du modèle psychologique sur GDB-004B à GDB-004J ;
- reconnaissance de la personnalité, des habitudes, des ambitions, des connaissances et de la réputation comme concepts déjà spécifiés ;
- clarification de la frontière entre valeurs sociales (GDB-009E) et adhésion individuelle ;
- alignement du pipeline sur ACT-002 et ENGINE-006 réellement présents ;
- remplacement du modèle simplifié `Intent → Plan → Action → Outcome` par l'architecture actuelle `Intent → Planner → Plan → Action Instance → Execution Engine → Outcome → Effects → Events → World Update` ;
- correction du rôle d'ENGINE-001 : journal d'événements du World, et non bus Publish/Subscribe ;
- suppression de toute dépendance cognitive directe envers `World.Events` ;
- alignement sur le Scheduler et les Systems réellement implémentés ;
- prise en compte des composants et systèmes déjà présents dans `CHRONIQUES-ENGINE` ;
- proposition d'une progression d'implémentation compatible avec l'état réel du moteur.
