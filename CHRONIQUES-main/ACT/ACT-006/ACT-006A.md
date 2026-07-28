# ACT-006-A — Taxonomie des Conditions

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
> - ACT-001-B, section 5 (Principe de conditions)
> - ACT-002-E, sections 5 et 6 (Preconditions, Constraints)
> - ACT-004-A (Acteurs)
> - ACT-005-A (Cibles)
>
> Utilisé par :
> - TECH
> - IA
> - QA

---

# 1. Objectif

Établir une taxonomie stable des catégories de Conditions, distincte de
la simple liste d'exemples donnée par ACT-001-B, section 5 (Principe de
conditions).

Ce document n'introduit aucun nouvel axiome. Il structure le Principe de
conditions posé par ACT-001-B et déjà intégré au Modèle universel par
ACT-002-E, sections 5 et 6 (Preconditions, Constraints) --- sans en
modifier la sémantique ni la place dans l'Action Contract.

---

# 2. Principe

Une Condition limite l'éligibilité d'une Action --- distincte de
l'éligibilité générale des Acteurs et des Cibles impliqués
(ACT-004-A, section 5 ; ACT-005-A, section 7). Une Action à Acteur et
Cible éligibles peut rester globalement inéligible par ses Conditions.

Les Conditions ne sont jamais des propriétés de l'Acteur ou de la Cible
pris isolément. Elles contraignent leur relation à travers l'Action :
possession (l'Acteur a-t-il l'objet requis), prérequis (la Cible
est-elle dans l'état requis), coût (l'Acteur a-t-il les ressources
requises), ou contrainte (la relation entre Acteur et Cible est-elle
possible ici et maintenant).

---

# 3. Catégories stables

**Physique.** L'état du monde rend-il l'Action possible ? Exemples :
distance (Cible hors de portée), obstacles (Cible inaccessible),
intégrité (Cible déjà détruite).

**Possession.** L'Acteur dispose-t-il des moyens requis ? Exemples :
posséder un outil, maîtriser une compétence, connaître une information.

**Coût.** L'Acteur peut-il s'acquitter de la dépense ? Toujours une
quantité consommée : endurance, argent, points d'action, matière
première.

**État.** La Cible est-elle dans une configuration compatible ?
Exemples : être vivant (Cible morte), être éveillé (Cible endormie),
stade de maturité (récolter un champ).

**Légal.** L'Action est-elle autorisée par les règles en vigueur ?
Exemples : propriété (Cible appartenant à autrui), consentement (accord
nécessaire), droit d'accès (autorisation invalide).

**Social.** L'Action est-elle acceptable par les normes du contexte ?
Exemples : opinion (Cible hostile à l'Acteur), égalité (Cible de rang
supérieur), coutume (geste tabou).

**Temporel.** Le moment est-il propice ? Exemples : jour/nuit, phase
lunaire, saison, jour de la semaine, heure précise.

**Narratif.** L'Action s'inscrit-elle dans la trame prévue ? Exemples :
quête non commencée, événement non survenu, étape manquante, Acteur non
impliqué.

---

# 4. Unicité

Une Condition n'appartient qu'à une seule catégorie. Lorsqu'un critère
pourrait relever de plusieurs (par exemple l'âge, à la fois État et
Temporel), c'est la nature profonde de la contrainte, non son apparence,
qui détermine la catégorie. Pour l'âge : si le simple écoulement du
temps suffit à lever la Condition, elle est Temporelle ; si l'Acteur
doit accomplir une Action supplémentaire (ex. : un rite de passage)
pour débloquer l'accès malgré son âge, elle est d'État.

---

# 5. Polarité

Une Condition peut exiger la présence ou l'absence d'un critère, sans
changer de catégorie. Par exemple, devoir être à moins de 3 mètres ou à
plus de 10 mètres d'une Cible sont deux Conditions Physiques ; « ne pas
détenir un objet précis » ou « ne pas avoir accompli une quête » restent
des Conditions de Possession et Narratives respectivement.

---

# 6. Héritage

Une Action hérite les Conditions des entités dont elle dépend : son
Acteur, sa Cible, et toute entité tierce impliquée (Ressource, Lieu...).
Par exemple, si un Lieu requiert une clé pour entrer (État), toute
Action ciblant une entité présente dans ce Lieu hérite de cette
Condition --- en plus des siennes propres. De même, une Cible protégée
par un statut légal (ex. : Monument Historique) transmet cette Condition
à toute Action qui la modifierait. Les Conditions d'une entité
s'ajoutent à celles de l'Action sans s'y substituer.

