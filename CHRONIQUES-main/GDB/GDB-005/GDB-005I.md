GDB-005I --- La Valeur

Version : 1.1
Statut : Officiel
Type : Économie & Progression
Maturité : 2
Bibliothèque : GDB
⸻
OBJECTIF

Définir les principes fondamentaux de la valeur dans Chroniques.

La valeur représente l'importance qu'un individu ou une communauté 
accorde à un bien, un service, un savoir ou une action.

Elle ne doit jamais être réduite à un simple prix.
⸻
PRINCIPE

La valeur est contextuelle.

Elle dépend des besoins, de la rareté, des compétences mobilisées, du 
temps investi, de la confiance et des circonstances.

Deux habitants peuvent attribuer une valeur différente à un même objet.
⸻
LES SOURCES DE VALEUR

La valeur peut provenir notamment :

	⁃	de l'utilité ;
	⁃	de la rareté ;
	⁃	de la qualité ;
	⁃	du savoir-faire ;
	⁃	de l'histoire ;
	⁃	de la réputation ;
	⁃	de la valeur sentimentale.

Aucune source de valeur n'est universellement dominante.
⸻
RELATION AVEC CORE VALUE

La Valeur économique décrite ici est un jugement contextuel et
subjectif porté par un individu ou une communauté --- elle n'a pas de
nombre unique et absolu.

Le Kernel définit par ailleurs une primitive nommée Value [réf:
CORE-000C], qui est un simple conteneur de donnée typée attaché à un
State. Les deux ne se confondent pas :

- CORE Value est la structure technique qui *porte* un nombre, un
  texte ou toute autre donnée dans la simulation.
- La Valeur économique de ce document est *ce que signifie* ce nombre
  pour un habitant donné, à un instant donné, dans un contexte donné.

Concrètement, un même prix stocké comme CORE Value (par exemple un
entier) peut correspondre à des Valeurs économiques différentes selon
l'habitant qui l'observe --- puisque la rareté, la confiance ou la
valeur sentimentale ne sont pas encodées dans ce nombre lui-même, mais
dans la relation entre l'habitant et le bien. La Valeur économique ne
redéfinit donc jamais CORE Value : elle en est une interprétation
contextuelle, jamais une seconde source de vérité pour la donnée
elle-même.
⸻
ÉVOLUTION

La valeur évolue avec le monde.

Une découverte, une pénurie, une innovation ou un changement culturel 
peuvent transformer progressivement la perception d'un bien ou d'un 
service.
⸻
IMPACT

La valeur influence :

	⁃	les échanges ;
	⁃	les marchés ;
	⁃	les investissements ;
	⁃	les décisions des habitants ;
	⁃	les projets des joueurs.

Elle participe à rendre l'économie organique plutôt que mécanique.
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée à la valeur devra :

	1.	rester dépendante du contexte ;
	2.	éviter les évaluations figées ;
	3.	prendre en compte plusieurs facteurs ;
	4.	renforcer l'économie vivante ;
	5.	favoriser les histoires émergentes.
⸻
CRITÈRE DE VALIDATION

Cette mécanique représente-t-elle une valeur crédible plutôt qu'un 
simple chiffre fixe ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : ajout de la section « Relation avec CORE Value », distinguant la
Valeur économique (jugement contextuel) de CORE Value (conteneur de donnée typée).
Corrige GDB-005-C03. En-tête mis en conformité avec MASTER-004.

Version 1.0 : création du document.
