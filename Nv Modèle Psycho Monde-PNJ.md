# AUDIT — Engagement joueur et modèle psychologique des PNJ

> Version : 1.0  
> Statut : Proposition  
> Type : Audit de conception  
> Domaine : Game Design / Simulation / Comportement / Engagement  
> Projet : Chroniques

---

# 1. Objet du document

Ce document analyse deux évolutions complémentaires de Chroniques :

1. un modèle d'engagement du joueur inspiré des boucles de progression observées dans certains jeux Roblox ;
2. un modèle psychologique permettant aux PNJ de percevoir, interpréter et réagir au monde selon leur propre histoire.

Ces deux modèles ne doivent pas être confondus.

Le premier répond à la question :

> Pourquoi le joueur a-t-il envie de poursuivre son histoire ?

Le second répond à la question :

> Pourquoi un PNJ décide-t-il d'agir d'une certaine manière ?

Ils utilisent néanmoins le même World, les mêmes événements et les mêmes conséquences de simulation.

---

# PARTIE I — MODÈLE D'ENGAGEMENT JOUEUR

# 2. Inspiration du modèle Roblox

Le modèle observé repose principalement sur une boucle :

```text
Action
↓
Récompense
↓
Progression visible
↓
Statut / reconnaissance
↓
Nouvel objectif
↓
Nouvelle action
```

Sa puissance ne provient pas uniquement du hasard.

Elle repose surtout sur :

- un feedback fréquent ;
- une progression compréhensible ;
- l'anticipation ;
- le statut ;
- la comparaison ;
- l'escalade des objectifs ;
- la présence permanente d'une prochaine possibilité.

Chroniques peut exploiter ces principes sans reprendre les mécanismes de gambling.

---

# 3. Ce que Chroniques ne doit pas reproduire

Le projet ne doit pas être construit autour de :

- lootboxes ;
- probabilités volontairement opaques ;
- quasi-victoires artificielles ;
- frustrations destinées à pousser à l'achat ;
- fausse rareté ;
- pay-to-win ;
- pression temporelle artificielle ;
- récompenses quotidiennes obligatoires ;
- inflation infinie des nombres.

L'objectif est :

> reprendre la boucle d'engagement, pas les mécanismes prédateurs.

---

# 4. Transposition dans Chroniques

Le modèle :

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
Le monde réagit
↓
Ma situation évolue
↓
Une nouvelle possibilité apparaît
↓
Je veux découvrir ce qu'elle produira
```

La récompense fondamentale de Chroniques devient donc :

> une nouvelle possibilité significative dans la simulation.

---

# 5. Boucle d'engagement cible

```text
Découverte
↓
Décision
↓
Action
↓
Conséquence
↓
Réaction du monde
↓
Progression perceptible
↓
Nouvelle possibilité
↓
Anticipation
↓
Nouvelle décision
```

L'engagement repose moins sur :

```text
Quelle sera ma prochaine récompense ?
```

que sur :

```text
Quelle sera la prochaine conséquence de mon histoire ?
```

---

# 6. Boucles temporelles

Chroniques doit pouvoir maintenir plusieurs boucles simultanément.

## Boucle courte

Quelques secondes à quelques minutes.

Exemple :

```text
Chercher un emploi
↓
Postuler
↓
Être accepté
↓
Premier salaire
```

---

## Boucle moyenne

Plusieurs dizaines de minutes ou sessions.

```text
Premier emploi
↓
Compétence
↓
Promotion
↓
Meilleur revenu
↓
Nouveau logement
```

---

## Boucle longue

Une vie ou plusieurs générations.

```text
Départ sans patrimoine
↓
Carrière
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

---

# 7. Progression perceptible

La simulation peut produire énormément de changements sans que le joueur les perçoive clairement.

Chroniques doit donc traduire certains états complexes en informations lisibles.

Exemples :

## Situation économique

```text
Précaire
↓
Stable
↓
Aisé
↓
Fortuné
↓
Grande fortune
```

## Influence

```text
Inconnu
↓
Connu
↓
Respecté
↓
Influent
↓
Figure majeure
```

## Patrimoine

```text
Aucun patrimoine
↓
Premier logement
↓
Propriétaire
↓
Entreprise
↓
Patrimoine familial
↓
Dynastie
```

Ces catégories doivent rester des interprétations de la simulation et non devenir nécessairement des niveaux artificiels.

---

# 8. La prochaine possibilité

Un principe particulièrement important est :

