# ACT — Catalogue

> Version : 1.5
>
> Statut : Foundation
>
> Bibliothèque : ACT
>
> Dépendances : MASTER, GDB
>
> Utilisée par : TECH, QA, UX

---

# Objectif

Ce catalogue référence l'ensemble des documents constituant la bibliothèque ACT.

ACT définit le langage universel des actions de Chroniques.

Chaque document appartient à une catégorie clairement identifiée.

Ce catalogue distingue explicitement ce qui existe dans le dépôt aujourd'hui de ce qui est planifié mais non encore créé. Un chapitre planifié n'est pas un chapitre audité : tant qu'il n'existe pas, il n'y a rien à auditer, seulement à créer.

---

# Structure générale

ACT

├── Fondements                (existant --- ACT-001)
├── Modèle universel          (existant --- ACT-002)
├── Cycle de vie              (retiré --- voir section « Chapitre retiré »)
├── Acteurs                   (créé --- ACT-004, Statut : Proposition)
├── Cibles                    (créé --- ACT-005, Statut : Proposition)
├── Conditions                (créé --- ACT-006-A, v1.1 audité --- voir note sur le périmètre restreint)
├── Conséquences              (créé --- ACT-007-A, v1.1 audité --- voir note sur le périmètre restreint)
├── Taxonomie                 (créé --- ACT-008-A, v1.0 audité --- voir note sur le périmètre restreint)
├── Composition                (créé --- ACT-009-A, v1.1 audité --- voir note sur la frontière avec le Plan)
├── Événements                (créé --- ACT-010-A, v1.0 audité --- voir note sur le périmètre restreint)
├── Patterns                  (planifié, non créé --- PATTERNS/)
└── Verbes                    (planifié, non créé --- VERBS/)

---

# Documents existants

## ACT-001 --- Fondements de l'action

Statut : Créé et audité.

Sections A à I. Définit la philosophie générale, les principes fondamentaux, la
définition universelle et le modèle canonique de l'action, son cycle de vie et
ses états, le périmètre de la bibliothèque, sa terminologie et ses références.

## ACT-002 --- Modèle universel de l'action

Statut : Créé et audité.

Sections A à J. Décrit la structure commune à toutes les actions : niveaux
d'abstraction, relations entre niveaux, définition et instanciation, Action
Contract, modèle d'exécution, Outcome, Intent, Plan, et gouvernance du modèle.

---

# Chapitre retiré

## ACT-003 --- Cycle de vie (retiré de la structure cible)

La version 1.1 de ce catalogue avertissait : *« avant de créer ACT-003,
vérifier qu'il n'en résultera pas une redondance avec [ACT-001-E et
ACT-002-F à ACT-002-I]. »* Cette vérification a été faite. Constat :

- `ACT-001-E` définit déjà la machine à états complète d'une action
  (Création → Validation → Planification → Préparation → Exécution →
  Résolution → Production des effets → Publication des événements → Mise à
  jour du monde → Archivage), avec les contrats TECH/IA/QA associés et les
  règles d'interruption, de suspension et d'annulation.
- `ACT-002-F`, section 3bis, relie explicitement ce cycle à Intent → Plan →
  Action Instance → Execution Engine → Effects → Events → World Update →
  Outcome, avec la règle de non-remontée d'un Outcome vers l'Intent
  d'origine.
- `ACT-002-I` autorise déjà des étapes de Plan séquentielles, parallèles,
  optionnelles ou conditionnelles --- le Plan n'est pas la séquence linéaire
  qu'on pourrait croire en lisant ACT-002 isolément.

Conclusion du test de non-duplication (ACT-001-G, section 13, test 4) :
aucun contenu réel ne resterait à écrire dans un ACT-003 « Cycle de vie »
sans reformuler ACT-001-E et ACT-002-F à l'identique. ACT-003 est donc
retiré de la structure cible plutôt que créé pour la forme. Si un besoin
réel et distinct apparaît un jour (par exemple une machine à états propre
à un type d'action non couvert par le cycle générique), il sera documenté
sous un nouvel identifiant, jamais en réutilisant ACT-003 comme si de rien
n'était (MASTER-006 : une décision qui ne peut être tranchée est
explicitement ajournée, elle ne réapparaît pas sous son ancien nom sans
trace du changement).

