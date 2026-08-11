# GDB-004B --- Les Besoins des Habitants

> Version : 1.2
> Statut : Officiel
> Type : Population du Monde
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes qui gouvernent les besoins des habitants de Chroniques et préciser leur rôle minimal dans la production de décisions autonomes.

Les besoins constituent l'un des moteurs principaux de leurs décisions et de leurs interactions.

---

# PRINCIPE

Chaque habitant agit pour satisfaire des besoins.

Ces besoins évoluent avec le temps, le contexte et son histoire.

Un besoin ne déclenche cependant jamais directement une mutation du monde : il peut contribuer à produire un objectif, exprimé sous forme d'Intent conformément à ACT, puis cet Intent doit traverser le pipeline normal d'Actions.

```text
Besoin
↓
évaluation
↓
Intent éventuel
↓
ACT
↓
Action
↓
Outcome
↓
World
```

---

# CATÉGORIES DE BESOINS

Les besoins peuvent concerner notamment :

- la nourriture ;
- le logement ;
- la sécurité ;
- les relations ;
- le travail ;
- l'apprentissage ;
- le repos ;
- les loisirs ;
- la transmission.

Toutes ces catégories n'ont pas à être implémentées simultanément.

Une implémentation progressive peut ne représenter qu'un sous-ensemble des besoins tant que les catégories absentes ne sont ni simulées artificiellement ni considérées à tort comme satisfaites.

---

# SATISFACTION D'UN BESOIN

Lorsqu'un besoin est représenté numériquement, sa valeur exprime son niveau de satisfaction :

```text
0
=
état critique / non satisfait

100
=
pleinement satisfait
```

La valeur reste bornée entre `0` et `100`.

Une valeur basse signifie donc qu'une réponse devient plus urgente ; une valeur haute signifie que le besoin ne justifie pas, à lui seul, une nouvelle Action.

Cette convention correspond au modèle déjà employé par les besoins fondamentaux de Chroniques et constitue leur contrat GDB.

---

# SEUIL D'ACTIVATION

Un besoin ne devient candidat à une décision autonome que si sa satisfaction passe strictement sous un seuil d'activation propre à ce besoin ou à sa politique de décision.

```text
satisfaction < seuil
→ besoin candidat

satisfaction >= seuil
→ pas d'Intent produit par ce besoin seul
```

Le cas d'égalité appartient explicitement au second cas.

Les valeurs numériques exactes des seuils ne sont pas fixées par la GDB.

Elles constituent des paramètres d'équilibrage.

Un seuil doit rester déterministe et stable pour une même configuration de simulation.

---

# BESOIN ACTIONNABLE

Un besoin sous son seuil n'est réellement actionnable que si le contexte permet au moteur de construire au moins une réponse exécutable susceptible de contribuer à le satisfaire.

Invariant :

```text
besoin urgent
+
aucune réponse exécutable disponible
≠
création d'un faux Intent
```

Un besoin sans mapping ou sans moyen d'exécuter son mapping reste un état réel de l'habitant, mais il ne doit pas pousser le moteur à inventer une Action, un Verbe, une Cible ou une ressource absente.

Il ne doit pas non plus bloquer l'évaluation des autres besoins disposant, eux, d'une réponse réellement exécutable.

---

# URGENCE DE BASE

Lorsque plusieurs besoins actionnables sont simultanément candidats, leur urgence de base suit leur niveau de satisfaction :

```text
satisfaction plus basse
→ urgence de base plus forte
```

Autrement dit, à paramètres comparables, l'habitant traite d'abord le besoin le moins satisfait parmi ceux qu'il sait actuellement adresser.

La GDB ne fixe pas une formule arithmétique unique de score. Elle fixe l'ordre monotone : diminuer la satisfaction d'un besoin ne peut jamais diminuer son urgence de base.

---

# ÉGALITÉS

Deux besoins peuvent présenter la même urgence de base.

Une égalité ne doit jamais être départagée par un hasard non déterministe.