> le joueur doit comprendre sa situation actuelle et entrevoir plusieurs évolutions possibles.

Exemple :

```text
Situation actuelle

Employé
Revenu stable
Petit logement
Relation stable
```

Le monde permet désormais :

```text
→ demander une promotion
→ changer de métier
→ acheter un logement
→ entreprendre
→ fonder une famille
```

Ce ne sont pas nécessairement des quêtes.

Ce sont des possibilités produites par l'état du monde.

---

# 9. Récompense systémique

Chroniques doit favoriser les récompenses qui ouvrent d'autres systèmes.

Exemple :

```text
Premier salaire
↓
Accès économique
├── logement
├── épargne
├── consommation
├── investissement
└── crédit
```

Une réussite ne donne donc pas seulement une récompense.

Elle élargit l'espace décisionnel.

---

# 10. Statut social

Le statut peut devenir une forme majeure de progression.

Mais contrairement à un jeu où le statut est seulement affiché, Chroniques peut le rendre fonctionnel.

```text
Richesse
↓
Perception sociale
↓
Réputation
↓
Réactions différentes
↓
Nouvelles relations
↓
Nouvelles opportunités
```

Exemple :

Un personnage devenu riche peut attirer :

- admiration ;
- jalousie ;
- demandes d'aide ;
- propositions commerciales ;
- alliances ;
- tentatives de manipulation ;
- criminalité.

Le statut devient une propriété du monde.

---

# 11. Méta-progression générationnelle

La mort ne constitue pas obligatoirement un reset.

```text
Vie 1
↓
Conséquences
↓
Transmission
↓
Vie 2
↓
Nouvelles conséquences
↓
Transmission
↓
Vie 3
```

Une lignée peut transmettre :

- patrimoine ;
- réputation familiale ;
- relations ;
- ennemis ;
- histoire ;
- influence ;
- croyances ;
- traditions ;
- conséquences politiques ou économiques.

La lignée devient la progression longue durée de Chroniques.

---

# 12. Incertitude

Le RNG artificiel n'est pas indispensable pour provoquer de l'anticipation.

Chroniques possède quelque chose de plus intéressant :

> l'incertitude systémique.

Exemple :

```text
Créer une entreprise
```

peut conduire à :

```text
croissance
faillite
association
dette
innovation
trahison
fortune
influence politique
```

Le joueur sait ce qu'il tente.

Il ne sait pas exactement comment le monde va réagir.

---

# 13. Échec comme contenu

L'échec ne doit pas signifier :

```text
pas de récompense
```

mais :

```text
nouvelle situation
```

Exemple :

```text
Entreprise
↓
Faillite
↓
Dette
↓
Conflit familial
↓
Déménagement
↓
Nouvelle carrière
```

L'échec peut générer davantage d'histoire qu'un succès.

---

# 14. Progression horizontale

Toutes les trajectoires ne doivent pas être comparables par une valeur unique.

```text
Entrepreneur
Politicien
Médecin
Criminel
Artiste
Parent
Militaire
Scientifique
Ermite
```

Une nouvelle trajectoire constitue elle-même une forme de récompense.

Cela protège Chroniques contre une progression exclusivement verticale.

---

# 15. Modèle final d'engagement

```text
ACTION SIGNIFICATIVE
        ↓
CONSÉQUENCE
        ↓
RÉACTION DU MONDE
        ↓
PROGRESSION PERCEPTIBLE
        ↓
NOUVELLE POSSIBILITÉ
        ↓
ANTICIPATION
        ↓
NOUVELLE DÉCISION
        ↓
ACTION SIGNIFICATIVE
```

L'engagement doit émerger de la simulation.

Il ne doit pas nécessiter un moteur artificiel chargé de rendre le jeu "addictif".

---

# PARTIE II — MODÈLE PSYCHOLOGIQUE DES PNJ

# 16. Objectif

Le modèle psychologique des PNJ vise à empêcher le comportement suivant :

```text
État du monde
↓
Règle
↓
Action
```

Un personnage ne doit pas simplement agir selon l'état objectif du World.

Il doit agir selon :

> sa représentation du monde.

Cela permet à deux personnages confrontés à la même situation de produire des comportements différents.

---

# 17. Modèle psychologique cible

La chaîne conceptuelle proposée est :

