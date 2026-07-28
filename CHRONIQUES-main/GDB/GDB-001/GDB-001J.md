GDB-001J --- Glossaire Officiel

Version : 1.2
Statut : Officiel
Type : Référence
Maturité : 1
Bibliothèque : GDB
⸻


OBJECTIF

Définir le vocabulaire officiel utilisé dans la Game Design Bible.

Chaque terme possède une définition unique afin d'éviter toute
ambiguïté.
⸻

RELATION AVEC CORE

Ce glossaire définit le vocabulaire de conception du jeu : les termes qui
décrivent l'expérience, le monde et le joueur tels que la GDB les met en scène.

Il ne redéfinit aucune primitive du Kernel documentaire [réf: CORE-000C]
(Entity, Component, Value, State, Relation, Event, Time, Space, Lifecycle).
Ces primitives restent définies exclusivement par CORE, qui en est la source
canonique [réf: CORE-000A].

Lorsqu'un terme de ce glossaire s'appuie sur une primitive CORE, ce document
le précise par une référence plutôt que de la redéfinir. Un terme de ce
glossaire qui se révélerait être une primitive générale du moteur, indépendante
de tout domaine de jeu, doit être proposé à CORE plutôt que conservé ici.
⸻
Chroniques

Le projet global et le jeu en développement.

Joueur

Personne qui vit une aventure dans Chroniques.

Personnage

Individu incarné par le joueur pendant une génération.

Lignée

Suite des générations contrôlées par un même joueur.

Héritage

Ensemble des biens, connaissances, relations et réalisations transmis
entre générations.

Monde personnel

Monde propre à un joueur, façonné par ses décisions.

Civilisation

Ensemble des joueurs reliés par des interactions sans partager
obligatoirement le même monde.

Projet

Objectif poursuivi sur le moyen ou le long terme.

Instant de vie

Activité réalisée principalement pour le plaisir, l'immersion ou le
rôle-play.

Conséquence

Réaction naturelle du monde à une action. Une conséquence de jeu s'appuie sur
un ou plusieurs Event du Kernel [réf: CORE-000C], sans s'y substituer : Event
décrit ce qui s'est passé au niveau du moteur, Conséquence décrit ce que cela
signifie pour l'expérience de jeu.

Mémoire du monde

Trace durable laissée par les événements importants.

Maîtrise

Progression obtenue grâce à la qualité de la pratique plutôt qu'à la
répétition.

Budget de complexité

Limite volontaire de complexité attribuée à un système afin de préserver
sa lisibilité.

Profondeur

Richesse des choix et des interactions qu'offre un système.

Système

Ensemble cohérent de règles poursuivant un objectif précis et
interagissant avec les autres systèmes.

Histoire émergente

Récit créé naturellement par les interactions entre le joueur et le
monde, sans scénario imposé.
⸻
RÈGLE

Toute nouvelle terminologie devra être ajoutée à ce glossaire avant
d'être utilisée dans la documentation officielle, sauf s'il s'agit d'une
primitive générale du moteur : celle-ci relève alors de CORE et non de ce
glossaire.
⸻
Fin du document

Statut : Validé -- Référence officielle.

⸻
HISTORIQUE

Version 1.2 : ajout des champs Maturité et Bibliothèque, absents malgré
l'obligation posée par MASTER-004 v1.2 pour tout document régénéré. Corrige le
constat GDB-C03.

Version 1.1 : ajout de la section « Relation avec CORE », clarification des
définitions de Conséquence et Système au regard des primitives CORE, correction
d'une coquille (« définititon »). Corrige le constat GDB-001-C01.

Version 1.0 : création du document.
