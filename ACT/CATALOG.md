# ACT — Catalogue

> Version : 1.7
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
├── Patterns                  (créé --- PATTERNS/, PAT-001 Officiel / M4)
└── Verbes                    (créé --- VERBS/, VERB-001 Officiel / M4)

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

# Chapitres créés, non encore audités

Les chapitres suivants existent dans le dépôt (Statut : Proposition) mais n'ont pas encore tous traversé les étapes Validée/Spécifiée du cycle de vie documentaire d'une mécanique.

## ACT-004 --- Acteurs

Décrit les entités capables d'initier des actions.

ACT-004 complète les axiomes déjà présents dans ACT-001 en précisant les règles d'éligibilité, de multiplicité et les liens avec l'Action Contract.

## ACT-005 --- Cibles

Décrit les entités pouvant recevoir une action.

ACT-005 précise multiplicité, rôle, éligibilité et perte d'éligibilité d'une Cible, sans redéfinir les axiomes de ciblage déjà présents dans ACT-001.

## ACT-006 --- Conditions

Décrit la taxonomie et la composition des conditions sans redéfinir Preconditions et Constraints déjà définies par ACT-002-E.

## ACT-007 --- Conséquences

Décrit la taxonomie et la composition des conséquences sans redéfinir Effects et Events déjà présents dans ACT-002-E.

## ACT-008 --- Taxonomie des verbes

Décrit les règles d'organisation des Verbes en familles partageant un même Pattern.

ACT-008 définit notamment :

- la multiplicité Pattern / Verbe ;
- le critère de création d'un nouveau Verbe en quatre tests ;
- la non-polysémie ;
- la responsabilité de la sous-bibliothèque VERBS pour l'énumération concrète.

## ACT-009 --- Composition d'Actions

Décrit la combinaison d'Actions simples en Actions complexes et tranche la frontière avec le Plan.

## ACT-010 --- Taxonomie des événements

Décrit les catégories conceptuelles d'événements sans redéfinir le mécanisme technique de publication.

---

# Chapitres planifiés, non créés

Aucun chapitre numéroté d'ACT ne reste planifié à ce stade : ACT-001 à ACT-010 sont créés, ACT-003 restant explicitement retiré.

Les deux sous-bibliothèques anciennement planifiées sont désormais créées :

```text
PATTERNS/
VERBS/
```

Leur contenu reste volontairement minimal et piloté par des besoins réels.

---

# Bibliothèque PATTERNS

Statut : créée et ouverte.

Catalogue :

```text
ACT/PATTERNS/readme.md
```

Premier Pattern réellement attribué et validé :

```text
PAT-001 — Repos
Officiel / Maturité 4
```

Chaîne validée :

```text
Principe Entretien
↓
PAT-001 Repos
↓
VERB-001 Se reposer
```

Validation technique de référence :

```text
dotnet build
→ succès

dotnet test
→ 161 / 161 tests réussis
→ 0 échec
```

Les exemples historiques `PAT-001 Influence`, `PAT-002 Transformation`, etc. présents avant la création effective de PATTERNS étaient explicitement « envisagés, à confirmer » et ne constituaient aucune réservation d'identifiant.

L'attribution réelle commence donc par le premier besoin effectivement requis par la simulation validée.

La validation de PAT-001 ne signifie pas que la sous-bibliothèque PATTERNS est clôturée.

---

# Bibliothèque VERBS

Statut : créée et ouverte.

Catalogue :

```text
ACT/VERBS/readme.md
```

Premier Verbe concret validé :

```text
VERB-001 — Se reposer
Officiel / Maturité 4
```

Il spécialise exactement :

```text
PAT-001 — Repos
```

et répond au besoin GDB réel défini par GDB-004B.

Objectif d'Intent associé dans l'implémentation actuelle :

```text
se_reposer
```

La suite globale de **161 / 161 tests réussis** confirme la chaîne canonique, la structure contractuelle, la planification vers `SeReposerDefinition` et l'exécution déjà couverte par les lots ENGINE précédents.

Aucun second Verbe ne doit être créé tant qu'il n'a pas passé, dans l'ordre, les quatre tests d'ACT-008-A : paramétrage, composition, Pattern existant, nouveau Pattern.

La validation de VERB-001 ne signifie pas que la sous-bibliothèque VERBS est clôturée.

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

## Version 1.7

- `PAT-001 — Repos` passe à **Officiel / Maturité 4** ;
- `VERB-001 — Se reposer` passe à **Officiel / Maturité 4** ;
- validation locale portée à **161 / 161 tests réussis** ;
- chaîne canonique `Entretien → PAT-001 → VERB-001 → Action` confirmée ;
- PATTERNS et VERBS restent ouvertes : aucune clôture de bibliothèque ni consolidation transverse n'est déclenchée.

## Version 1.6

- création effective des sous-bibliothèques `PATTERNS/` et `VERBS/` ;
- création de leurs catalogues respectifs ;
- attribution du premier Pattern réel `PAT-001 — Repos` ;
- attribution du premier Verbe réel `VERB-001 — Se reposer` ;
- rattachement `Entretien → PAT-001 → VERB-001` ;
- suppression du statut « planifié, non créé » pour PATTERNS et VERBS ;
- clarification que les anciennes listes PAT-xxx / VERB-xxx n'étaient que des exemples non réservés.

## Version 1.5

- `ACT-008-A` créé : règles de multiplicité Pattern/Verbe, critère de nouveau Verbe en quatre tests et non-polysémie ;
- `ACT-009-A` créé : composition d'Actions et frontière avec le Plan ;
- `ACT-010-A` créé : taxonomie conceptuelle des événements ;
- ACT-001 à ACT-010 désormais créés, ACT-003 excepté car retiré ;
- PATTERNS et VERBS restaient alors à créer.

## Version 1.4

- `ACT-007-A` créé ;
- correction du statut d'ACT-006 dans le catalogue.

## Version 1.3

- correction d'une citation erronée sur la non-réattribution d'identifiants ;
- `ACT-004` marqué comme créé ;
- `ACT-005` créé.

## Version 1.2

- retrait d'ACT-003 après vérification de redondance ;
- confirmation de la non-duplication d'ACT-004 et ACT-005 ;
- restriction du périmètre annoncé d'ACT-006 et ACT-007.

## Version 1.1

- distinction explicite entre chapitres existants et planifiés ;
- avertissement sur le recouvrement potentiel d'ACT-003 ;
- correction du champ `Bibliothèque`.

Corrige le constat ACT-C01.

## Version 1.0

- création du document.
