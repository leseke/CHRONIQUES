# ACT — Catalogue

> Version : 1.12
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
├── Patterns                  (PAT-001 M4 ; PAT-002 M4 ; PAT-003 M4 ; PAT-004 M2)
└── Verbes                    (VERB-001 M4 ; VERB-002 M4 ; VERB-003 M4 ; VERB-004 M2)

---

# Bibliothèque PATTERNS

Statut : créée et ouverte.

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
Officiel / Maturité 4
Validation : 201 / 201
Principe : Transformation
Verbe : VERB-003 Produire une denrée
```

## PAT-004 — Transfert

```text
Proposition / Maturité 2
Principe : Échange
Verbe proposé : VERB-004 Donner une denrée
```

Origine : GDB-005E v1.2 + GDB-005F v1.1.

Structure proposée :

```text
source P -= q
destination P += q
```

La quantité totale est conservée. Aucun prix, paiement ou marché n'est inclus.

PATTERNS reste ouverte.

---

# Bibliothèque VERBS

Statut : créée et ouverte.

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
Officiel / Maturité 4
Validation : 201 / 201
Intent : produire_denree
Pattern : PAT-003 Production
```

## VERB-004 — Donner une denrée

```text
Proposition / Maturité 2
Intent : donner_denree
Pattern : PAT-004 Transfert
```

Le premier contrat resserré transfère une denrée existante d'un habitant à un autre entre deux stocks alimentaires distincts et compatibles.

VERB-004 ne constitue ni une vente, ni un troc réciproque, ni un système de prix.

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

## Version 1.12

- création de `PAT-004 — Transfert` en Proposition / Maturité 2 ;
- création de `VERB-004 — Donner une denrée` en Proposition / Maturité 2 ;
- rattachement `Échange → PAT-004 → VERB-004` ;
- transfert conservatif de denrée entre habitants ;
- prix, monnaie, vente et troc réciproque maintenus hors périmètre ;
- aucune validation M4 anticipée ;
- aucune consolidation TECH/roadmap/README déclenchée.

## Version 1.11

- PAT-003 et VERB-003 validés / Maturité 4 ;
- validation portée à 201 / 201.

## Versions 1.0 à 1.10

- création et consolidation des fondations ACT et des trois premiers couples Pattern/Verbe.