---

# 7. Éligibilité globale

Pour qu'une Action soit globalement éligible, toutes ses Conditions
doivent être remplies simultanément : son Acteur doit être éligible
(ACT-004-A, section 5), sa Cible doit être éligible (ACT-005-A,
section 7), et ses Conditions propres (Preconditions + Constraints) du
présent document doivent être satisfaites --- le tout au même instant.

L'échec d'une seule Condition suffit à invalider l'ensemble, quelle que
soit sa catégorie ou son origine (Acteur, Cible, tiers, ou Action
elle-même). Une Action dont l'Acteur n'a plus l'énergie requise (Coût)
n'est pas plus éligible que celle dont la Cible vient d'être détruite
(Physique) ou celle que l'Acteur n'a pas encore le droit d'initier
(Narratif).

---

# 8. Contrat

Une Action ne peut jamais devenir éligible par la seule éligibilité de
son Acteur et de sa Cible : une Condition non remplie invalide toujours
l'ensemble.

Une Condition ne peut jamais introduire une possibilité d'Action
interdite par l'éligibilité de l'Acteur ou de la Cible : les Conditions
s'ajoutent aux restrictions d'éligibilité, elles ne s'y substituent pas.

Une Condition manquante produit toujours un échec de type « invalidité
interne » au sens d'ACT-002-F, section 8bis --- distinct d'une
disparition d'Acteur ou de Cible en cours d'exécution.

---

# 9. Contrat TECH

Le moteur doit être capable de :

- vérifier chaque Condition individuellement avant exécution ;
- vérifier simultanément les éligibilités Acteur/Cible et l'ensemble des
  Conditions propres à l'Action ;
- refuser d'exécuter une Action dont une seule Condition manque, comme
  une « invalidité interne » (ACT-002-F, section 8bis) --- sans la
  confondre avec une disparition ;
- collecter toutes les Conditions héritées des entités tierces
  impliquées (Ressource, Lieu...), en plus de celles explicitement
  déclarées par l'Action.

---

# 10. Contrat QA

Les tests devront vérifier :

✓ qu'une Action dont une seule Condition manque reste non éligible,
quelle que soit la catégorie manquante ;

✓ que la vérification des Conditions est distincte de celle des
éligibilités Acteur/Cible, et que les deux restent requises
simultanément ;

✓ que l'échec d'une Condition produit bien une « invalidité interne »,
distincte d'une disparition ;

✓ que les Conditions des entités tierces impliquées (Ressource,
Lieu...) sont bien collectées et combinées aux Conditions explicites de
l'Action.

---

# 11. Critères de validation

Ce document est conforme si :

✓ il n'introduit aucun axiome déjà posé par ACT-001-B, sections 5 et 6 ;

✓ il ne redéfinit aucune règle déjà couverte par ACT-002-E, sections 5
et 6 ;

✓ il n'empiète pas sur les règles d'éligibilité de l'Acteur et de la
Cible déjà couvertes par ACT-004-A, section 5 et ACT-005-A, section 7 ;

✓ la taxonomie qu'il propose est complète (toute Condition existante
appartient à exactement une catégorie stable) et extensible (l'ajout
d'une nouvelle catégorie ne perturbe pas les autres).

---

# 12. Historique

## Version 1.1

- audit formel (méthodologie MASTER-008) : une coquille mineure trouvée
  et corrigée, aucun constat de fond. Toutes les citations de dépendances
  (ACT-001-B, ACT-002-E, ACT-004-A, ACT-005-A) vérifiées et validées. Les
  sections Contrat TECH et Contrat QA sont suffisamment précises pour le
  niveau de Maturité 2 (Spécification) déjà présent dans l'en-tête.

## Version 1.0

- Création du document. Élabore ACT-001-B, section 5 et ACT-002-E,
  sections 5 et 6 avec une taxonomie stable des catégories de Conditions,
  absente des trois sections sources. Statut Proposition : n'a pas encore
  traversé les étapes Validée/Spécifiée du cycle de vie documentaire
  d'une mécanique (ACT-001-G, section 14).