Le système ou les données de décision doivent disposer d'un ordre stable et explicite des règles candidates.

```text
mêmes besoins
+
mêmes valeurs
+
même configuration
→ même besoin choisi
```

Cet ordre technique ne constitue pas nécessairement une hiérarchie morale ou narrative universelle entre les besoins.

---

# PRIORITÉS

Tous les besoins n'ont pas la même importance dans toutes les situations.

Le modèle minimal définit d'abord l'urgence de base par la satisfaction courante.

Des modificateurs futurs pourront faire évoluer cette priorité selon :

- l'âge ;
- la profession ;
- la famille ;
- les saisons ;
- les conséquences du monde ;
- la personnalité [réf: GDB-004D] ;
- les habitudes [réf: GDB-004E] ;
- les ambitions [réf: GDB-004F].

Ces modificateurs ne doivent pas être implémentés avant que leur propre règle d'influence soit suffisamment spécifiée.

L'existence conceptuelle d'une influence ne constitue pas à elle seule une formule de pondération.

---

# CONTRAT AUTONOME 1 — REPOS

Le premier cas autonome validé est :

```text
Besoin : repos / fatigue
↓
satisfaction de Fatigue strictement sous le seuil configuré
↓
Intent : se_reposer
```

Si la satisfaction de Fatigue est supérieure ou égale au seuil configuré :

```text
aucun nouvel Intent de repos
```

La capacité ACT correspondante est `VERB-001 — Se reposer`.

---

# CONTRAT AUTONOME 2 — NOURRITURE

Le second besoin rendu spécifiable est la nourriture.

Dans la représentation actuelle :

```text
Besoin : nourriture
→ Faim

0
→ critique

100
→ pleinement satisfait
```

La réponse autonome minimale est :

```text
Faim < seuil configuré
+
au moins un produit alimentaire accessible et consommable
↓
Intent : manger
```

Le produit alimentaire et son accessibilité sont définis par GDB-005E [réf: GDB-005E].

Si aucun produit alimentaire accessible n'est disponible :

```text
Faim < seuil
+
aucune nourriture accessible
↓
pas d'Intent manger produit par ce besoin
```

Cette absence ne signifie jamais que le besoin est satisfait.

Elle signifie seulement qu'aucune réponse exécutable n'est actuellement disponible.

L'Intent exprime uniquement l'objectif `manger`. Il ne porte pas lui-même la Cible concrète : la sélection d'une Cible alimentaire appartient au Plan et à l'Action conformément à ACT.

---

# EFFET DE L'ALIMENTATION

Une Action alimentaire résolue avec succès peut augmenter la satisfaction de Faim.

La quantité de restauration n'est pas universelle : elle dépend du produit ou des données d'équilibrage applicables [réf: GDB-005E].

La décision autonome ne modifie jamais directement `Faim`.

```text
Intent manger
↓
ACT
↓
Action résolue avec succès
↓
consommation du produit
+
Faim ↑
```

---

# FRONTIÈRE AVEC LA PERSONNALITÉ

GDB-004D affirme que la personnalité influence les décisions et les priorités.

Cette influence reste réelle, mais son poids exact n'est pas encore défini sous une forme suffisamment précise pour modifier l'arbitrage autonome minimal.

La politique minimale de besoins doit donc fonctionner sans personnalité plutôt que d'inventer des coefficients de traits.

---

# FRONTIÈRE AVEC LES HABITUDES

GDB-004E affirme que les habitudes rendent les comportements cohérents et influencent les routines.

Une habitude pourra ultérieurement favoriser certains Intents ou certains contextes, mais aucune pondération n'est définie à ce stade.

---

# FRONTIÈRE AVEC LES AMBITIONS

GDB-004F affirme que les ambitions donnent une direction durable à la vie des habitants.

Les ambitions ne remplacent pas les besoins et ne sont pas requises pour satisfaire un besoin physiologique minimal.

Leur arbitrage avec les besoins devra être spécifié avant toute implémentation d'une politique multi-objectifs enrichie.

---

