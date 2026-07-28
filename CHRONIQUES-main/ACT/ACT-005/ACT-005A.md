# ACT-005-A — Cibles

> Version : 1.2
>
> Statut : Proposition
>
> Type : Contrat d'architecture
>
> Maturité : 2
>
> Bibliothèque : ACT
>
> Dépendances :
> - ACT-001-B (Principe de ciblage)
> - ACT-001-D (Structure canonique, section Cibles)
> - ACT-001-H (Terminologie officielle, entrée Cible)
> - ACT-002-E (Action Contract, section Inputs)
> - ACT-002-F (Modèle d'exécution, sections 8 et 8bis)
> - ACT-004-A (Acteurs, section 8 --- Auto-ciblage)
>
> Utilisé par :
> - TECH
> - IA
> - QA

---

# 1. Objectif

Définir ce qui qualifie une entité comme Cible d'une Action : ses
catégories, sa multiplicité, son rôle lorsqu'une Action possède plusieurs
Cibles, et ce qui se passe quand l'une d'elles devient invalide en cours
d'exécution.

Ce document élabore le Principe de ciblage déjà posé par ACT-001-B,
section 3, et honore le renvoi explicite laissé ouvert par ACT-004-A,
section 8 (Auto-ciblage), en tranchant sa validité.

---

# 2. Principe

Toute Action possède au moins une Cible --- y compris lorsque cette Cible
est le monde lui-même (ACT-001-B, section 3). Il n'existe pas d'Action
sans Cible : une Action qui semble n'affecter personne en particulier
cible implicitement le monde.

Contrairement à l'Acteur (ACT-004-A, section 7 : exactement un par
Action Instance), une Action peut posséder plusieurs Cibles.

---

# 3. Définition

Une Cible est l'entité concernée par une Action (ACT-001-H). Être Cible
n'implique aucune capacité d'initiative --- une Cible peut être un objet
inerte, une ressource ou une information, catégories qui ne pourraient
jamais qualifier un Acteur (ACT-004-A, section 4).

---

# 4. Catégories officielles

Reprises d'ACT-001-B, section 3, sans modification :

- un acteur ;
- un objet ;
- une ressource ;
- un lieu ;
- une organisation ;
- une information ;
- le monde lui-même.

Comme pour les Acteurs, ce document ne désigne aucune entité concrète du
jeu : cette responsabilité appartient à GDB (ACT-001-G, section 4).

---

# 5. Multiplicité

Une Action référence une ou plusieurs Cibles, sans plafond fixé par ACT.
Un plafond éventuel, s'il est nécessaire, est une Constraint propre à un
Action Contract donné (ACT-002-E, section 6) --- jamais une règle
générale de ce document.

Les Cibles d'une même Action peuvent appartenir à des catégories
différentes (section 4) simultanément, sauf si l'Action Contract
restreint explicitement cette hétérogénéité par une Constraint.

Cette absence de plafond contraste délibérément avec l'unicité stricte
de l'Acteur (ACT-004-A, section 7) : une même personne agit toujours
seule, mais peut affecter plusieurs entités à la fois.

---

# 6. Rôle d'une Cible

ACT-001-D liste « rôle » parmi les champs d'une Cible sans le définir.
Ce document le précise : lorsqu'une Action possède plusieurs Cibles,
chacune y occupe l'un des rôles suivants.

- **Cible principale.** L'entité que l'Action a explicitement pour objet
  d'affecter, désignée par l'Action Definition elle-même --- non par
  l'Intent d'origine. ACT-002-H, section Indépendance, est explicite :
  un Intent ne connaît pas les Actions. Or une Cible est par définition
  une propriété d'une Action (ACT-001-H : « entité concernée par une
  action »), jamais d'un Intent : un Intent ne peut donc pas désigner de
  Cible, seul un Plan qui l'instancie en Actions le peut. Une Action
  possède toujours exactement une Cible principale.
- **Cible secondaire.** Une entité affectée par voie de conséquence de
  l'Action, sans être l'objet de l'Intent (ex. : les personnes présentes
  lors d'une action publique). Une Action peut posséder zéro, une ou
  plusieurs Cibles secondaires.

La distinction importe pour la Résolution (ACT-001-E, étape Résolution) :
l'échec vis-à-vis de la Cible principale détermine l'Outcome de l'Action
(ACT-002-G) ; l'échec vis-à-vis d'une Cible secondaire ne produit qu'un
Effect ou un Event dégradé pour cette Cible seule, sans changer la forme
de l'Outcome global (voir section 8).

---

# 7. Éligibilité d'une Cible

Comme pour l'Acteur (ACT-004-A, section 5), une Cible potentielle doit
satisfaire une éligibilité générale, distincte et antérieure aux
Preconditions propres à une Action donnée.

Une Cible est éligible si :

✓ elle existe encore dans le World au moment de la Validation
(ACT-001-E, étape Validation) ;

✓ son état (ACT-001-D, champ « état ») ne la désigne pas comme
incapable de recevoir une Action de ce type --- la liste exacte des
états disqualifiants par catégorie de Cible relève de GDB, pas d'ACT ;

