GDB-004H --- Les Compétences

Version : 1.2
Statut : Officiel
Type : Population du Monde
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir les principes qui gouvernent les compétences des habitants de
Chroniques, avec une précision suffisante pour être implémentées sans
interprétation (MASTER-007, Maturité 2).

Les compétences représentent ce qu'un individu est réellement capable de
faire grâce à son apprentissage et à son expérience.
⸻
PRINCIPE

Les compétences ne sont jamais innées dans leur forme finale.

Elles se développent progressivement par la pratique, l'observation,
l'enseignement et l'expérience.
⸻
FRONTIÈRE AVEC LES CONNAISSANCES

Une Compétence se distingue d'une Connaissance [réf: GDB-004G] par un
critère unique : elle exige la pratique, jamais la seule communication.
Un mentor, un livre ou un récit peuvent transmettre une Connaissance en
une seule interaction ; ils ne transmettent jamais directement une
Compétence, qui reste à construire par la pratique de celui qui
l'acquiert. Voir GDB-004G pour le détail complet de cette frontière.
⸻
FRONTIÈRE AVEC GDB-007A ET GDB-007B

`GDB-007A` (Les Compétences du Joueur) et `GDB-007B` (La Maîtrise)
décrivent, sous un titre différent, la même mécanique que ce document ---
sans qu'aucun renvoi croisé n'existe entre les deux chapitres avant cette
révision.

La frontière retenue suit le même principe que celle qui sépare déjà
GDB-002/GDB-011 (simulation) de GDB-006 (expérience joueur) :

- **`GDB-004H` fait autorité sur le mécanisme.** La Compétence telle que
  définie ici (section MODÈLE DE PROGRESSION) s'applique à tout
  habitant, y compris le personnage du joueur --- il n'existe qu'une
  seule donnée de Compétence, jamais une version « joueur » distincte
  d'une version « PNJ ».
- **`GDB-007A` et `GDB-007B` décrivent le vécu du joueur** de ce même
  mécanisme --- pourquoi la progression est satisfaisante, comment la
  maîtrise se ressent, quels chemins existent --- sans redéfinir la
  donnée elle-même.

Ce document n'implémente pas cette correction pour GDB-007A/B, dont la
régénération reste à faire séparément (un constat à la fois, MASTER-008).
Un troisième recoupement, avec GDB-012 (Métiers, savoir-faire), reste à
vérifier et n'est pas traité ici.
⸻
ACQUISITION

Une compétence peut être développée grâce à :

	⁃	la répétition d'une activité ;
	⁃	un mentor ;
	⁃	la transmission familiale ;
	⁃	l'expérimentation ;
	⁃	l'étude.

La qualité de la pratique est plus importante que la simple quantité.
⸻
MODÈLE DE PROGRESSION

Chaque Compétence d'un habitant possède un Niveau, sur une échelle
continue de 0 à 100. Une Compétence non encore pratiquée n'existe pas
tant qu'aucune pratique qualifiante n'a eu lieu --- il n'y a pas de
Niveau 0 par défaut pour toute compétence imaginable, seulement pour
celles effectivement entamées.

**Progression.** Chaque pratique qualifiante augmente le Niveau d'un
montant qui dépend de deux facteurs : la Qualité de cette pratique
(section ACQUISITION --- « la qualité de la pratique est plus importante
que la simple quantité »), et le Niveau actuel. Le gain diminue à mesure
que le Niveau approche 100 --- opérationnalise directement le principe
déjà énoncé : « l'excellence doit rester rare » (section MAÎTRISE). Un
habitant débutant progresse visiblement ; un habitant déjà expert ne
progresse plus que marginalement, quelle que soit la qualité de sa
pratique.

**Affaiblissement.** Une Compétence non pratiquée pendant un nombre de
Ticks consécutifs dépassant un seuil d'inactivité commence à décliner ---
opérationnalise « s'affaiblir lorsqu'elles ne sont plus utilisées »
(section ÉVOLUTION). Le déclin cesse dès qu'une nouvelle pratique
qualifiante a lieu, quel que soit le temps déjà écoulé en inactivité.

Le Niveau reste toujours borné entre 0 et 100 (Clamp).
⸻
MAÎTRISE

La maîtrise d'une compétence est progressive.

Atteindre un niveau exceptionnel demande du temps, de la constance et
des réussites répétées.

L'excellence doit rester rare --- voir MODÈLE DE PROGRESSION pour le
mécanisme qui rend cette rareté systémique plutôt que déclarative.
⸻
ÉVOLUTION

Les compétences peuvent :

	⁃	progresser ;
	⁃	se maintenir ;
	⁃	s'affaiblir lorsqu'elles ne sont plus utilisées.

Leur évolution reste cohérente avec la vie de l'habitant.
⸻
IMPACT

Les compétences influencent :

	⁃	les métiers ;
	⁃	les projets ;
	⁃	les relations ;
	⁃	la réputation ;
	⁃	les opportunités.

Elles participent directement aux histoires émergentes.
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée aux compétences devra :

	1.	valoriser la pratique de qualité ;
	2.	respecter le temps investi ;
	3.	éviter les progressions artificielles ;
	4.	rester compatible avec les autres systèmes ;
	5.	renforcer la crédibilité des habitants.
⸻
PARAMÈTRES D'IMPLÉMENTATION

Les valeurs suivantes ne sont volontairement pas fixées par ce
document : facteur de gain par pratique, forme exacte de la diminution
du gain avec le Niveau, seuil d'inactivité, taux de déclin par Tick
inactif. Le modèle ci-dessus contraint leur forme (un Niveau borné
0-100, un gain décroissant avec le Niveau, un déclin déclenché par un
seuil d'inactivité) sans en imposer la valeur numérique exacte --- même
posture que GDB-004C (Relations) et que NeedsDecaySystem/AgingSystem
(ENGINE-004) : des paramètres de constructeur, des valeurs de travail
plausibles à ajuster par le playtesting, jamais des constantes GDB
invérifiables avant toute implémentation réelle.
⸻
CRITÈRE DE VALIDATION

Cette mécanique récompense-t-elle une véritable progression de
compétence plutôt qu'une simple accumulation d'actions ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.2 : ajout du modèle de progression (Niveau borné 0-100, gain
décroissant à l'approche de 100, déclin après un seuil d'inactivité),
opérationnalisant les principes déjà énoncés en MAÎTRISE et ÉVOLUTION.
Ajout de la frontière avec GDB-007A/GDB-007B (recoupement de contenu sous
un titre différent, jusqu'ici sans renvoi croisé --- non couvert par
GDB-CATALOG-C01, qui appariait par titre identique) et signalement d'un
recoupement possible avec GDB-012, non traité ici. Passage effectif en
Maturité 2 : le modèle est désormais suffisamment précis pour être
implémenté sans interprétation, les seules valeurs laissées ouvertes
étant les constantes numériques exactes (voir PARAMÈTRES
D'IMPLÉMENTATION) --- la v1.1 portait déjà ce champ sans que le contenu
en respecte encore le critère.

Version 1.1 : ajout d'un renvoi vers GDB-004G pour la frontière avec les
Connaissances (corrige GDB-004-C01, en complément de GDB-004G). En-tête mis en
conformité avec MASTER-004.

Version 1.0 : création du document.
