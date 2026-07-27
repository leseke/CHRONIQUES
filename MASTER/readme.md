# MASTER

> Version : 1.1
> Statut : Officiel
> Type : Bibliothèque
> Maturité : 1
> Bibliothèque : MASTER

---

# Présentation

Le dossier **MASTER** rassemble les documents qui définissent les fondations du projet.

Contrairement aux GDB, ils ne décrivent pas le jeu.

Ils définissent la manière dont le projet est conçu, organisé, documenté et développé.

Ils servent de référence à l'ensemble des autres bibliothèques.

---

# Objectif

Les MASTER garantissent :

- une vision commune ;
- une architecture documentaire cohérente ;
- des standards partagés ;
- des conventions de travail ;
- une gouvernance stable.

Ils permettent à tous les contributeurs --- humains comme IA --- de travailler selon les mêmes règles.

---

# Responsabilités

Les MASTER définissent notamment :

- les principes du projet ;
- l'organisation documentaire ;
- les standards d'écriture ;
- les méthodes de développement ;
- les conventions ;
- la gouvernance.

Ils ne décrivent jamais le fonctionnement du jeu.

---

# Ce qu'un MASTER ne doit jamais contenir

Les documents MASTER ne doivent pas contenir :

- des mécaniques de gameplay ;
- des systèmes du jeu ;
- des règles économiques ;
- des caractéristiques de personnages ;
- des spécifications techniques.

Ces informations appartiennent aux autres bibliothèques.

---

# Quand créer un MASTER ?

Un nouveau MASTER ne doit être créé que lorsqu'une règle de gouvernance manque réellement.

Avant toute création, il convient de vérifier que le sujet n'est pas déjà couvert par un document existant.

Les MASTER doivent rester peu nombreux afin de conserver une gouvernance claire.

---

# Quand modifier un MASTER ?

Un MASTER est modifié uniquement lorsque :

- une règle évolue ;
- une convention change ;
- une amélioration de gouvernance est validée.

Les modifications doivent rester exceptionnelles.

---

# Hiérarchie documentaire

Les MASTER constituent le niveau le plus élevé de la documentation.

Ils servent de référence aux autres bibliothèques.

```
MASTER
    ↓
GDB
    ↓
TECH
    ↓
Code
```

Aucun niveau inférieur ne peut contredire un MASTER.

---

# Documents

| Document | Objet |
|----------|-------|
| MASTER-001 | Vision du projet |
| MASTER-002 | Principes fondamentaux |
| MASTER-003 | Architecture officielle |
| MASTER-004 | Conventions de documentation |
| MASTER-005 | Roadmap |
| MASTER-006 | Gouvernance des décisions |
| MASTER-007 | Standards de qualité |
| MASTER-008 | Méthodologie d'audit et de correction documentaire |

Ce tableau est maintenu à la main, contrairement à GDB/CATALOG.md. Toute création ou suppression d'un document MASTER doit mettre à jour cette table dans le même lot de correction, jamais après coup.

---

# Principes

Les documents MASTER respectent les principes suivants :

- simplicité ;
- cohérence ;
- stabilité ;
- modularité ;
- non-redondance ;
- évolutivité.

Chaque information officielle ne possède qu'une seule source de vérité.

---

# Historique

## Version 1.1

- en-tête mis en conformité avec MASTER-004 (Version, Statut, Type, Maturité, Bibliothèque) ;
- correction de la description de MASTER-007 (indiquée à tort comme « Gestion des dépendances documentaires », alors qu'il s'agit de « Standards de qualité ») ;
- ajout de MASTER-008, absent du tableau.

Constat découvert lors de l'analyse d'impact de la création de MASTER-008 (ADR-004) ; corrige MASTER-C03.

## Version 1.0

- Création du document.
