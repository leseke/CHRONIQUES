# ACT-010-A — Taxonomie des Événements

> Version : 1.0
>
> Statut : Proposition
>
> Type : Classification
>
> Maturité : 2
>
> Bibliothèque : ACT
>
> Dépendances :
> - ACT-002-E, section 11 (Events)
> - ACT-002-G (Outcome)
> - ACT-007-A (Taxonomie des Conséquences)
> - ENGINE-001 (Journal d'événements du World)
>
> Utilisé par :
> - TECH
> - IA
> - QA

---

# 1. Objectif

Établir une taxonomie stable des catégories d'événements qu'une Action
peut publier, et leur relation avec les Conséquences (ACT-007-A).

Ce document n'introduit aucun nouvel axiome. ACT-002-E, section 11,
définit déjà ce qu'est un Event dans l'Action Contract (« décrivent les
événements publiés [...] permettent aux autres systèmes de réagir sans
couplage direct ») ; ENGINE-001 définit déjà le mécanisme concret de
publication (`World.Publish`, une simple accumulation, sans abonnement).
Ce document ne redéfinit ni l'un ni l'autre --- il structure les
catégories conceptuelles d'événements, absentes des deux.

---

# 2. Principe

Un Event n'est jamais la Conséquence elle-même --- il en est la trace
observable. Une Conséquence Matérielle (ACT-007-A, section 3) modifie
effectivement un Component ; l'Event qui l'accompagne ne fait que
signaler que ce changement a eu lieu, pour que d'autres systèmes
puissent y réagir sans consulter directement l'état modifié.

Un Event peut exister sans Conséquence correspondante (le simple fait
d'avoir tenté une Action, y compris en Échec, est parfois un événement
en soi --- ACT-007-A, section 6). Une Conséquence n'a en revanche pas
toujours besoin d'un Event : un changement mineur, purement interne à
une Entity, peut rester silencieux si aucun autre System n'a besoin d'y
réagir.

---

# 3. Catégories stables

**Transition.** Signale qu'une Entity a changé d'état ou d'étape.
Toujours associé à une Conséquence Statutaire (ACT-007-A, section 3).
Exemple déjà en usage dans le moteur : `vie.etape.age_adulte`,
`vie.mort` (ENGINE-004).

**Fait.** Signale qu'une Action a eu lieu, indépendamment de son
Outcome --- y compris un Échec (ACT-007-A, section 6). Ne modifie rien
par lui-même : il rend observable une tentative.

**Notification.** Signale un changement destiné à être consommé par un
autre System, sans portée narrative propre. Exemple : un inventaire mis
à jour, une valeur de State recalculée.

**Narratif.** Signale un fait destiné à interagir avec une trame GDB ---
symétrique de la catégorie Narrative des Conséquences (ACT-007-A,
section 3). Exemple : une étape de quête franchie, un événement du monde
déclenché.

---

# 4. Portée

Un Event hérite la portée de la Conséquence qui l'a produit
(ACT-007-A, section 4) : Locale s'il ne concerne que l'Acteur et les
Cibles de l'Action (ACT-004-A ; ACT-005-A), Globale s'il concerne l'état
du monde au-delà des Entity impliquées.

Un Event de portée Globale ne devient jamais, à lui seul, une nouvelle
source d'Intent (ACT-002-H) --- seul un System qui l'observe activement
peut en tirer un nouvel Intent ; l'Event lui-même reste passif
(ENGINE-001, section 2 : aucun mécanisme d'abonnement, aucune
distribution automatique).

---

# 5. Relation avec les Conséquences

Une Action produit zéro, un, ou plusieurs Events, indépendamment du
nombre de Conséquences qu'elle produit --- la relation n'est jamais
strictement un pour un.

Toute Conséquence Statutaire (ACT-007-A, section 3) produit toujours au
moins un Event de catégorie Transition --- c'est la seule
correspondance obligatoire entre les deux taxonomies. Les autres
catégories de Conséquences (Matérielle, Relationnelle, Informationnelle,
Narrative) peuvent produire un Event ou rester silencieuses, selon les
besoins de l'Action Contract (ACT-002-E) --- ce document ne fixe pas
cette décision au cas par cas.

---

# 6. Contrat

Un Event ne peut jamais modifier le monde par lui-même --- seule une
Conséquence le peut (ACT-002-G : un Outcome, et par extension tout ce
qui en découle, précède toujours les Effets, ne les produit jamais
lui-même).

Toute Conséquence Statutaire produit toujours au moins un Event de
catégorie Transition, sans exception.

Un Event de catégorie Fait peut exister sans aucune Conséquence
associée --- un Échec sans aucun changement du monde reste un fait
observable.

---

# 7. Contrat TECH

Le moteur doit être capable de :

- catégoriser tout `GameEvent` (ENGINE-001) selon les sections 3 et 4 de
  ce document ;
- garantir qu'une Conséquence Statutaire produit toujours un Event de
  catégorie Transition ;
- ne jamais faire dépendre l'exécution d'un System de la publication
  d'un Event par un autre --- conformément à ENGINE-001, section 2
  (aucune distribution).

---

# 8. Contrat QA

Les tests devront vérifier :

✓ que toute transition de Lifecycle produit un Event de catégorie
Transition (déjà couvert par `AgingSystemTests`, à recatégoriser plutôt
qu'à retester) ;

✓ qu'un Échec sans Conséquence Matérielle produit tout de même un Event
de catégorie Fait, quand l'Action Contract le prévoit ;

✓ qu'aucun Event ne modifie l'état du monde par lui-même.

---

# 9. Critères de validation

Ce document est conforme si :

✓ il n'introduit aucun axiome déjà posé par ACT-002-E, section 11 ;

✓ il ne redéfinit jamais le mécanisme concret de publication, déjà
couvert par ENGINE-001 ;

✓ sa taxonomie reste cohérente avec celle des Conséquences (ACT-007-A),
sans la dupliquer --- la section 5 relie les deux sans les fusionner.

---

# 10. Historique

## Version 1.0

- Création du document. Élabore ACT-002-E, section 11, avec une
  taxonomie stable des catégories d'événements (Transition, Fait,
  Notification, Narratif) et leur relation avec les Conséquences
  (ACT-007-A), absentes de la section source. Statut Proposition : n'a
  pas encore traversé les étapes Validée/Spécifiée du cycle de vie
  documentaire d'une mécanique (ACT-001-G, section 14).
