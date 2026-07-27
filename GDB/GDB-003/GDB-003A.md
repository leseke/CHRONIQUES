GDB-003A --- La Structure du Monde

Version : 1.1
Statut : Officiel
Type : Architecture du Monde
Maturité : 2
Bibliothèque : GDB
⸻
OBJECTIF

Définir la structure générale du monde de Chroniques avant la création 
des continents, régions et villes.
⸻
PRINCIPE

Le monde est organisé selon une hiérarchie stable afin de garantir sa 
cohérence et son évolutivité.
⸻
HIÉRARCHIE

Le monde est composé de :

	⁃	Monde
	⁃	Continents
	⁃	Régions
	⁃	Zones
	⁃	Lieux
	⁃	Points d'intérêt

Chaque niveau possède sa propre identité et influence les niveaux 
inférieurs.
⸻
CARDINALITÉS

Chaque niveau de la hiérarchie appartient à exactement un niveau
parent, jamais zéro, jamais plusieurs --- à l'exception des Frontières
et des Biomes, qui ne sont pas des niveaux de la hiérarchie mais des
qualifications transversales [réf: GDB-003H, GDB-003J].

| Niveau | Appartient à | Cardinalité du parent | Contient | Cardinalité de l'enfant |
|---|---|---|---|---|
| Continent | Monde | exactement 1 | Régions | 1 ou plus |
| Région | Continent | exactement 1 | Zones | 0 ou plus |
| Zone | Région | exactement 1 | Lieux | 0 ou plus |
| Lieu | Zone | exactement 1 | Points d'intérêt | 0 ou plus |
| Point d'intérêt | Zone | exactement 1 | Lieu (optionnel) | 0 ou 1 |

Trois invariants découlent de ce tableau :

- **Aucun rattachement double.** Une Région n'appartient jamais à deux
  Continents ; une Zone n'appartient jamais à deux Régions ; ainsi de
  suite à chaque niveau. Un déplacement d'un élément d'un parent à un
  autre est un événement de conception explicite, jamais un état
  transitoire du monde.
- **Le vide est autorisé sous Continent.** Une Région peut ne contenir
  aucune Zone détaillée (terres non explorées ou non encore générées).
  Un Continent, en revanche, ne peut jamais exister sans au moins une
  Région : c'est ce qui lui donne une identité au sens de GDB-003B.
- **Un Point d'intérêt appartient toujours à une Zone, parfois à un
  Lieu.** Voir GDB-003F pour le détail de cette relation [réf: GDB-003F].
⸻
IDENTITÉ

Chaque continent possède :

	⁃	une histoire ;
	⁃	un climat dominant ;
	⁃	des cultures ;
	⁃	des ressources ;
	⁃	des dangers.

Chaque région développe ensuite ses propres particularités.
⸻
COHÉRENCE

Les villes, métiers, ressources et populations devront toujours être 
justifiés par leur environnement.

Aucun élément important ne sera placé au hasard.
⸻
EXPLORATION

L'exploration progresse naturellement du général vers le particulier.

Chaque découverte doit donner envie d'en découvrir une autre.
⸻
RÈGLES DE CONCEPTION

Toute création de zone devra :

	1.	respecter cette hiérarchie ;
	2.	renforcer la cohérence du monde ;
	3.	posséder une identité propre ;
	4.	créer des opportunités d'histoires ;
	5.	rester évolutive.
⸻
CRITÈRE DE VALIDATION

Cette nouvelle zone possède-t-elle une raison crédible d'exister dans 
le monde ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : ajout des cardinalités géographiques (tableau des relations
parent/enfant et trois invariants de rattachement). Corrige GDB-003-C01. En-tête
mis en conformité avec MASTER-004.

Version 1.0 : création du document.