```text
Perception
↓
Attention
↓
Interprétation
↓
Émotion
↓
Mémoire
↓
Croyances
↓
Valeurs
↓
Personnalité
↓
Motivations
↓
Objectifs
↓
Intent
↓
Plan
↓
Action
↓
Outcome
↓
Nouvelle perception / mémoire
```

ACT commence réellement au niveau de :

```text
Intent
↓
Plan
↓
Action
↓
Outcome
```

La psychologie se situe principalement en amont.

---

# 18. Perception

Un PNJ ne connaît pas automatiquement l'état du World.

Il ne perçoit que :

- ce qu'il voit ;
- ce qu'il entend ;
- ce qu'on lui raconte ;
- ce qu'il peut raisonnablement détecter.

Exemple :

```text
World réel :
Pierre est ruiné.

PNJ :
Pierre possède toujours une grande maison.

Perception :
Pierre semble riche.
```

Le PNJ peut donc agir sur une information incorrecte.

---

# 19. Attention

Tout ce qui est perceptible n'est pas nécessairement traité.

L'attention sélectionne ce qui est pertinent pour le personnage.

Elle peut dépendre de :

- besoins ;
- peur ;
- intérêts ;
- personnalité ;
- objectifs ;
- relations.

Exemple :

Dans une même pièce :

```text
un marchand remarque les vêtements coûteux ;
un garde remarque l'arme ;
un amoureux remarque le comportement ;
un voleur remarque la montre.
```

Même scène.

Attention différente.

---

# 20. Interprétation

La perception brute doit être interprétée.

Exemple :

```text
Une personne ne répond pas à un salut.
```

Interprétation A :

```text
Elle ne m'a probablement pas entendu.
```

Interprétation B :

```text
Elle me méprise.
```

Interprétation C :

```text
Elle cache quelque chose.
```

L'interprétation dépend du personnage.

---

# 21. Émotions

L'interprétation produit des états émotionnels.

Exemples :

- joie ;
- peur ;
- colère ;
- honte ;
- jalousie ;
- fierté ;
- tristesse ;
- admiration ;
- gratitude.

Les émotions influencent ensuite :

- l'attention ;
- les décisions ;
- la mémoire ;
- les relations.

Elles ne doivent pas déterminer directement une Action.

---

# 22. Mémoire

Le PNJ conserve certaines expériences.

```text
Événement
↓
Interprétation
↓
Importance
↓
Mémoire
```

Toutes les expériences ne doivent pas nécessairement devenir des souvenirs durables.

La mémoire peut notamment contenir :

- événement ;
- personnes impliquées ;
- contexte ;
- émotion ;
- importance ;
- interprétation.

---

# 23. Croyances

Une distinction fondamentale doit exister entre :

```text
ce qui est vrai dans le World
```

et :

```text
ce que le PNJ croit vrai.
```

Une croyance peut être :

- vraie ;
- fausse ;
- partielle ;
- obsolète ;
- incertaine.

Exemple :

```text
Croyance :
Paul a volé mon argent.

Réalité :
Paul est innocent.
```

Le PNJ peut néanmoins :

```text
détester Paul
↓
refuser de l'aider
↓
chercher vengeance
```

Le monde obtient ainsi de véritables malentendus.

---

# 24. Valeurs

Les PNJ ne doivent pas uniquement maximiser leur intérêt personnel.

Ils peuvent accorder différentes importances à :

- famille ;
- argent ;
- liberté ;
- religion ;
- loyauté ;
- honneur ;
- pouvoir ;
- justice ;
- sécurité ;
- tradition.

Les valeurs permettent notamment de résoudre les conflits de motivation.

---

# 25. Personnalité

La personnalité modifie la manière dont les informations sont interprétées et transformées en décisions.

Exemple :

```text
Situation :
un inconnu insulte le personnage.
```

Personnage agressif :

```text
colère
↓
confrontation
```

Personnage prudent :

```text
colère
↓
évitement
```

Personnage manipulateur :

```text
colère
↓
mémorisation
↓
vengeance différée
```

Même stimulus.

Comportements différents.

---

# 26. Motivations

Une Motivation représente une force relativement durable.

Exemples :

- survivre ;
- protéger sa famille ;
- devenir riche ;
- appartenir à un groupe ;
- être respecté ;
- obtenir du pouvoir ;
- découvrir ;
- aimer ;
- se venger.

Les Motivations ne sont pas des Actions.

Elles génèrent des objectifs.

---

# 27. Objectifs

Un objectif représente un état futur désiré.

Exemple :

```text
Motivation :
sécurité familiale
```