Les identifiants ACT-004 à ACT-010 ci-dessous ne sont donc pas renumérotés :
un identifiant retiré reste retiré, il n'est jamais réattribué. Cette règle
n'est pas (encore) écrite dans MASTER-004 --- c'est une convention retenue
par l'équipe le jour où ce cas s'est présenté, dont le coût (renumérotage
de toutes les références croisées) dépasse le seul bénéfice cosmétique
d'une numérotation sans trou (voir Historique, version 1.3).

---

# Chapitres créés, non encore audités

Les chapitres suivants existent dans le dépôt (Statut : Proposition) mais
n'ont pas encore traversé les étapes Validée/Spécifiée du cycle de vie
documentaire d'une mécanique (ACT-001-G, section 14). Ils ne sont donc pas
comptés comme « audités » au sens d'AUDIT-GLOBALE.md tant qu'une relecture
d'équipe ne les a pas fait passer au statut Officiel.

## ACT-004 --- Acteurs

Décrit les entités capables d'initier des actions.

Vérification de non-duplication (ACT-001-G, section 13, test 4) : ACT-001-B
section 2 (Principe de responsabilité) et ACT-001-H (entrée « Acteur » du
glossaire) posent l'axiome --- « toute action possède un acteur identifiable »
--- et une liste de catégories, mais aucun des deux ne définissait les règles
d'éligibilité (quand un Acteur cesse-t-il d'être valide), la multiplicité
(une action à plusieurs Acteurs) ni le contrat vis-à-vis d'ACT-002-E
(Inputs) et ACT-002-F (échec de disparition). Ce contenu n'existait encore
nulle part : ACT-004 n'est pas redondant.

## ACT-005 --- Cibles

Décrit les entités pouvant recevoir une action.

Même constat que pour ACT-004 : ACT-001-B section 3 (Principe de ciblage)
et ACT-001-D (section « Cibles » du modèle canonique : type, rôle, état,
accessibilité) posaient l'axiome et une liste de champs, sans définir les
règles de multiplicité, le rôle exact d'une cible (principale/secondaire),
l'éligibilité par type de cible, ni le cas d'une cible devenant invalide en
cours d'exécution lorsqu'une Action en possède plusieurs. ACT-005 tranche
aussi explicitement le renvoi laissé ouvert par ACT-004, section 8
(Auto-ciblage). ACT-005 n'est pas redondant.

## ACT-006 --- Conditions

Décrit les prérequis nécessaires à l'exécution.

**Périmètre restreint par rapport à la version 1.1 de ce catalogue.**
ACT-002-E (Action Contract, sections 5 et 6 --- Preconditions et
Constraints) et ACT-001-B section 5 (Principe de conditions) couvrent déjà
la place des conditions dans le contrat d'une action et leurs catégories
(matérielles, sociales, économiques, juridiques, environnementales,
temporelles, physiologiques, psychologiques). ACT-006 ne redéfinit pas ce
que sont les Preconditions/Constraints ; il couvre ce qui manquait : une
taxonomie stable des catégories de conditions (au-delà de la simple
liste), et les règles de composition de plusieurs conditions entre elles
(unicité par catégorie, polarité, héritage entre entités liées). ACT-006
n'est pas redondant.

## ACT-007 --- Conséquences

Décrit les effets produits par une action.

**Périmètre restreint par rapport à la version 1.1 de ce catalogue**, pour
la même raison qu'ACT-006 : ACT-002-E (sections 10 et 11 --- Effects et
Events) et ACT-001-B section 6 (Principe de conséquence) couvrent déjà la
place des effets et événements dans le contrat d'une action. ACT-007 ne
redéfinit pas Effects/Events ; il couvre une taxonomie des catégories de
conséquences (matérielle, relationnelle, informationnelle, statutaire,
narrative), trois dimensions transverses (temporalité, réversibilité,
portée), et les règles de composition selon la forme de l'Outcome
(ACT-002-G), qui n'existaient nulle part. ACT-007 n'est pas redondant.

## ACT-008 --- Taxonomie des verbes

Décrit les règles d'organisation des Verbes en familles partageant un
même Pattern.

