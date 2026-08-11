# ACT — Catalogue

> Version : 1.13
> Statut : Foundation
> Bibliothèque : ACT
> Dépendances : MASTER, GDB
> Utilisée par : TECH, QA, UX

---

# Objectif

Ce catalogue référence l'ensemble des documents constituant la bibliothèque ACT.

ACT définit le langage universel des Actions de Chroniques.

---

# Structure générale

```text
ACT
├── ACT-001 Fondements
├── ACT-002 Modèle universel
├── ACT-003 retiré
├── ACT-004 à ACT-010 créés
├── PATTERNS
│   ├── PAT-001 Repos         M4
│   ├── PAT-002 Alimentation  M4
│   ├── PAT-003 Production    M4
│   └── PAT-004 Transfert     M2
└── VERBS
    ├── VERB-001 Se reposer           M4
    ├── VERB-002 Manger               M4
    ├── VERB-003 Produire une denrée  M4
    └── VERB-004 Donner une denrée    M2
```

ACT-003 reste retiré et son identifiant n'est pas réattribué.

---

# Couples Pattern / Verbe validés

## Entretien

```text
PAT-001 Repos
↓
VERB-001 Se reposer
Validation : 161 / 161
```

```text
PAT-002 Alimentation
↓
VERB-002 Manger
Validation : 178 / 178
```

## Transformation

```text
PAT-003 Production
↓
VERB-003 Produire une denrée
Validation : 201 / 201
```

---

# Couple en cours — Circulation économique

Autorités métier courantes :

```text
GDB-004A v1.2
GDB-005E v1.3
GDB-005F v1.2
```

Chaîne proposée :

```text
Échange
↓
PAT-004 Transfert v1.1 — Proposition / M2
↓
VERB-004 Donner une denrée v1.1 — Proposition / M2
```

Contrat :

```text
source P -= q
destination P += q
```

avec :

- `q > 0` ;
- donneur et destinataire distincts ;
- source et destination distinctes ;
- même identité de produit ;
- conservation de la quantité ;
- opportunité volontaire contextuelle ;
- aucun prix, monnaie ou paiement implicite.

Intent moteur :

```text
donner_denree
```

PAT-004 et VERB-004 ne passent pas M4 avant validation locale d'ENGINE-014.

---

# Règle d'évolution

Toute nouvelle mécanique doit :

- respecter ses autorités GDB ;
- passer les quatre tests d'ACT-008-A ;
- éviter la duplication d'un Pattern existant ;
- rattacher chaque Verbe à exactement un Pattern ;
- documenter ses impacts QA ;
- ne déclencher TECH/roadmap/README qu'à un point de consolidation significatif conformément à MASTER-006.

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

## Version 1.13

- PAT-004 / VERB-004 synchronisés avec GDB-005E v1.3 et GDB-005F v1.2 ;
- invariant `stock source ≠ stock destination` propagé jusqu'à ACT ;
- PAT-004 et VERB-004 restent Proposition / M2 ;
- aucune consolidation transverse déclenchée.

## Version 1.12

- création de PAT-004 — Transfert et VERB-004 — Donner une denrée.

## Version 1.11

- PAT-003 / VERB-003 validés à 201 / 201.

## Versions 1.0 à 1.10

- fondations ACT, retrait d'ACT-003, ouverture des sous-bibliothèques et validation progressive des premiers couples Pattern/Verbe.