produit :

```text
Objectif :
acheter une maison
```

qui peut produire :

```text
Intent :
augmenter mes revenus
```

puis :

```text
Plan :
chercher un meilleur emploi
```

---

# 28. Habitudes

Tous les comportements ne doivent pas utiliser la chaîne cognitive complète.

Une action répétée peut devenir une habitude :

```text
Stimulus
↓
Routine
```

Exemple :

```text
Matin
↓
aller travailler
```

Cela permet :

- des comportements crédibles ;
- une réduction importante du coût de simulation ;
- des routines facilement perturbables par les événements.

Lorsqu'une habitude échoue :

```text
Routine impossible
↓
Cognition complète
```

Le personnage cherche alors une nouvelle solution.

---

# 29. Interaction avec ACT

Le modèle psychologique ne remplace pas ACT.

Il alimente ACT.

```text
Psychologie
↓
Intent

ACT
↓
Plan
↓
Action
↓
Outcome
```

Puis l'Outcome revient dans le système cognitif :

```text
Outcome
↓
Perception
↓
Mémoire
↓
Nouvelle décision
```

La boucle devient :

```text
MONDE
↓
PERCEPTION
↓
PSYCHOLOGIE
↓
INTENT
↓
ACT
↓
OUTCOME
↓
MONDE
```

---

# 30. Exemple complet

Situation :

```text
Le joueur obtient une promotion.
```

PNJ A :

```text
Perception
↓
"Il gagne désormais davantage."

Valeur dominante :
réussite

Personnalité :
ambitieuse

Émotion :
admiration + jalousie

Motivation :
statut

Objectif :
obtenir une promotion

Intent :
améliorer ma carrière
```

PNJ B :

```text
Même événement

Valeur dominante :
famille

Personnalité :
peu compétitive

Émotion :
neutre

Résultat :
aucun nouvel Intent majeur
```

PNJ C :

```text
Même événement

Relation avec le joueur :
rivalité

Interprétation :
"Il va devenir plus puissant que moi."

Émotion :
peur + jalousie

Objectif :
affaiblir le joueur

Intent :
nuire à sa réputation
```

Un seul événement produit trois histoires différentes.

---

# PARTIE III — INTERACTION DES DEUX MODÈLES

# 31. Point de connexion

Le modèle joueur et le modèle PNJ ne doivent pas communiquer directement.

Ils se rencontrent dans le World.

```text
JOUEUR
↓
Action
↓
Outcome
↓
WORLD
↓
Event
```

Puis deux traitements indépendants peuvent exister :

```text
                    WORLD EVENT
                    /         \
                   /           \
                  ▼             ▼
        Engagement joueur    Perception PNJ
                ↓                 ↓
        Progression visible     Psychologie
                ↓                 ↓
        Opportunités           Intent PNJ
```

Cette séparation est fondamentale.

---

# 32. Exemple combiné

Le joueur achète une propriété prestigieuse.

## Simulation

```text
Action
↓
Achat
↓
Outcome
↓
World modifié
```

## Engagement joueur

```text
Nouvelle propriété
↓
Patrimoine augmenté
↓
Nouveau statut perceptible
↓
Possibilités :
- louer
- revendre
- agrandir
- transmettre
```

## PNJ

PNJ A :

```text
admiration
↓
relation positive
```

PNJ B :

```text
jalousie
↓
rivalité
```

PNJ C :

```text
opportunité commerciale
↓
proposition au joueur
```

La même conséquence nourrit donc simultanément :

- l'engagement joueur ;
- la simulation sociale.

---

# 33. Effet recherché

Ces deux modèles combinés permettent de créer une boucle particulièrement puissante :

```text
LE JOUEUR AGIT
        ↓
LE MONDE CHANGE
        ↓
LES PNJ LE PERÇOIVENT
        ↓
LES PNJ RÉAGISSENT
        ↓
LE MONDE CHANGE DAVANTAGE
        ↓
LE JOUEUR DÉCOUVRE DE NOUVELLES POSSIBILITÉS
        ↓
LE JOUEUR AGIT
```

La boucle d'engagement n'est donc plus seulement alimentée par les propres actions du joueur.

Elle est également alimentée par les conséquences autonomes produites par les PNJ.

---

# 34. Conséquence architecturale majeure

Chroniques peut alors éviter un système traditionnel :

```text
Quête
↓
Récompense
↓
Nouvelle quête
```

et tendre vers :

