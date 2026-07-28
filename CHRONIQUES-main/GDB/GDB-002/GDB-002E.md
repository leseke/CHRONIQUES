GDB-002E --- Les Opportunités

Version : 1.1
Statut : Officiel
Type : Fondations du Gameplay
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir la philosophie des opportunités dans Chroniques.

Les opportunités sont les occasions offertes au joueur par le monde.

Elles remplacent les objectifs imposés.
⸻
DÉFINITION

Une opportunité est une possibilité d'agir.

Elle peut apparaître naturellement à la suite :

	⁃	d'un événement ;
	⁃	d'une rencontre ;
	⁃	d'une découverte ;
	⁃	d'une rumeur ;
	⁃	d'un besoin exprimé par le monde.

Le joueur reste libre de l'ignorer.
⸻
LE MONDE PROPOSE

Chroniques ne pousse jamais le joueur à suivre un chemin précis.

Le monde propose.

Le joueur dispose.
⸻
PAS D'OBLIGATION

Une opportunité n'est jamais une mission obligatoire.

Son absence ne bloque pas la progression.

Sa disparition ne constitue pas une punition.
⸻
RENOUVELLEMENT PERMANENT

Les opportunités apparaissent et disparaissent naturellement.

Certaines deviennent rares.

D'autres naissent continuellement.

Le joueur ne doit jamais avoir le sentiment que le monde est vide parce 
qu'il a manqué une occasion.
⸻
DIVERSITÉ

Les opportunités peuvent concerner :

	⁃	l'exploration ;
	⁃	les métiers ;
	⁃	les relations ;
	⁃	l'économie ;
	⁃	la politique ;
	⁃	la famille ;
	⁃	la découverte ;
	⁃	les loisirs.

Le monde doit toujours offrir plusieurs directions possibles.
⸻
CYCLE DE VIE D'UNE OPPORTUNITÉ

Une opportunité traverse toujours les états suivants, dans cet ordre :

Latente → Visible → (Saisie | Ignorée) → Résolue

- **Latente.** Les conditions du monde permettent l'apparition de
  l'opportunité, mais elle n'est pas encore portée à la connaissance du
  joueur. Cet état n'a pas de durée fixe : il dépend entièrement du
  contexte qui l'a rendu possible (un événement, une rencontre, une
  rumeur, un besoin exprimé par le monde).
- **Visible.** L'opportunité est perceptible par le joueur. Elle
  possède une fenêtre de validité propre à sa nature --- une rumeur
  s'éteint plus vite qu'une vacance de poste, une vacance de poste plus
  vite qu'un droit d'héritage. Cette fenêtre n'est jamais instantanée :
  le joueur dispose toujours d'un délai réel pour choisir.
- **Saisie.** Le joueur agit sur l'opportunité avant l'expiration de sa
  fenêtre de validité. Elle entre alors dans le moteur ACT (Intent →
  Plan → Action → Outcome) [réf: ACT-002] comme origine d'une ou
  plusieurs actions.
- **Ignorée.** La fenêtre de validité expire sans action du joueur.
  Ce n'est jamais un échec ni une sanction : c'est une issue neutre au
  même titre que « Saisie ».
- **Résolue.** L'opportunité quitte le cycle, saisie ou non. Sa
  disparition peut, selon son ampleur, produire un nouvel événement
  dynamique [réf: GDB-002D] ou un élément de la Mémoire du Monde
  [réf: GDB-002B] --- jamais une pénalité au joueur qui ne l'a pas
  saisie.

Invariant : une opportunité ignorée ne réduit jamais le nombre
d'opportunités futures. Le renouvellement permanent (voir plus haut)
s'applique indépendamment du taux de saisie du joueur --- c'est ce qui
distingue ce cycle d'une file d'attente à ressource limitée.
⸻
RÈGLES DE CONCEPTION

Toute mécanique d'opportunité devra :

	1.	respecter la liberté du joueur ;
	2.	éviter le FOMO ;
	3.	renouveler naturellement les possibilités ;
	4.	favoriser les histoires émergentes ;
	5.	rester cohérente avec l'état du monde.
⸻
CRITÈRE DE VALIDATION

Cette opportunité donne-t-elle envie d'agir sans créer une obligation 
artificielle ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : ajout du cycle de vie complet d'une opportunité (Latente → Visible →
Saisie/Ignorée → Résolue), avec renvoi vers ACT-002 pour la saisie et vers
GDB-002B/GDB-002D pour la résolution. Corrige GDB-002-C02. En-tête mis en
conformité avec MASTER-004.

Version 1.0 : création du document.
