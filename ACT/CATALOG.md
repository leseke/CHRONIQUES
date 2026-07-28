# ACT — Catalogue

> Version : 1.2
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
├── Acteurs                   (planifié, non créé --- ACT-004)
├── Cibles                    (planifié, non créé --- ACT-005)
├── Conditions                (planifié, non créé --- ACT-006, périmètre restreint --- voir note)
├── Conséquences              (planifié, non créé --- ACT-007, périmètre restreint --- voir note)
├── Taxonomie                 (planifié, non créé --- ACT-008)
├── Composition                (planifié, non créé --- ACT-009)
├── Événements                (planifié, non créé --- ACT-010)
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
un identifiant retiré reste retiré, il n'est jamais réattribué (MASTER-004).

---

# Chapitres planifiés, non créés

Les chapitres suivants sont annoncés par l'architecture cible d'ACT (section 7
du README) mais **n'existent pas encore** dans le dépôt. Ils ne doivent pas être
comptés comme « non audités » : il n'y a aucun document à auditer tant qu'ils
n'ont pas été rédigés.

## ACT-004 --- Acteurs

Décrira les entités capables d'initier des actions.

Vérification de non-duplication (ACT-001-G, section 13, test 4) : ACT-001-B
section 2 (Principe de responsabilité) et ACT-001-H (entrée « Acteur » du
glossaire) posent l'axiome --- « toute action possède un acteur identifiable »
--- et une liste de catégories, mais aucun des deux ne définit les règles
d'éligibilité (quand un Acteur cesse-t-il d'être valide), la multiplicité
(une action à plusieurs Acteurs) ni le contrat vis-à-vis d'ACT-002-E
(Inputs) et ACT-002-F (échec de disparition). Ce contenu n'existe encore
nulle part : ACT-004 n'est pas redondant.

## ACT-005 --- Cibles

Décrira les entités pouvant recevoir une action.

Même constat que pour ACT-004 : ACT-001-B section 3 (Principe de ciblage)
et ACT-001-D (section « Cibles » du modèle canonique : type, rôle, état,
accessibilité) posent l'axiome et une liste de champs, sans définir les
règles de validité par type de cible, la frontière entre auto-ciblage et
ciblage d'autrui, ni la multiplicité des cibles. ACT-005 n'est pas
redondant.

## ACT-006 --- Conditions

Décrira les prérequis nécessaires à l'exécution.

**Périmètre restreint par rapport à la version 1.1 de ce catalogue.**
ACT-002-E (Action Contract, sections 5 et 6 --- Preconditions et
Constraints) et ACT-001-B section 5 (Principe de conditions) couvrent déjà
la place des conditions dans le contrat d'une action et leurs catégories
(matérielles, sociales, économiques, juridiques, environnementales,
temporelles, physiologiques, psychologiques). ACT-006 ne doit donc pas
redéfinir ce que sont les Preconditions/Constraints, mais peut légitimement
couvrir ce qui manque : une taxonomie stable des catégories de conditions
(au-delà de la simple liste), et les règles de composition de plusieurs
conditions entre elles (ET/OU, conditions mutuellement exclusives,
priorité en cas de conflit). À vérifier une nouvelle fois avant rédaction
que ce périmètre restreint reste suffisant pour justifier un document à
part entière plutôt qu'une extension d'ACT-002-E.

## ACT-007 --- Conséquences

Décrira les effets produits par une action.

**Périmètre restreint par rapport à la version 1.1 de ce catalogue**, pour
la même raison qu'ACT-006 : ACT-002-E (sections 10 et 11 --- Effects et
Events) et ACT-001-B section 6 (Principe de conséquence) couvrent déjà la
place des effets et événements dans le contrat d'une action. ACT-007 ne
doit pas redéfinir Effects/Events, mais peut couvrir une taxonomie des
catégories de conséquences (immédiate/différée, réversible/irréversible,
locale/globale) qui n'existe nulle part actuellement. Même vérification
requise avant rédaction qu'ACT-006.

## ACT-008 --- Taxonomie

Décrira les familles de verbes.

## ACT-009 --- Composition

Décrira la combinaison des actions simples en actions complexes.

## ACT-010 --- Événements

Décrira les événements générés par les actions.

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
