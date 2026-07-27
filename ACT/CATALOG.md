# ACT — Catalogue

> Version : 1.1
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
├── Cycle de vie              (planifié, non créé --- ACT-003)
├── Acteurs                   (planifié, non créé --- ACT-004)
├── Cibles                    (planifié, non créé --- ACT-005)
├── Conditions                (planifié, non créé --- ACT-006)
├── Conséquences              (planifié, non créé --- ACT-007)
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

# Chapitres planifiés, non créés

Les chapitres suivants sont annoncés par l'architecture cible d'ACT (section 7
du README) mais **n'existent pas encore** dans le dépôt. Ils ne doivent pas être
comptés comme « non audités » : il n'y a aucun document à auditer tant qu'ils
n'ont pas été rédigés.

## ACT-003 --- Cycle de vie

Décrira toutes les étapes d'une action. Une partie de ce sujet est déjà
esquissée par ACT-001-E (Cycle de vie d'une action) et par ACT-002-F à
ACT-002-I (modèle d'exécution, Outcome, Intent, Plan) : avant de créer ACT-003,
vérifier qu'il n'en résultera pas une redondance avec ces sections existantes,
conformément au principe de responsabilité unique (MASTER-003).

## ACT-004 --- Acteurs

Décrira les entités capables d'initier des actions.

## ACT-005 --- Cibles

Décrira les entités pouvant recevoir une action.

## ACT-006 --- Conditions

Décrira les prérequis nécessaires à l'exécution.

## ACT-007 --- Conséquences

Décrira les effets produits par une action.

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

## Version 1.1

- distinction explicite entre chapitres/dossiers existants (ACT-001, ACT-002) et
  chapitres/dossiers planifiés mais non créés (ACT-003 à ACT-010, PATTERNS, VERBS) ;
- ajout d'un avertissement sur le recouvrement potentiel entre un futur ACT-003 et
  le contenu déjà présent dans ACT-001-E et ACT-002-F à ACT-002-I ;
- correction du champ `Bibliothèque` de l'en-tête.

Corrige le constat ACT-C01.

## Version 1.0

- Création du document.
