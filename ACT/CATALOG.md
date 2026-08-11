# ACT — Catalogue

> Version : 1.8
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
├── Composition               (créé --- ACT-009-A, v1.1 audité --- voir note sur la frontière avec le Plan)
├── Événements                (créé --- ACT-010-A, v1.0 audité --- voir note sur le périmètre restreint)
├── Patterns                  (PAT-001 Officiel/M4 ; PAT-002 Proposition/M2)
└── Verbes                    (VERB-001 Officiel/M4 ; VERB-002 Proposition/M2)

---

# Documents existants

## ACT-001 --- Fondements de l'action

Statut : Créé et audité.

Sections A à I. Définit la philosophie générale, les principes fondamentaux, la définition universelle et le modèle canonique de l'action, son cycle de vie et ses états, le périmètre de la bibliothèque, sa terminologie et ses références.

## ACT-002 --- Modèle universel de l'action

Statut : Créé et audité.

Sections A à J. Décrit la structure commune à toutes les actions : niveaux d'abstraction, relations entre niveaux, définition et instanciation, Action Contract, modèle d'exécution, Outcome, Intent, Plan, et gouvernance du modèle.

---

# Chapitre retiré

## ACT-003 --- Cycle de vie (retiré de la structure cible)

La version 1.1 de ce catalogue avertissait : *« avant de créer ACT-003, vérifier qu'il n'en résultera pas une redondance avec [ACT-001-E et ACT-002-F à ACT-002-I]. »* Cette vérification a été faite.

- `ACT-001-E` définit déjà la machine à états complète d'une action, avec les contrats TECH/IA/QA associés et les règles d'interruption, de suspension et d'annulation.
- `ACT-002-F`, section 3bis, relie explicitement ce cycle à Intent → Plan → Action Instance → Execution Engine → Effects → Events → World Update → Outcome.
- `ACT-002-I` autorise déjà des étapes de Plan séquentielles, parallèles, optionnelles ou conditionnelles.

Conclusion du test de non-duplication : aucun contenu réel ne resterait à écrire dans un ACT-003 « Cycle de vie » sans reformuler ACT-001-E et ACT-002-F à l'identique. ACT-003 reste donc retiré de la structure cible.

Les identifiants ACT-004 à ACT-010 ne sont pas renumérotés : un identifiant retiré reste retiré, il n'est jamais réattribué.

---

# Chapitres créés, non encore tous validés

## ACT-004 --- Acteurs

Décrit les entités capables d'initier des actions et leurs règles d'éligibilité.

## ACT-005 --- Cibles

Décrit multiplicité, rôle, éligibilité et accessibilité des Cibles.

## ACT-006 --- Conditions

Décrit la taxonomie et la composition des conditions sans redéfinir Preconditions et Constraints déjà définies par ACT-002-E.

## ACT-007 --- Conséquences

Décrit la taxonomie et la composition des conséquences sans redéfinir Effects et Events déjà présents dans ACT-002-E.

## ACT-008 --- Taxonomie des verbes

Décrit notamment :

- la multiplicité Pattern / Verbe ;
- le critère de création d'un nouveau Verbe en quatre tests ;
- la non-polysémie ;
- la responsabilité de VERBS pour l'énumération concrète.

## ACT-009 --- Composition d'Actions

Décrit la combinaison d'Actions simples en Actions complexes et tranche la frontière avec le Plan.

## ACT-010 --- Taxonomie des événements

Décrit les catégories conceptuelles d'événements sans redéfinir le mécanisme technique de publication.

---

# Bibliothèque PATTERNS

Statut : créée et ouverte.

Catalogue :

```text
ACT/PATTERNS/readme.md
```

## PAT-001 — Repos

```text
Officiel / Maturité 4
Validation : 161 / 161
```

Chaîne validée :

```text
Principe Entretien
↓
PAT-001 Repos
↓
VERB-001 Se reposer
```

## PAT-002 — Alimentation

```text
Proposition / Maturité 2
```

Origine : GDB-004B v1.2 + GDB-005E v1.1.

Chaîne proposée :

```text
Principe Entretien
↓
PAT-002 Alimentation
↓
VERB-002 Manger
```

PAT-002 est distinct de PAT-001 car il exige une Cible-produit alimentaire accessible, une consommation réelle et un effet sur le besoin de nourriture.

PATTERNS reste ouverte.

---

# Bibliothèque VERBS

Statut : créée et ouverte.

Catalogue :

```text
ACT/VERBS/readme.md
```

## VERB-001 — Se reposer

```text
Officiel / Maturité 4
Validation : 161 / 161
Intent : se_reposer
```

## VERB-002 — Manger

```text
Proposition / Maturité 2
Intent : manger
```

VERB-002 spécialise exactement PAT-002.

Son contrat exige :

```text
Acteur
+
produit alimentaire accessible
↓
Action Manger réussie
↓
disponibilité du produit ↓
+
Faim ↑
```

La Cible alimentaire appartient au Plan/Action, jamais à l'Intent.

VERBS reste ouverte.

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

- ne pas dupliquer un Pattern existant ;
- ne pas créer un Verbe si un paramétrage d'un Verbe existant couvre déjà le besoin ;
- ne pas créer un Verbe si une composition de Verbes existants couvre déjà le besoin ;
- rattacher tout Verbe à exactement un Pattern ;
- documenter les impacts QA ;
- ne consolider TECH/roadmap/README qu'aux points de clôture significatifs retenus par le projet.

---

# Références

MASTER

GDB

TECH

QA

UX

---

# Historique

## Version 1.8

- création de `PAT-002 — Alimentation` en Proposition / Maturité 2 ;
- création de `VERB-002 — Manger` en Proposition / Maturité 2 ;
- origine métier fixée par GDB-004B v1.2 et GDB-005E v1.1 ;
- distinction contractuelle avec PAT-001 / VERB-001 confirmée par les quatre tests d'ACT-008-A ;
- PATTERNS et VERBS restent ouvertes ;
- aucune consolidation TECH/roadmap/README déclenchée.

## Version 1.7

- `PAT-001 — Repos` passe à Officiel / Maturité 4 ;
- `VERB-001 — Se reposer` passe à Officiel / Maturité 4 ;
- validation locale portée à 161 / 161 tests réussis ;
- chaîne canonique `Entretien → PAT-001 → VERB-001 → Action` confirmée.

## Version 1.6

- création effective des sous-bibliothèques PATTERNS/ et VERBS/ ;
- attribution du premier Pattern réel PAT-001 ;
- attribution du premier Verbe réel VERB-001.

## Version 1.5

- ACT-008-A créé ;
- ACT-009-A créé ;
- ACT-010-A créé.

## Version 1.4

- ACT-007-A créé ;
- correction du statut d'ACT-006 dans le catalogue.

## Version 1.3

- correction d'une citation erronée sur la non-réattribution d'identifiants ;
- ACT-004 marqué comme créé ;
- ACT-005 créé.

## Version 1.2

- retrait d'ACT-003 après vérification de redondance ;
- restriction du périmètre annoncé d'ACT-006 et ACT-007.

## Version 1.1

- distinction explicite entre chapitres existants et planifiés ;
- correction du champ Bibliothèque.

## Version 1.0

- création du document.
