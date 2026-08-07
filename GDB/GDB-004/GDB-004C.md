GDB-004C --- Les Relations Sociales

Version : 1.1
Statut : Officiel
Type : Population du Monde
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir les principes qui gouvernent les relations sociales entre les
habitants de Chroniques, avec une précision suffisante pour être
implémentées sans interprétation (MASTER-007, Maturité 2).

Les relations sociales constituent un moteur majeur des histoires
émergentes.
⸻
PRINCIPE

Chaque habitant entretient un réseau de relations.

Ces relations évoluent avec le temps, les événements et les conséquences
des actions.
⸻
TYPES DE RELATIONS

Les relations peuvent être :

	⁃	familiales ;
	⁃	amicales ;
	⁃	professionnelles ;
	⁃	commerciales ;
	⁃	politiques ;
	⁃	conflictuelles ;
	⁃	sentimentales.

Une paire d'habitants peut entretenir plusieurs relations de nature
différente simultanément (par exemple familiale et conflictuelle). Une
paire n'entretient jamais deux relations de la même nature en parallèle
--- une nouvelle interaction de même nature fait évoluer la relation
existante, elle n'en crée jamais une seconde.
⸻
MODÈLE DE FORCE

Chaque relation possède une Force, sur une échelle continue de 0 à 100.

La Force représente l'intensité du lien, jamais son signe narratif ---
une relation Conflictuelle de Force 90 est un conflit intense, pas une
relation positive de Force négative. Le signe (positif ou négatif) est
porté par le Type de relation (section précédente), jamais par la
Force elle-même.

Une relation naît à la première interaction qualifiante entre deux
habitants, à une Force initiale modérée --- ni nulle (les deux habitants
se connaissent désormais), ni maximale (une première interaction ne
vaut jamais une relation éprouvée).
⸻
ÉVOLUTION

Une relation n'est jamais figée. Deux forces l'affectent, à distinguer
strictement :

1. **Érosion naturelle.** En l'absence de toute interaction, la Force
   d'une relation diminue progressivement à chaque Tick --- un lien
   qu'on n'entretient plus s'affaiblit, conformément au principe déjà
   énoncé. L'érosion ne peut jamais faire disparaître une relation
   Familiale en dessous d'un plancher non nul --- un lien du sang
   s'affaiblit, il ne s'efface jamais complètement par le seul écoulement
   du temps (cohérent avec GDB-009C, Les Familles). Les autres types de
   relation n'ont pas de plancher : ils peuvent s'éteindre entièrement.

2. **Effet d'interaction.** Chaque interaction qualifiante modifie la
   Force d'un montant positif ou négatif, selon sa nature narrative
   (un Moment fort renforce, une Rupture érode fortement). Cet effet
   s'ajoute à l'érosion naturelle du Tick, il ne la remplace pas.

La Force reste toujours bornée entre 0 et 100 (Clamp) --- aucune
interaction ni aucune érosion ne peut la faire sortir de cet intervalle.

Une relation dont la Force atteint 0 disparaît --- sauf plancher
familial (voir ci-dessus). Une relation disparue n'est jamais restaurée
directement : une nouvelle interaction qualifiante en recrée une, à la
Force initiale de la section précédente, sans mémoire de l'ancienne
Force. Les Épisodes qui lui étaient attachés suivent la règle de la
section suivante.
⸻
ÉPISODES

Toute interaction ne mérite pas d'être retenue individuellement --- seule
une interaction dont l'ampleur (positive ou négative) franchit un seuil
d'importance devient un Épisode, conservé et attaché à la relation.

Un Épisode conserve : le Tick de l'interaction, une description courte,
et son impact sur la Force.

Le nombre d'Épisodes attachés à une relation est borné. Au-delà de cette
capacité, le plus ancien Épisode est retiré en priorité lorsqu'un nouvel
Épisode significatif survient --- jamais le plus marquant, quel que soit
son âge.

FRONTIÈRE AVEC GDB-002B (MÉMOIRE DU MONDE) --- un Épisode n'est jamais un
Souvenir au sens de GDB-002B. Un Épisode est une donnée strictement
bilatérale, privée à la paire d'habitants concernée, sans portée
narrative au-delà d'eux. Un Souvenir (GDB-002B) est un palier de la
Mémoire du Monde, à portée familiale ou communautaire, atteint
uniquement si l'événement franchit le seuil de significativité propre à
ce système. Un Épisode particulièrement significatif *peut* déclencher
la création d'une Anecdote puis d'un Souvenir dans la Mémoire du Monde
--- c'est une promotion vers un système distinct, jamais une
renumérotation ou une double appartenance au même palier.
⸻
IMPACT

Les relations influencent :

	⁃	la confiance ;
	⁃	la coopération ;
	⁃	les opportunités ;
	⁃	la réputation ;
	⁃	les décisions futures.

FRONTIÈRE AVEC GDB-004I (RÉPUTATION) --- ce document ne construit pas la
Réputation. La Réputation (GDB-004I) est une perception agrégée,
observateur-dépendante, à l'échelle d'un groupe ; la Force et les
Épisodes décrits ici sont une donnée bilatérale, entre deux habitants
précis. Les Relations fourniront une des entrées dont la Réputation aura
besoin le moment venu (MASTER-005, Phase 3, quand des habitants
autonomes existeront pour former et faire vivre ces perceptions) ---
sans qu'il soit nécessaire, ni souhaitable par anticipation (MASTER-006),
de construire ce lien avant que des observateurs autonomes existent
réellement.
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée aux relations devra :

	1.	évoluer naturellement ;
	2.	produire des conséquences crédibles ;
	3.	éviter les scripts artificiels ;
	4.	enrichir les histoires émergentes ;
	5.	respecter la personnalité des habitants.
⸻
PARAMÈTRES D'IMPLÉMENTATION

Les valeurs suivantes ne sont volontairement pas fixées par ce document :
taux d'érosion par Tick, plancher familial exact, seuil d'importance
déclenchant un Épisode, capacité maximale d'Épisodes, Force initiale
d'une nouvelle relation. Le modèle ci-dessus contraint leur forme (une
Force bornée 0-100, une érosion monotone, un seuil qualifiant un
Épisode, une capacité avec éviction du plus ancien) sans en imposer la
valeur numérique exacte --- même posture que NeedsDecaySystem et
AgingSystem (ENGINE-004) : des paramètres de constructeur, des valeurs
de travail plausibles à ajuster par le playtesting, jamais des
constantes GDB invérifiables avant toute implémentation réelle.
⸻
CRITÈRE DE VALIDATION

Cette mécanique rend-elle les relations plus vivantes et crédibles
sans les réduire à une simple statistique ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : ajout du modèle de Force (échelle 0-100, érosion naturelle
distincte de l'effet d'interaction, plancher familial), introduction des
Épisodes avec seuil d'importance et capacité bornée, frontière explicite
avec GDB-002B (Souvenir, réservé à la Mémoire du Monde --- jamais réemployé
ici) et avec GDB-004I (Réputation, différée à MASTER-005 Phase 3). Passage
en Maturité 2 : le modèle est désormais suffisamment précis pour être
implémenté sans interprétation, les seules valeurs laissées ouvertes étant
les constantes numériques exactes (voir PARAMÈTRES D'IMPLÉMENTATION).
En-tête mis en conformité avec MASTER-004 (Maturité et Bibliothèque,
absents de la v1.0).

Version 1.0 : création du document.
