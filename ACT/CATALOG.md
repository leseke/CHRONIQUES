# ACT — Catalogue

> Version : 1.10
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

---

# Structure générale

ACT

├── Fondements                (ACT-001)
├── Modèle universel          (ACT-002)
├── Cycle de vie              (ACT-003 retiré)
├── Acteurs                   (ACT-004, Proposition)
├── Cibles                    (ACT-005, Proposition)
├── Conditions                (ACT-006-A, audité)
├── Conséquences              (ACT-007-A, audité)
├── Taxonomie                 (ACT-008-A, audité)
├── Composition               (ACT-009-A, audité)
├── Événements                (ACT-010-A, audité)
├── Patterns                  (PAT-001 M4 ; PAT-002 M4 ; PAT-003 M2)
└── Verbes                    (VERB-001 M4 ; VERB-002 M4 ; VERB-003 M2)

---

# Documents existants

## ACT-001 — Fondements de l'action

Créé et audité.

## ACT-002 — Modèle universel de l'action

Créé et audité.

## ACT-003 — Retiré

ACT-003 reste retiré car son contenu serait redondant avec ACT-001-E et ACT-002-F à I. Son identifiant ne sera pas réattribué.

## ACT-004 à ACT-010

Créés. Leur statut documentaire détaillé reste porté par leurs documents propres et les audits applicables.

---

# Bibliothèque PATTERNS

Statut : créée et ouverte.

Catalogue : `ACT/PATTERNS/readme.md`.

## PAT-001 — Repos

```text
Officiel / Maturité 4
Validation : 161 / 161
Principe : Entretien
Verbe : VERB-001 Se reposer
```

## PAT-002 — Alimentation

```text
Officiel / Maturité 4
Validation : 178 / 178
Principe : Entretien
Verbe : VERB-002 Manger
```

## PAT-003 — Production

```text
Proposition / Maturité 2
Principe : Transformation
Verbe proposé : VERB-003 Produire une denrée
```

Origine : GDB-004A v1.1, GDB-005C v1.2, GDB-012B v1.1 et GDB-012E v1.1.

Structure proposée :

```text
entrées accessibles consommées
↓
sortie produite
+
provenance persistante
```

PAT-003 est distinct de Repos et Alimentation par sa structure de contrat entrée → sortie.

PATTERNS reste ouverte.

---

# Bibliothèque VERBS

Statut : créée et ouverte.

Catalogue : `ACT/VERBS/readme.md`.

## VERB-001 — Se reposer

```text
Officiel / Maturité 4
Validation : 161 / 161
Intent : se_reposer
```

## VERB-002 — Manger

```text
Officiel / Maturité 4
Validation : 178 / 178
Intent : manger
```

## VERB-003 — Produire une denrée

```text
Proposition / Maturité 2
Intent : produire_denree
Pattern : PAT-003 Production
```

Le premier contrat resserré transforme une entrée matérielle en sortie alimentaire selon une opération explicite, sans métier, salaire, prix ni marché implicites.

VERBS reste ouverte.

---

# Règle d'évolution

Toute nouvelle mécanique doit :

- éviter la duplication d'un Pattern existant ;
- passer les quatre tests d'ACT-008-A ;
- rattacher tout Verbe à exactement un Pattern ;
- documenter ses impacts QA ;
- ne consolider TECH/roadmap/README qu'à un point de clôture significatif conformément à MASTER-006.

---

# Dépendances

```text
MASTER
↓
GDB
↓
ACT
↓
ENGINE
↓
CODE
```

---

# Historique

## Version 1.10

- création de `PAT-003 — Production` en Proposition / Maturité 2 ;
- création de `VERB-003 — Produire une denrée` en Proposition / Maturité 2 ;
- rattachement `Transformation → PAT-003 → VERB-003` ;
- origine métier fixée par GDB-004A v1.1, GDB-005C v1.2, GDB-012B v1.1 et GDB-012E v1.1 ;
- aucune validation M4 anticipée ;
- aucune consolidation TECH/roadmap/README déclenchée.

## Version 1.9

- PAT-002 et VERB-002 validés / Maturité 4 ;
- validation portée à 178 / 178.

## Version 1.8

- création de PAT-002 et VERB-002.

## Version 1.7

- PAT-001 et VERB-001 validés / Maturité 4 ;
- validation portée à 161 / 161.

## Version 1.6

- création effective des sous-bibliothèques PATTERNS/ et VERBS/.

## Versions 1.0 à 1.5

- création et consolidation initiales d'ACT-001 à ACT-010, avec retrait d'ACT-003 et ouverture de la taxonomie/composition/événements.
