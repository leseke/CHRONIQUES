GDB-002B --- La Mémoire du Monde

Version : 1.1
Statut : Officiel
Type : Fondations du Gameplay
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir le fonctionnement de la mémoire du monde.

La mémoire du monde permet à Chroniques de conserver les traces des 
actions importantes afin que chaque aventure laisse une empreinte 
durable.
⸻
DÉFINITION

Le monde se souvient.

Toutes les actions ne méritent pas d'être mémorisées.

Seules celles qui modifient réellement le monde, une communauté ou une 
lignée peuvent devenir des souvenirs persistants.
⸻
CE QUI PEUT ÊTRE MÉMORISÉ

	⁃	constructions majeures ;
	⁃	destructions importantes ;
	⁃	découvertes remarquables ;
	⁃	événements historiques ;
	⁃	familles influentes ;
	⁃	œuvres durables ;
	⁃	transformations du paysage.
⸻
CE QUI NE DOIT PAS ÊTRE MÉMORISÉ

Les actions répétitives ou sans impact significatif.

La mémoire du monde doit rester lisible et pertinente.
⸻
ÉVOLUTION

Les souvenirs peuvent évoluer.

Certains disparaissent naturellement.

D'autres deviennent des légendes ou des traditions.

La mémoire privilégie les événements ayant réellement influencé le 
monde.
⸻
LIEN AVEC LA LIGNÉE

Les générations suivantes héritent d'un monde possédant déjà une 
histoire.

Leur aventure s'inscrit dans cette continuité sans être enfermée par le 
passé.
⸻
DISTINCTION : MÉMOIRE DU MONDE CONTRE MÉMOIRE DE SIMULATION

Ce document décrit la **Mémoire du Monde** : un sous-ensemble narratif,
curaté, de ce qui mérite d'être raconté.

Elle ne doit pas être confondue avec la mémoire technique de la
simulation --- l'ensemble des State et des Event que le moteur retient
en permanence pour chaque entité, à chaque tick, conformément aux
primitives du Kernel [réf: CORE-000C].

La différence tient à trois points :

- **Volume.** La mémoire de simulation couvre potentiellement chaque
  entité et chaque tick. La Mémoire du Monde ne couvre qu'une fraction
  infime de ces événements --- ceux qui franchissent le seuil de
  significativité défini ci-dessous.
- **Fonction.** La mémoire de simulation sert à faire tourner le monde
  (recalculer un état, rejouer une séquence, sauvegarder). La Mémoire du
  Monde sert à raconter le monde (légendes, traditions, réputation,
  souvenirs transmis).
- **Durée de vie.** Une donnée de simulation peut être recalculée ou
  écrasée sans conséquence narrative. Un élément de la Mémoire du Monde
  suit le cycle de persistance ci-dessous, indépendamment du cycle de
  vie technique de l'Event qui l'a produit.

Tout Event de simulation peut *devenir* un élément de la Mémoire du
Monde s'il franchit le seuil de significativité. L'inverse est faux :
un élément de la Mémoire du Monde n'est jamais lui-même un State de
simulation, seulement une trace qui y fait référence.
⸻
CRITÈRES DE PERSISTANCE

Un élément de la Mémoire du Monde appartient toujours à l'un des quatre
paliers suivants, du plus éphémère au plus durable.

| Palier | Portée | Condition d'entrée | Condition de sortie |
|---|---|---|---|
| Anecdote | Un individu ou un petit groupe | Franchit le seuil de significativité (voir liste « ce qui peut être mémorisé ») | S'efface si jamais reliée à un autre événement dans la génération qui suit |
| Souvenir | Une famille ou une communauté locale | Une Anecdote reliée à au moins un autre événement mémorisé, ou transmise à la génération suivante | S'efface sur deux générations sans nouvelle référence ni transmission |
| Légende | Une région ou plusieurs communautés | Un Souvenir reste référencé après deux générations, ou influence un événement d'ampleur régionale | Ne s'efface jamais spontanément ; ne peut être révisée que par un événement contradictoire d'ampleur au moins égale |
| Tradition | La civilisation ou une culture entière | Une Légende donne naissance à une pratique répétée (rite, fête, coutume, institution) | Permanente tant que la pratique qu'elle a engendrée existe |

Un élément ne saute jamais un palier : il progresse ou régresse d'un
palier à la fois, à chaque évaluation de génération. La progression
exige une condition d'entrée remplie ; en son absence, l'élément régresse
ou s'efface selon sa condition de sortie.

Ce mécanisme rend opérationnelle la règle déjà énoncée plus haut :
« Certains disparaissent naturellement. D'autres deviennent des
légendes ou des traditions. »
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée à la mémoire devra :

	1.	préserver les performances ;
	2.	conserver uniquement les éléments significatifs ;
	3.	renforcer le sentiment de continuité ;
	4.	favoriser les histoires émergentes ;
	5.	rester compréhensible pour le joueur.
⸻
CRITÈRE DE VALIDATION

Cette mécanique permet-elle au monde de conserver une histoire 
crédible sans l'encombrer d'informations inutiles ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : ajout de la distinction Mémoire du Monde / mémoire de simulation
(corrige GDB-002-C03) et des critères de persistance à quatre paliers --- Anecdote,
Souvenir, Légende, Tradition --- avec conditions d'entrée et de sortie explicites
(corrige GDB-002-C01). Passage en Maturité 2 : les critères sont désormais
suffisamment précis pour être implémentés sans interprétation. En-tête mis en
conformité avec MASTER-004.

Version 1.0 : création du document.