```text
Décision
↓
Conséquence
↓
Réaction
↓
Nouvelle situation
↓
Nouvelle décision
```

Le contenu n'est plus seulement consommé.

Il est produit par la simulation.

---

# 35. Risque principal

Le risque majeur n'est pas conceptuel.

Il est computationnel.

Avec plusieurs milliers de PNJ, il serait trop coûteux d'exécuter en permanence :

```text
Perception
Attention
Interprétation
Émotion
Mémoire
Croyances
Motivations
Objectifs
Planning
```

pour chaque personnage à chaque Tick.

Le modèle devra donc respecter le principe de simulation à plusieurs niveaux.

Exemple :

```text
PNJ proche / important
→ cognition détaillée

PNJ éloigné
→ cognition simplifiée

PNJ dormant
→ simulation agrégée
```

La richesse psychologique doit être compatible avec l'échelle du monde.

---

# 36. Ordre d'implémentation recommandé

Ne pas construire toute la psychologie simultanément.

## Phase 1

```text
Perception
↓
Besoin
↓
Intent
↓
ACT
```

Permet déjà des PNJ autonomes simples.

---

## Phase 2

Ajouter :

```text
Mémoire
Personnalité
Émotions
```

---

## Phase 3

Ajouter :

```text
Croyances
Valeurs
Motivations
```

---

## Phase 4

Ajouter :

```text
Objectifs long terme
Habitudes
Interprétation avancée
Attention
```

---

## Phase 5

Optimisation multi-échelle.

```text
Cognition complète
Cognition simplifiée
Simulation agrégée
```

---

# 37. Verdict — modèle d'engagement joueur

**Compatibilité avec Chroniques : très élevée.**

Le modèle Roblox doit être utilisé comme inspiration structurelle :

```text
progression
+
anticipation
+
statut
+
nouvelle possibilité
```

et non comme modèle économique ou de gambling.

La meilleure adaptation est :

> remplacer l'attente de la prochaine récompense par l'attente de la prochaine conséquence.

---

# 38. Verdict — modèle psychologique PNJ

**Compatibilité avec Chroniques : très élevée.**

Ce modèle transforme les PNJ :

```text
de systèmes réactifs
```

en :

```text
agents possédant leur propre représentation du monde.
```

La distinction entre :

```text
World réel
```

et :

```text
World perçu
```

est particulièrement importante.

Elle permet :

- malentendus ;
- rumeurs ;
- erreurs ;
- jalousie ;
- confiance ;
- manipulation ;
- évolution des relations ;
- comportements réellement différents.

---

# 39. Vision combinée

Le modèle global de Chroniques devient :

```text
                     WORLD
                       │
                       ▼
                    EVENTS
                  /          \
                 /            \
                ▼              ▼
          JOUEUR             PNJ
             │                │
             │          PERCEPTION
             │                ↓
             │          INTERPRÉTATION
             │                ↓
             │           PSYCHOLOGIE
             │                ↓
             │              INTENT
             │                ↓
             └──────────────► ACT
                              ↓
                             PLAN
                              ↓
                            ACTION
                              ↓
                           OUTCOME
                              ↓
                            WORLD
```

Autour du joueur :

```text
WORLD
↓
CONSÉQUENCES
↓
PROGRESSION PERCEPTIBLE
↓
OPPORTUNITÉS
↓
ANTICIPATION
↓
DÉCISION
```

Les deux boucles s'auto-alimentent.

---

# 40. Principe directeur

La synthèse des deux modèles peut être formulée ainsi :

> **Le joueur doit avoir envie de découvrir ce que le monde fera ensuite, tandis que les PNJ doivent avoir leurs propres raisons de provoquer ce qui arrivera ensuite.**

C'est probablement la meilleure articulation entre :

- simulation ;
- narration émergente ;
- IA comportementale ;
- engagement ;
- rejouabilité.

---

# Historique

## Version 1.0

- audit du modèle d'engagement inspiré de Roblox ;
- exclusion explicite des mécanismes de gambling ;
- adaptation du modèle à la progression systémique de Chroniques ;
- définition du modèle psychologique des PNJ ;
- introduction de Perception, Attention, Interprétation, Émotion, Mémoire, Croyances, Valeurs, Personnalité, Motivations et Objectifs ;
- articulation avec ACT ;
- définition de la relation entre engagement joueur et cognition PNJ ;
- identification des risques de performance ;
- proposition d'une implémentation progressive et multi-échelle.
