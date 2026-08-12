GDB-004F --- Les Ambitions

Version : 1.1
Statut : Officiel
Type : Population du Monde
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir les principes qui gouvernent les ambitions des habitants de
Chroniques, avec une précision suffisante pour être implémentées sans
interprétation (MASTER-007, Maturité 2).

Les ambitions donnent une direction de vie durable aux habitants et
expliquent une grande partie de leurs décisions à long terme.
⸻
PRINCIPE

Chaque habitant poursuit des ambitions qui lui sont propres.

Elles peuvent être modestes ou très importantes.

Aucune ambition n'est universelle.
⸻
DÉFINITION

Une Ambition est une direction de vie relativement durable : un état
futur désiré que l'habitant cherche à atteindre sur plusieurs Ticks,
voire plusieurs générations. Elle ne décrit pas un comportement
contextuel immédiat (c'est le rôle des Habitudes, GDB-004E) ni un
besoin urgent (GDB-004B), mais une aspiration qui oriente les décisions
lorsque les besoins urgents et les Habitudes ne dictent pas de réponse
immédiate.

FRONTIÈRE AVEC GDB-004E (HABITUDES) : une Habitude est un comportement
acquis par répétition, contextuel et à déclencheur immédiat. Une Ambition
est une aspiration durable, sans déclencheur contextuel strict. Une
Habitude peut avoir été formée en réponse à une Ambition, mais elle ne
la représente pas. GDB-004E reste l'autorité sur les comportements
routiniers ; ce document sur les directions de vie.

FRONTIÈRE AVEC GDB-004B (BESOINS) : un Besoin est un état courant qui
déclenche un Intent urgent lorsqu'il est sous-satisfait. Une Ambition
est un désir de progression qui génère des Intents même lorsque les
besoins sont satisfaits. GDB-004B reste l'autorité sur les besoins
physiologiques urgents.
⸻
MODÈLE

Chaque Ambition d'un habitant possède cinq attributs :

- **Objectif.** L'état futur désiré, exprimé de façon identifiable dans
  le World : « posséder un logement », « atteindre le Niveau 80 en
  cuisine », « établir une relation de Force > 70 avec l'habitant X »,
  « accumuler N portions d'un produit ». L'objectif doit pouvoir être
  évalué comme atteint ou non à chaque Tick --- c'est ce qui permet à
  l'Ambition de produire un Intent orienté plutôt qu'un comportement
  vague.

- **Intensité.** Valeur continue bornée entre 0 et 100. Elle exprime
  la force du désir : à Intensité élevée, l'Ambition produit un Intent
  même lorsque l'objectif est encore très loin ; à Intensité basse,
  elle ne se manifeste que si aucune autre source d'Intent n'est
  exécutable. L'Intensité n'est pas la priorité de l'Ambition dans la
  chaîne GDB-004A --- les besoins urgents restent toujours prioritaires
  --- mais son poids interne parmi les Ambitions concurrentes.

- **Progrès.** Valeur continue bornée entre 0 et 100, représentant la
  distance parcourue vers l'objectif. 0 = début, 100 = objectif atteint.
  Le Progrès est mis à jour à chaque Tick où l'état du World est
  évalué contre l'objectif. Il n'est jamais calculé par l'Ambition
  elle-même --- c'est le System responsable des Ambitions qui lit l'état
  du World et met à jour le Progrès.

- **Intent produit.** L'objectif que l'Ambition soumet au pipeline ACT
  si elle est activée. Conforme au contrat Intent ordinaire : acteur,
  objectif, priorité. L'Ambition ne produit jamais directement une
  Action Instance [réf: ACT-002].

- **Tick de création.** Le Tick auquel l'Ambition est née. Sert au
  tie-break déterministe entre Ambitions de même Intensité.
⸻
ORIGINE DES AMBITIONS

Les ambitions naissent de l'interaction entre :

- la personnalité [réf: GDB-004D] ;
- les besoins [réf: GDB-004B] ;
- les expériences vécues ;
- la culture [réf: GDB-009D, GDB-009E] ;
- les opportunités [réf: GDB-002E] ;
- les relations [réf: GDB-004C].

Une Ambition n'est jamais imposée par le moteur. Elle émerge de l'état
du World et de l'histoire de l'habitant. Le moteur peut créer une
Ambition lorsqu'une combinaison de conditions la rend plausible, mais
la règle de déclenchement de création appartient aux documents qui
spécifient chaque type d'Ambition concret --- pas à ce document.
⸻
ÉVOLUTION

**Renforcement.** Un événement significatif [réf: GDB-002B] cohérent
avec l'Ambition peut augmenter son Intensité. Un succès partiel vers
l'objectif renforce sans saturer.

**Affaiblissement.** Un événement significatif contraire (échec majeur,
perte d'un prérequis, changement de vie) peut diminuer l'Intensité.
Si l'Intensité atteint 0, l'Ambition disparaît.

**Accomplissement.** Lorsque le Progrès atteint 100, l'Ambition est
considérée comme accomplie et disparaît. Sa disparition peut déclencher
la naissance d'une nouvelle Ambition plus élevée (progression vers un
objectif supérieur) ou simplement laisser de l'espace à d'autres
Ambitions. Ce comportement n'est pas automatique --- il dépend de
règles spécifiques à chaque type d'Ambition.

**Abandon.** L'habitant peut abandonner une Ambition si les conditions
de sa vie la rendent durablement inatteignable. L'abandon est un
événement identifiable, jamais une dérive silencieuse (invariant partagé
avec GDB-004D et GDB-004E).

L'Intensité reste toujours bornée entre 0 et 100 (Clamp).
⸻
ARBITRAGE AVEC LES AUTRES SOURCES D'INTENT

Une Ambition est une source d'Intent parmi d'autres, placée après les
besoins urgents, les opportunités économiques et les Habitudes dans la
chaîne définie par GDB-004A :

```
besoins physiologiques urgents (GDB-004B)
↓
transfert volontaire exécutable (GDB-004A)
↓
activité productive exécutable (GDB-004A)
↓
Habitudes actives (GDB-004E)
↓
Ambitions
↓
aucun Intent
```

Lorsque plusieurs Ambitions sont simultanément candidates, la priorité
suit :

1. Intensité la plus élevée.
2. En cas d'égalité d'Intensité : Progrès le plus avancé (l'Ambition
   la plus proche de son objectif est traitée en premier --- cohérent
   avec GDB-004B : « satisfaction plus basse → urgence plus forte »,
   traduit ici en « objectif plus proche → traitement prioritaire »).
3. En cas d'égalité d'Intensité et de Progrès : Ambition créée au Tick
   le plus bas (la plus ancienne).

Ce tie-break est entièrement déterministe.
⸻
DIVERSITÉ

Deux habitants ayant vécu des expériences proches peuvent poursuivre des
ambitions totalement différentes, car la personnalité module l'origine
et l'Intensité des Ambitions de façon individuelle.

Cette diversité contribue à rendre le monde crédible.
⸻
IMPACT

Les ambitions influencent :

- les choix quotidiens ;
- les relations ;
- les métiers ;
- les déplacements ;
- les projets personnels ;
- les histoires émergentes.
⸻
PARAMÈTRES D'IMPLÉMENTATION

Les valeurs suivantes ne sont pas fixées par ce document : Intensité
initiale d'une nouvelle Ambition, montant de renforcement ou
d'affaiblissement par événement significatif, seuil d'inatteignabilité
déclenchant un abandon. Même posture que GDB-004C, GDB-004E : le modèle
est fixé, les constantes restent des paramètres d'équilibrage.
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée aux ambitions devra :

1. respecter l'identité de chaque habitant ;
2. évoluer avec son histoire ;
3. influencer plusieurs systèmes ;
4. rester cohérente avec les autres principes de la Game Design Bible ;
5. favoriser les histoires émergentes.
⸻
CRITÈRE DE VALIDATION

Cette mécanique permet-elle aux habitants d'avoir de véritables
objectifs de vie plutôt que des comportements préprogrammés ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : passage en Maturité 2. Ajout du MODÈLE (cinq attributs :
Objectif évaluable dans le World, Intensité 0-100, Progrès 0-100,
Intent produit conforme ACT, Tick de création), des règles d'ÉVOLUTION
(renforcement, affaiblissement, accomplissement, abandon --- jamais de
dérive silencieuse), d'ARBITRAGE (place des Ambitions en fin de chaîne
GDB-004A, tie-break déterministe Intensité → Progrès → ancienneté), et
des frontières explicites avec GDB-004E (Habitudes) et GDB-004B
(Besoins). Section PARAMÈTRES D'IMPLÉMENTATION ajoutée. En-tête mis en
conformité avec MASTER-004 (Maturité et Bibliothèque absents de la
v1.0).

Version 1.0 : création du document.
