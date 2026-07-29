# ACT-007-A — Taxonomie des Conséquences

> Version : 1.1
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
> - ACT-001-B, section 6 (Principe de conséquence)
> - ACT-002-E, sections 10 et 11 (Effects, Events)
> - ACT-002-G (Outcome)
> - ACT-005-A (Cibles, sections 6 et 8)
> - ENGINE-001 (Journal d'événements du World)
>
> Utilisé par :
> - TECH
> - IA
> - QA

---

# 1. Objectif

Établir une taxonomie stable des catégories de Conséquences, et les
règles de composition lorsqu'une Action en produit plusieurs à la fois.

Ce document n'introduit aucun nouvel axiome. Il structure le Principe de
conséquence posé par ACT-001-B, section 6 --- « toute action modifie
l'état du monde [...] aucune action n'est totalement neutre » --- déjà
intégré au Modèle universel par ACT-002-E, sections 10 et 11 (Effects,
Events), sans en modifier la sémantique ni la place dans l'Action
Contract.

---

# 2. Principe

Une Conséquence est ce que produit une Action une fois résolue --- jamais
avant. ACT-002-G est explicite : l'Outcome précède les Effets et ne les
connaît pas ; ce document ne s'applique donc jamais à l'Outcome
lui-même, seulement à ce qui en découle une fois qu'il est connu.

Une Conséquence n'est jamais optionnelle par nature : même un Échec ou
une Interruption en produisent (ACT-001-B, section 6). Ce qui varie
selon la forme de l'Outcome, ce n'est pas l'existence d'une Conséquence,
mais son ampleur et sa catégorie (section 6).

---

# 3. Catégories stables

**Matérielle.** Modification d'un objet, d'une ressource, ou d'un
Component d'une Entity. Exemples : un objet détruit, une ressource
consommée, une valeur de State modifiée.

**Relationnelle.** Modification d'une Relation entre deux Entity.
Exemples : une opinion qui change, une dette contractée, une alliance
rompue.

**Informationnelle.** Une connaissance nouvellement accessible à une ou
plusieurs Entity. Exemples : un secret découvert, une rumeur propagée,
une carte révélée.

**Statutaire.** Changement d'état ou d'étape de vie d'une Entity.
Exemples : un Lifecycle qui progresse (ACT-004-A ne couvre que
l'Acteur ; ce cas concerne toute Entity), un titre acquis ou perdu.

**Narrative.** Progression dans une trame prévue par GDB --- symétrique
de la catégorie Narratif des Conditions (ACT-006-A, section 3).
Exemples : une quête qui avance, un événement du monde déclenché.

---

# 4. Dimensions transverses

Contrairement aux Conditions (ACT-006-A), où chaque catégorie suffit à
elle seule, une Conséquence se qualifie toujours par sa catégorie
**et** par trois dimensions indépendantes, qui peuvent varier librement
entre elles.

## Temporalité

**Immédiate.** Appliquée dès la production des Effets, dans le même
Tick que la Résolution (ACT-001-E, étape Production des effets).

**Différée.** Programmée pour un Tick futur au moment de la Résolution,
mais déjà entièrement déterminée à cet instant --- son contenu ne dépend
d'aucun événement intermédiaire (le déterminisme de l'Outcome, ACT-002-G,
l'exige). Une Conséquence différée n'est jamais une Conséquence
recalculée plus tard : sa valeur est fixée à la Résolution, seule son
application est reportée.

## Réversibilité

**Réversible.** Une Action ultérieure peut ramener l'état affecté à sa
valeur antérieure.

**Irréversible.** Aucune Action ne peut annuler cette Conséquence ---
seule une autre Conséquence peut en compenser les effets, jamais les
effacer (ex. : la disparition d'une Entity --- ACT-004-A, section 5,
l'utilise comme exemple d'état disqualifiant un Acteur, sans se
prononcer sur sa réversibilité --- est typiquement de cette nature : un
nouvel Acteur peut hériter d'un rôle similaire, il ne ressuscite pas
l'ancien).

## Portée

**Locale.** N'affecte que les Entity directement impliquées dans
l'Action --- son Acteur et ses Cibles (ACT-004-A ; ACT-005-A, section 6).

**Globale.** Affecte l'état du monde au-delà des Entity impliquées
(ex. : une variation de marché, un climat social). Une Conséquence
globale reste toujours rattachée à l'Action qui l'a produite --- elle
n'apparaît jamais spontanément sans Action origine (ACT-001-B, section 6).

---

# 5. Conséquences directes et indirectes

Une Conséquence est **directe** si elle affecte la Cible principale de
l'Action (ACT-005-A, section 6), **indirecte** si elle affecte une
Cible secondaire ou une Entity tierce non ciblée par l'Action elle-même.

Cette distinction est indépendante des dimensions de la section 4 : une
Conséquence directe peut être différée, une Conséquence indirecte peut
être irréversible. Elle détermine seulement la responsabilité causale
--- utile pour toute future mécanique de réputation ou de traçabilité
(hors périmètre de ce document).

---

# 6. Composition selon la forme de l'Outcome

ACT-002-G définit quatre formes d'Outcome (Réussite, Réussite partielle,
Échec, Interruption). Ce document précise comment chacune détermine
l'ensemble des Conséquences réellement produites, sans jamais modifier
la définition de ces formes.

**Réussite.** Toutes les Conséquences prévues par l'Action Contract
(ACT-002-E) sont produites intégralement.

**Réussite partielle.** Un sous-ensemble strict des Conséquences
prévues est produit --- jamais l'ensemble complet, jamais aucune. Lequel
exactement dépend de l'Action Contract concerné, pas de ce document
(ACT-002-E reste seul responsable de définir ce sous-ensemble pour
chaque Action).

**Échec.** Aucune des Conséquences visées par l'Intent n'est produite,
mais l'Échec lui-même en produit --- toujours au moins une Conséquence
Informationnelle ou Relationnelle (ex. : une tentative d'action devient
un fait observable, même ratée), jamais aucune Conséquence Matérielle
visée par l'Intent d'origine.

**Interruption.** Seules les Conséquences déjà appliquées avant
l'interruption (ACT-001-E, section 5 --- Interruptions) subsistent ---
aucune Conséquence prévue pour une étape non atteinte n'est produite,
qu'elle soit Immédiate ou Différée.

---

# 7. Contrat

Une Action ne peut jamais produire zéro Conséquence, quelle que soit la
forme de son Outcome --- y compris un Échec ou une Interruption
(ACT-001-B, section 6).

Une Conséquence Différée reste entièrement déterminée au moment de sa
programmation ; son application ultérieure ne réévalue jamais son
contenu en fonction de l'état du monde à ce moment futur.

Une Conséquence Irréversible ne peut jamais être annulée par une
Conséquence produite par une Action ultérieure --- seule une
compensation explicite est possible, jamais une annulation.

---

# 8. Contrat TECH

Le moteur doit être capable de :

- catégoriser chaque Conséquence selon les sections 3, 4 et 5 ;
- produire au moins une Conséquence pour tout Outcome, y compris Échec
  et Interruption ;
- programmer une Conséquence Différée avec un contenu figé à la
  Résolution, appliqué sans recalcul au Tick prévu ;
- refuser toute opération qui annulerait une Conséquence marquée
  Irréversible.

---

# 9. Contrat QA

Les tests devront vérifier :

✓ qu'un Échec produit toujours au moins une Conséquence, jamais aucune ;

✓ qu'une Interruption ne produit que les Conséquences déjà appliquées
avant l'arrêt, jamais celles d'une étape non atteinte ;

✓ qu'une Conséquence Différée appliquée plus tard correspond exactement
à ce qui a été programmé à la Résolution, sans dérive ;

✓ qu'une Conséquence Irréversible ne peut jamais être défaite par une
Action ultérieure, seulement compensée.

---

# 10. Critères de validation

Ce document est conforme si :

✓ il n'introduit aucun axiome déjà posé par ACT-001-B, section 6 ;

✓ il ne redéfinit aucune règle déjà couverte par ACT-002-E, sections 10
et 11, ni par ACT-002-G (Outcome) ;

✓ il ne redéfinit jamais le mécanisme concret de publication des Events,
déjà couvert par ENGINE-001 ;

✓ la taxonomie qu'il propose est complète et extensible, sur le même
modèle qu'ACT-006-A.

---

# 11. Historique

## Version 1.1

- audit formel (méthodologie MASTER-008), deux constats corrigés avant
  livraison : (1) section 4, Réversibilité --- la citation attribuait à
  tort à ACT-004-A, section 6, une affirmation sur l'irréversibilité de
  la mort qu'elle ne contient pas ; ACT-004-A section 5 utilise
  seulement la mort comme exemple d'état disqualifiant, sans se
  prononcer sur sa réversibilité --- reformulé pour ne plus sur-attribuer
  cette affirmation. (2) section 4, référence à ACT-001-E précisée
  (section 5, Interruptions) plutôt qu'une description vague. Une
  coquille de label également corrigée (« Narrative » → « Narratif »,
  pour respecter l'orthographe exacte du label utilisé par ACT-006-A).

## Version 1.0

- Création du document. Élabore ACT-001-B, section 6 et ACT-002-E,
  sections 10 et 11 avec une taxonomie stable des catégories de
  Conséquences et des règles de composition selon la forme de l'Outcome
  (ACT-002-G), absentes des trois sections sources. Statut Proposition :
  n'a pas encore traversé les étapes Validée/Spécifiée du cycle de vie
  documentaire d'une mécanique (ACT-001-G, section 14).