# FRONTIÈRE AVEC LES OPPORTUNITÉS

GDB-002E définit actuellement les Opportunités comme des possibilités offertes au joueur.

Elles ne constituent donc pas, dans leur forme documentaire actuelle, une entrée normative de la politique autonome minimale des habitants.

---

# ÉVOLUTION

Les besoins changent avec :

- l'âge ;
- la profession ;
- la famille ;
- les saisons ;
- les conséquences du monde.

Leur satisfaction peut être modifiée par les Systems compétents et par les Effects d'Actions validées.

La couche de décision ne doit jamais devenir une seconde source de vérité pour cette évolution.

---

# IMPACT SUR LE MONDE

Les besoins influencent :

- l'économie ;
- les métiers ;
- les échanges ;
- les déplacements ;
- les relations sociales.

Ils participent à faire vivre le monde sans intervention du joueur.

Cette influence doit passer par les Actions et Systems responsables, jamais par une mutation directe effectuée par la politique de décision.

Le besoin de nourriture crée notamment un lien explicite avec les produits alimentaires et leur consommation [réf: GDB-005E].

---

# INVARIANTS

- Un besoin ne modifie jamais directement le World.
- Une décision autonome produit au maximum un Intent avant de passer par ACT.
- Un besoin sans réponse exécutable ne génère aucun faux Intent.
- Le seuil d'activation est strict : égal au seuil signifie non activé.
- Une satisfaction plus faible ne peut pas produire une urgence de base plus faible.
- Les égalités utilisent un ordre stable, jamais un hasard non déterministe.
- `se_reposer` ne nécessite aucune ressource alimentaire.
- `manger` nécessite qu'au moins un produit alimentaire accessible permette réellement l'exécution.
- L'Intent `manger` ne transporte pas la Cible alimentaire concrète.
- Une Action alimentaire réussie consomme ou réduit la disponibilité du produit utilisé [réf: GDB-005E].
- Personnalité, Habitudes et Ambitions ne reçoivent aucun coefficient implicite avant spécification.
- Les Opportunités joueur de GDB-002E ne sont pas réutilisées silencieusement comme Opportunités PNJ.

---

# RÈGLES DE CONCEPTION

Toute mécanique liée aux besoins devra :

1. rester crédible ;
2. évoluer naturellement ;
3. influencer plusieurs systèmes ;
4. éviter les comportements artificiels ;
5. renforcer les histoires émergentes ;
6. produire des décisions reproductibles à état et configuration identiques ;
7. ne jamais inventer une Action, une Cible ou une ressource absente des contrats disponibles.

---

# CRITÈRE DE VALIDATION

Le système permet-il à un habitant de transformer un besoin réellement insatisfait en objectif autonome cohérent, reproductible et réellement exécutable dans son contexte, sans contourner ACT ni créer gratuitement les ressources nécessaires ?

Si la réponse est non, il devra être repensé.

---

# HISTORIQUE

## Version 1.2

- ajout du second contrat autonome `Faim → manger` ;
- exigence d'un produit alimentaire accessible et consommable [réf: GDB-005E] ;
- interdiction explicite de produire `manger` lorsqu'aucune nourriture accessible n'existe ;
- clarification que l'Intent ne porte pas la Cible alimentaire ;
- liaison entre Action alimentaire réussie, consommation du produit et restauration de Faim ;
- conservation de l'arbitrage déterministe entre besoins actionnables.

## Version 1.1

- passage en Maturité 2 ;
- formalisation de la satisfaction des besoins sur une échelle `0..100` ;
- ajout du seuil d'activation strict ;
- définition d'un besoin actionnable et interdiction des faux Intents ;
- définition de l'urgence de base monotone et du départage déterministe des égalités ;
- clarification des frontières avec Personnalité, Habitudes, Ambitions et Opportunités ;
- définition du premier contrat autonome implémentable `Fatigue → se_reposer` ;
- ajout des invariants de décision autonome nécessaires à la Phase 3 de MASTER-005.

## Version 1.0

- création du document.

---

Fin du document
