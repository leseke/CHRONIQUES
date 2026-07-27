GDB-003H --- Les Frontières Naturelles

Version : 1.1
Statut : Officiel
Type : Architecture du Monde
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir le rôle des frontières naturelles dans Chroniques.

Les frontières structurent le monde sans recourir à des barrières 
artificielles.
⸻
PRINCIPE

Une frontière naturelle découle de la géographie, du climat ou de 
l'activité humaine.

Elle guide l'exploration tout en restant crédible.
⸻
TYPES DE FRONTIÈRES

Les frontières peuvent être formées par :

	⁃	chaînes de montagnes ;
	⁃	fleuves ;
	⁃	forêts profondes ;
	⁃	déserts ;
	⁃	marécages ;
	⁃	falaises ;
	⁃	mers.
⸻
FONCTIONS

Les frontières :

	⁃	différencient les territoires ;
	⁃	influencent les cultures ;
	⁃	orientent les échanges ;
	⁃	créent des défis d'exploration.
⸻
ÉVOLUTION

Certaines frontières évoluent avec le temps (cours d'eau, forêts, zones 
côtières), tandis que d'autres restent relativement stables.
⸻
STATUT DOCUMENTAIRE

Une frontière n'est pas un niveau supplémentaire de la hiérarchie
géographique [réf: GDB-003A]. Elle ne possède aucune existence
indépendante d'une Zone.

Une frontière est une **qualification** apposée à une ou plusieurs
Zones contiguës qui séparent deux Régions ou deux Continents. Une forêt
profonde qui sert de frontière reste, structurellement, une Zone comme
une autre : elle possède son propre biome [réf: GDB-003J], ses propres
Lieux et Points d'intérêt éventuels, exactement comme le prévoit
GDB-003D.

Ce que la qualification de frontière ajoute, ce n'est donc pas une
structure de données supplémentaire, mais deux propriétés :

- elle relie exactement deux Régions (ou deux Continents) adjacents,
  jamais un nombre différent ;
- elle influence, à ce titre, les échanges, les cultures et les
  déplacements entre ces deux territoires précis --- ce que ne fait
  pas une Zone ordinaire.

Une Zone peut donc être une frontière ou non ; elle ne cesse jamais
d'être une Zone à part entière pour autant.
⸻
RÈGLES DE CONCEPTION

Toute frontière devra :

	1.	être justifiée par le monde ;
	2.	renforcer l'immersion ;
	3.	ne jamais bloquer arbitrairement le joueur ;
	4.	enrichir l'identité des territoires ;
	5.	créer des opportunités d'histoires.
⸻
CRITÈRE DE VALIDATION

Cette frontière paraît-elle naturelle et cohérente sans donner 
l'impression d'une limite artificielle de jeu ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : ajout de la section « Statut documentaire », clarifiant qu'une
frontière est une qualification de Zone(s) et non un niveau supplémentaire de la
hiérarchie. Corrige GDB-003-C03. En-tête mis en conformité avec MASTER-004.

Version 1.0 : création du document.
