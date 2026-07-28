# ACT-001-I — Références et dépendances

> Version : 1.1
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Maturité : 1
>
> Bibliothèque : ACT
>
> Dépendances :
> - MASTER
> - GDB
>
> Utilisé par :
> - TECH
> - QA
> - UX
> - IA
> - Documentation

---

# 1. Objectif

Définir les relations officielles entre la bibliothèque ACT et les autres bibliothèques du projet Chroniques.

Ce document garantit la cohérence globale de l'architecture documentaire.

---

# 2. Principe

Aucune bibliothèque n'est isolée.

Chaque document appartient à une chaîne documentaire clairement définie.

Les dépendances sont toujours orientées dans le même sens.

---

# 3. Architecture documentaire

MASTER

↓

CORE

↓

GDB

↓

ACT

↓

TECH

↓

QA

↓

CODE

Cette hiérarchie constitue l'architecture officielle du projet [réf: MASTER-003].

Une version antérieure de ce document plaçait STANDARDS entre MASTER et GDB.
STANDARDS a depuis été absorbé par MASTER (MASTER-004, MASTER-006, MASTER-007) ;
CORE a été créé comme bibliothèque de primitives fondamentales, positionnée entre
MASTER et GDB [réf: ADR-001, ADR-003].

---

# 4. Dépendances entrantes

ACT dépend uniquement des bibliothèques suivantes :

## MASTER

Définit :

- la vision ;
- les objectifs ;
- les principes directeurs ;
- les conventions documentaires (absorbant l'ancien rôle de STANDARDS).

---

## CORE

Définit les primitives fondamentales du moteur --- Entity, Component, Value,
State, Relation, Event, Time, Space, Lifecycle [réf: CORE-000C].

Toute action manipule ces primitives sans les redéfinir : un Acteur est une
Entity, un Effet modifie un State, un Événement publié par ACT est un Event au
sens de CORE. ACT ne redéfinit jamais ces concepts, il les emploie.

---

## GDB

Décrit :

- les entités ;
- les ressources ;
- les organisations ;
- les métiers ;
- les lois du monde.

ACT utilise ces concepts sans les modifier.

---

# 5. Dépendances sortantes

ACT est utilisé par :

## TECH

Implémente les mécaniques.

---

## QA

Valide les mécaniques.

---

## UX

Présente les mécaniques.

---

## IA

Planifie les actions.

---

## LORE

Peut utiliser les actions comme base narrative.

---

# 6. Traçabilité

Toute mécanique doit pouvoir être suivie :

Vision

↓

Concept

↓

Action

↓

Implémentation

↓

Test

↓

Historique

---

# 7. Références croisées

Chaque document ACT doit référencer :

- les documents MASTER concernés ;
- les documents GDB utilisés ;
- les modules TECH impactés ;
- les scénarios QA associés.

---

# 8. Dépendances interdites

ACT ne peut jamais dépendre :

- du code ;
- d'une implémentation TECH ;
- d'un scénario QA ;
- d'une interface UX.

Ces dépendances inverseraient l'architecture.

---

# 9. Cohérence

Toute modification :

MASTER

↓

peut impacter

↓

GDB

↓

ACT

↓

TECH

↓

QA

La propagation des changements doit toujours respecter cet ordre.

---

# 10. Contrat

Aucun document ACT ne peut être validé s'il :

- référence une couche inférieure ;
- duplique une information de GDB ;
- décrit une implémentation TECH.

---

# 11. Critères de validation

Le document est conforme si :

✓ les dépendances sont acycliques ;

✓ les responsabilités restent séparées ;

✓ chaque référence possède une justification.

---

# 12. Historique

Version 1.1

Correction de la hiérarchie documentaire : STANDARDS (absorbé par MASTER) retiré,
CORE ajouté comme dépendance explicite. Corrige ACT-001-C01. En-tête mis en
conformité avec MASTER-004.

Version 1.0

Création du modèle officiel de dépendances documentaires.