Vérification de non-duplication : ACT-002-B (définitions de Principe,
Pattern, Verbe) et ACT-002-C (relations autorisées entre niveaux,
sections 3, 4, 8) posent déjà les définitions et la relation de
spécialisation, mais aucun des deux ne définit la multiplicité
Pattern/Verbe, le critère de création d'un nouveau Verbe, ni la règle de
non-polysémie. Ce document n'énumère aucun Verbe concret --- cette
responsabilité reste à VERBS, pilotée par GDB. ACT-008 n'est pas
redondant.

## ACT-009 --- Composition d'Actions

Décrit la combinaison d'Actions simples en Actions complexes.

Vérification de non-duplication : ACT-002-C, section 6, pose déjà
l'axiome (« une Action peut être composée de plusieurs Actions ») avec un
exemple, mais sans règle de propagation d'échec, d'agrégation de
l'Outcome ni d'héritage du Contexte --- et surtout sans trancher la
frontière avec le Plan (ACT-002-I), qui décrit lui aussi plusieurs
Actions liées entre elles. ACT-009 comble ce vide et tranche cette
frontière explicitement. ACT-009 n'est pas redondant.

## ACT-010 --- Taxonomie des événements

Décrit les catégories d'événements qu'une Action peut publier et leur
relation avec les Conséquences (ACT-007).

Vérification de non-duplication : ACT-002-E, section 11, définit déjà ce
qu'est un Event dans l'Action Contract, et ENGINE-001 définit déjà le
mécanisme concret de publication --- mais aucun des deux ne propose de
taxonomie des catégories conceptuelles d'événements. ACT-010 ne redéfinit
ni l'un ni l'autre. ACT-010 n'est pas redondant.

---

# Chapitres planifiés, non créés

Aucun chapitre numéroté d'ACT ne reste planifié à ce stade --- ACT-001 à
ACT-010 sont désormais tous créés (ACT-003 excepté, retiré). Seules les
bibliothèques PATTERNS et VERBS, distinctes du présent catalogue de
chapitres, restent à créer (voir sections dédiées ci-dessous).

---

# Bibliothèque PATTERNS (planifiée, non créée)

Les patterns représenteront les modèles génériques de gameplay.

Un pattern pourra être partagé par plusieurs verbes.

Exemples envisagés, à confirmer au moment de la création effective :

PAT-001 Influence

PAT-002 Transformation

PAT-003 Transfert

PAT-004 Déplacement

PAT-005 Observation

PAT-006 Communication

PAT-007 Contrainte

PAT-008 Création

PAT-009 Destruction

PAT-010 Coopération

Cette liste pourra évoluer, mais chaque nouveau pattern devra démontrer qu'il apporte une mécanique réellement distincte.

---

# Bibliothèque VERBS (planifiée, non créée)

Chaque verbe représentera une spécialisation d'un pattern.

Exemple envisagé :

PAT-001

↓

VERB-004 Convaincre

↓

Action exécutée

---

# Dépendances

MASTER

↓

GDB

↓

ACT

↓

TECH

↓

CODE

---

# Évolution

Toute nouvelle mécanique devra respecter les principes suivants :

- ne pas dupliquer un pattern existant ;
- ne pas créer un verbe si une composition de verbes couvre déjà le besoin ;
- documenter les impacts sur TECH ;
- documenter les impacts QA ;
- mettre à jour ce catalogue, y compris la distinction existant / planifié.

---

# Références

MASTER

GDB

TECH

QA

UX

---

# Historique

## Version 1.5

- `ACT-008-A` (Taxonomie des verbes) créé --- règles de multiplicité
  Pattern/Verbe, critère de nouveau Verbe en quatre tests, non-polysémie ;
  n'énumère aucun Verbe concret (réservé à VERBS, piloté par GDB) ;