✓ elle est accessible (ACT-001-D, champ « accessibilité ») dans les
conditions du Contexte de l'Action --- l'accessibilité elle-même est une
notion GDB (ex. : distance, visibilité, droits d'accès), ACT ne fait que
garantir qu'elle est vérifiée avant Validation.

L'absence d'une de ces conditions pour la Cible principale empêche la
création de l'Action Instance, au même titre qu'un Acteur inéligible
(ACT-004-A, section 5). Son absence pour une Cible secondaire n'empêche
pas la création : cette Cible est simplement retirée de la liste avant
Validation --- une Action peut perdre des Cibles secondaires sans jamais
en perdre sa Cible principale sans échouer.

---

# 8. Perte d'éligibilité en cours d'exécution

ACT-002-F, section 8bis, traite déjà « la cible devient invalide » comme
une cause d'échec de disparition, au même titre que la disparition de
l'Acteur --- mais ce traitement suppose implicitement une seule Cible.
Ce document précise le cas à plusieurs Cibles, sans modifier la règle
existante pour le cas à une seule Cible :

- si la Cible principale disparaît ou devient invalide pendant
  l'Exécution, l'Action suit intégralement ACT-002-F section 8bis
  (Échec de disparition) --- rien ne change ;
- si une Cible secondaire disparaît ou devient invalide pendant
  l'Exécution, l'Action se poursuit sans elle. Les Effects et Events déjà
  produits à son égard restent valides ; ceux qui en dépendaient encore
  sont annulés pour cette Cible seule --- l'Action dans son ensemble ne
  passe pas à FAILED (ACT-001-F) pour cette seule raison.

---

# 9. Auto-ciblage

ACT-004-A, section 8, laissait ce point ouvert. Il est tranché ici :
un Acteur peut être sa propre Cible sans restriction ni permission
supplémentaire --- ACT-001-B, section 3, autorise déjà explicitement
qu'une Cible soit un acteur, sans distinguer le cas où cet acteur est
celui-là même qui initie l'Action.

L'auto-ciblage ne fusionne jamais les deux rôles en un seul concept :
Acteur et Cible restent deux rôles distincts (ACT-004-A, section 3 ;
présent document, section 3), même lorsqu'une seule entité les occupe
tous les deux pour une Action donnée.

---

# 10. Contrat

Une Action Instance ne peut jamais être créée sans au moins une Cible
identifiable et éligible (section 7), dont exactement une porte le rôle
de Cible principale (section 6).

La perte d'une Cible secondaire ne peut jamais, à elle seule, faire
échouer une Action Instance (section 8).

---

# 11. Contrat TECH

Le moteur doit être capable de :

- vérifier l'existence et l'éligibilité de chaque Cible avant Validation ;
- distinguer Cible principale et Cibles secondaires dans l'Action
  Instance ;
- appliquer ACT-002-F section 8bis intégralement si la Cible principale
  disparaît ;
- retirer une Cible secondaire devenue invalide sans interrompre
  l'Action, en annulant uniquement les Effects qui en dépendaient.

---

# 12. Contrat QA

Les tests devront vérifier :

✓ qu'une Action Instance ne peut pas être créée sans Cible ;

✓ qu'une Action Instance ne peut pas être créée avec une Cible principale
inéligible ;

✓ qu'une Cible secondaire inéligible est retirée sans empêcher la
création de l'Action Instance ;

✓ que la disparition d'une Cible secondaire en cours d'Exécution
n'entraîne pas l'échec de l'Action dans son ensemble ;

✓ qu'un Acteur peut valablement être sa propre Cible.

---

# 13. Critères de validation

Ce document est conforme si :

✓ il n'introduit aucun axiome déjà posé par ACT-001-B ou ACT-001-H ;

✓ il ne redéfinit aucune règle déjà couverte par ACT-002-E ou ACT-002-F ;

✓ il tranche explicitement le renvoi laissé ouvert par ACT-004-A,
section 8 ;

✓ il laisse à GDB la responsabilité des états et de l'accessibilité
concrets par catégorie de Cible.

---

# 14. Historique

## Version 1.2

- audit formel (méthodologie MASTER-008), deux constats :
  1. Ajout du champ obligatoire `Maturité` à l'en-tête, absent depuis la
     création --- non-conformité à MASTER-004. Valeur retenue : 2
     (Spécification), même justification que ACT-004-A v1.2.
  2. Resserrement de la citation section 6 (Rôle d'une Cible) : la
     correction v1.1 citait ACT-002-H (section Indépendance) comme
     support direct de « un Intent ne connaît jamais de cible », alors
     que cette section dit littéralement que l'Intent ne connaît pas les
     *Actions*, pas explicitement pas les Cibles. La chaîne logique
     complète est désormais explicite : Intent ne connaît pas les
     Actions (ACT-002-H) --- une Cible est une propriété d'une Action
     (ACT-001-H) --- donc un Intent ne peut pas porter de Cible.

## Version 1.1

- correction du constat ACT-005-C01 (relecture interne) : la section 6
  (Rôle d'une Cible) attribuait à tort la désignation de la Cible
  principale à l'Intent d'origine, en citant ACT-002-H à l'appui. Or
  ACT-002-H (section Indépendance) est explicite : un Intent ne connaît
  jamais de cible, seul le résultat recherché. La Cible principale est
  désormais définie comme désignée par l'Action Definition elle-même, pas
  par l'Intent.

## Version 1.0

- Création du document. Élabore ACT-001-B section 3 et ACT-001-H (entrée
  Cible) avec des règles de multiplicité, de rôle, d'éligibilité et de
  perte d'éligibilité absentes des deux documents source. Tranche le
  renvoi laissé ouvert par ACT-004-A section 8 (Auto-ciblage). Statut
  Proposition : n'a pas encore traversé les étapes Validée/Spécifiée du
  cycle de vie documentaire d'une mécanique (ACT-001-G, section 14).
