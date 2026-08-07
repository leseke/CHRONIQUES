GDB-004J --- La Transmission

Version : 1.2
Statut : Officiel
Type : Population du Monde
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir les principes qui gouvernent la transmission entre les individus
et les générations.

La transmission permet au monde de conserver et faire évoluer son
savoir, ses traditions et ses réalisations.
⸻
PRINCIPE

Rien d'important ne devrait disparaître sans laisser de trace.

Les connaissances, techniques, valeurs, œuvres et patrimoines peuvent
être transmis.
⸻
FRONTIÈRE AVEC GDB-008G

`GDB-008G` (L'Héritage) décrit, sous un titre différent, le même
principe --- « ce qui peut être transmis » y est presque mot pour mot
identique à la section suivante --- sans qu'aucun renvoi croisé n'existe
entre les deux documents avant cette révision. Troisième occurrence du
même défaut que celui déjà signalé entre GDB-004H et GDB-007A/B : deux
chapitres traitant le même sujet sous des titres distincts échappent au
repérage par titre identique qu'a effectué GDB-CATALOG-C01. Ce document
ne résout pas la frontière ici --- la régénération de GDB-008G reste à
faire séparément (un constat à la fois, MASTER-008) --- mais signale
qu'un passage d'audit dédié au repérage par *concept* plutôt que par
*titre* serait probablement nécessaire pour trouver les occurrences
restantes de ce même défaut ailleurs dans la GDB.

En l'attente de cette régénération, la frontière de fait est : GDB-004J
fait autorité sur le mécanisme de transmission entre deux individus
(un défunt et son héritier) --- ce document, y compris son MODÈLE DE
DÉSIGNATION DE L'HÉRITIER ci-dessous ; GDB-008G reste la référence sur
la portée générationnelle plus large (ce qu'une génération, au sens
collectif, laisse à la suivante).
⸻
CE QUI PEUT ÊTRE TRANSMIS

	⁃	savoir-faire ;
	⁃	connaissances ;
	⁃	patrimoine matériel ;
	⁃	réputation ;
	⁃	traditions ;
	⁃	relations ;
	⁃	responsabilités.
⸻
LA TRANSMISSION N'EST PAS UNE COPIE

Chaque génération reçoit un héritage.

Elle reste libre de l'utiliser, de le transformer ou de l'abandonner.

La transmission influence l'avenir sans le déterminer.
⸻
ÉVOLUTION

Chaque transmission peut enrichir ou modifier ce qui est transmis.

Le monde évolue ainsi naturellement de génération en génération.
⸻
IMPACT

La transmission influence :

	⁃	les lignées ;
	⁃	les communautés ;
	⁃	les métiers ;
	⁃	les cultures ;
	⁃	les histoires émergentes.
⸻
MODÈLE DE DÉSIGNATION DE L'HÉRITIER

Les cas d'échec ci-dessous supposent qu'un « successeur » soit
identifié ou non --- ce que ce document ne précisait pas jusqu'ici.
S'appuyant sur le modèle de Force désormais défini par GDB-004C, la
désignation suit une règle déterministe, conforme au Principe 10 de
MASTER-002 (« à état identique, la même séquence produit toujours le
même résultat ») :

1. Parmi les relations actives du défunt au moment de la transmission,
   isoler celles de type Familiale [réf: GDB-004C].
2. S'il en existe au moins une, l'héritier est celle dont la Force est
   la plus élevée. En cas d'égalité stricte de Force, la relation la
   plus ancienne (Tick de création le plus bas) l'emporte.
3. Si aucune relation Familiale n'existe, la même règle s'applique à
   l'ensemble des relations actives du défunt, tous types confondus.
4. Si aucune relation active n'existe, il n'y a pas de successeur ---
   voir CAS D'ÉCHEC, « Absence de successeur ».

Ce modèle ne privilégie jamais un type de relation autre que Familiale
par construction --- une relation Amicale très forte ne l'emporte
jamais sur une relation Familiale plus faible, conformément à la place
que GDB-009C (Les Familles) accorde au lien du sang. Il reste
volontairement silencieux sur tout critère narratif supplémentaire
(mérite, promesse, testament explicite du défunt) --- leur ajout
éventuel reste un enrichissement futur de ce document, pas une
correction de celui-ci.
⸻
CAS D'ÉCHEC DE LA TRANSMISSION

La transmission n'aboutit pas toujours. Trois cas d'échec doivent être
distingués, car ils appellent des résolutions différentes.

- **Absence de successeur.** Aucun héritier n'existe au moment de la
  transmission (mort sans descendance, lignée interrompue) --- au sens
  du MODÈLE DE DÉSIGNATION ci-dessus, aucune relation active. Le
  patrimoine matériel rejoint alors la communauté ou la relation la
  plus proche du défunt [réf: GDB-004C] ; la réputation et les œuvres
  durables suivent leur propre cycle de persistance indépendamment de
  tout héritier [réf: GDB-002B] ; le savoir-faire non enseigné à
  quiconque est simplement perdu --- une Compétence, à la différence
  d'une Connaissance consignée, ne survit jamais à celui qui la
  pratiquait seul [réf: GDB-004G].
- **Refus du successeur.** L'héritier existe mais rejette
  l'héritage --- en tout ou en partie. Ce refus est toujours possible
  et jamais pénalisé : il concrétise le principe déjà énoncé plus haut
  selon lequel la génération suivante reste libre d'abandonner ce
  qu'elle reçoit. Le patrimoine refusé suit alors le même chemin que
  s'il n'y avait pas eu de successeur.
- **Transmission incomplète.** L'héritier reçoit le patrimoine matériel
  ou la réputation, mais la mort du transmetteur survient avant qu'une
  Compétence ait pu être réellement enseignée par la pratique. Seule la
  Connaissance théorique associée passe alors à la génération suivante
  [réf: GDB-004G] ; la Compétence correspondante doit être reconstruite
  depuis le début, ce qui peut devenir la source d'un nouveau projet de
  vie pour l'héritier [réf: GDB-002F].

Invariant commun aux trois cas : un échec de transmission n'est jamais
un événement muet. Il produit toujours soit une conséquence visible
dans le monde (patrimoine redistribué, savoir perdu et remarqué comme
tel), soit une opportunité nouvelle pour la génération suivante --- il
ne doit jamais se résoudre en simple disparition silencieuse de
données.
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée à la transmission devra :

	1.	respecter le temps investi ;
	2.	valoriser l'apprentissage ;
	3.	préserver la liberté des successeurs ;
	4.	éviter les bonus automatiques démesurés ;
	5.	renforcer la continuité du monde.
⸻
CRITÈRE DE VALIDATION

Cette mécanique transmet-elle un héritage crédible sans supprimer la
liberté de la génération suivante ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.2 : ajout du MODÈLE DE DÉSIGNATION DE L'HÉRITIER, absent
jusqu'ici alors que les CAS D'ÉCHEC en dépendaient implicitement ---
règle déterministe fondée sur le modèle de Force de GDB-004C
(priorité Familiale, puis Force la plus élevée, tie-break par
ancienneté). Ajout de la frontière avec GDB-008G (troisième
recoupement de contenu sous un titre différent, après GDB-004C/GDB-002B
et GDB-004H/GDB-007A --- suggère un défaut structurel du repérage par
titre de GDB-CATALOG-C01, à corriger par un passage dédié). Aucun
changement aux CAS D'ÉCHEC ni aux RÈGLES DE CONCEPTION, déjà conformes.

Version 1.1 : ajout des trois cas d'échec de la transmission (absence de
successeur, refus, transmission incomplète) et de leur invariant commun. Corrige
GDB-004-C03. En-tête mis en conformité avec MASTER-004.

Version 1.0 : création du document.