- `ACT-009-A` (Composition d'Actions) créé --- règles de propagation
  d'échec, d'agrégation de l'Outcome, d'héritage du Contexte, et
  surtout tranche explicitement la frontière avec le Plan (ACT-002-I),
  qui n'était pas résolue depuis la création d'ACT-002. Audit formel :
  1 constat corrigé avant livraison (imprécision de citation sur le
  vocabulaire de réévaluation d'un Plan) --- voir l'Historique
  d'ACT-009-A ;
- `ACT-010-A` (Taxonomie des événements) créé --- catégories
  conceptuelles d'événements et leur relation avec les Conséquences
  (ACT-007), sans redéfinir le mécanisme déjà couvert par ACT-002-E §11
  et ENGINE-001 ;
- ACT-001 à ACT-010 sont désormais tous créés (ACT-003 excepté, retiré).
  Seules les bibliothèques PATTERNS et VERBS restent à créer.

## Version 1.4

- `ACT-007-A` (Conséquences) créé --- taxonomie (matérielle,
  relationnelle, informationnelle, statutaire, narrative), trois
  dimensions transverses (temporalité, réversibilité, portée), et
  composition selon la forme de l'Outcome (ACT-002-G), qui n'existaient
  nulle part. Audit formel : 2 constats trouvés et corrigés avant
  livraison (citation erronée sur l'irréversibilité, référence imprécise
  à ACT-001-E) --- voir l'Historique d'ACT-007-A ;
- correction d'un oubli constaté en traitant ACT-007 : la sous-section
  `## ACT-006 --- Conditions` était restée dans « Chapitres planifiés,
  non créés » alors qu'ACT-006 est créé et audité depuis la v1.3 --- la
  structure générale du catalogue le disait déjà correctement, seule
  cette sous-section descriptive ne l'avait jamais suivie. Déplacée vers
  « Chapitres créés, non encore audités », aux côtés d'ACT-004/005/007,
  texte remis au présent.

## Version 1.3

- correction d'une citation erronée introduite en version 1.2 : la règle
  « un identifiant retiré n'est jamais réattribué » y était attribuée à
  MASTER-004, qui ne la contient pas. La règle reste appliquée --- le coût
  d'un renumérotage (retrouver et corriger chaque référence croisée) dépasse
  son seul bénéfice cosmétique, et un précédent existe déjà avec GDB-001I-2
  --- mais elle n'est plus présentée comme déjà écrite ailleurs. Sa
  formalisation officielle dans MASTER-004 a été proposée à l'équipe et n'a
  pas été retenue pour l'instant ;
- `ACT-004` (Acteurs) marqué comme créé dans la structure générale : la
  version 1.2 avait rédigé le document sans mettre à jour son propre statut
  dans ce catalogue, laissant « planifié, non créé » à tort ;
- `ACT-005` (Cibles) créé --- élabore ACT-001-B section 3 et ACT-001-D/H avec
  des règles de multiplicité, de rôle (principale/secondaire), d'éligibilité
  par Cible et de perte d'éligibilité en cours d'exécution pour une Action à
  Cibles multiples ; tranche le renvoi laissé ouvert par ACT-004, section 8
  (Auto-ciblage).

## Version 1.2

- retrait d'ACT-003 (« Cycle de vie ») de la structure cible, après vérification
  effective de la redondance déjà signalée en version 1.1 : le contenu annoncé
  est intégralement couvert par ACT-001-E et ACT-002-F à ACT-002-I. L'identifiant
  ACT-003 n'est pas réattribué (MASTER-004) ;
- confirmation qu'ACT-004 (Acteurs) et ACT-005 (Cibles) ne font pas doublon :
  ACT-001-B et ACT-001-H/D ne posent que l'axiome et un placeholder de structure,
  jamais les règles d'éligibilité, de multiplicité ou les cas limites ;
- restriction du périmètre annoncé d'ACT-006 (Conditions) et ACT-007
  (Conséquences), déjà partiellement couverts par ACT-002-E (Preconditions,
  Constraints, Effects, Events) : ces deux chapitres devront se limiter à une
  taxonomie et à des règles de composition, pas à une redéfinition des
  Preconditions/Effects.

## Version 1.1

- distinction explicite entre chapitres/dossiers existants (ACT-001, ACT-002) et
  chapitres/dossiers planifiés mais non créés (ACT-003 à ACT-010, PATTERNS, VERBS) ;
- ajout d'un avertissement sur le recouvrement potentiel entre un futur ACT-003 et
  le contenu déjà présent dans ACT-001-E et ACT-002-F à ACT-002-I ;
- correction du champ `Bibliothèque` de l'en-tête.

Corrige le constat ACT-C01.

## Version 1.0

- Création du document.
