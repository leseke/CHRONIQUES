# GDB

> Les GDB constituent la bibliothèque officielle de conception de Chroniques.

---

# Présentation

La **Game Design Bible (GDB)** rassemble l'ensemble des connaissances décrivant Chroniques.

Chaque document répond à une question précise concernant le jeu.

Ensemble, les GDB décrivent l'intégralité de l'expérience joueur, du fonctionnement du monde et des systèmes qui composent Chroniques.

---

# Mission

Les GDB répondent à une seule question :

> **Qu'est-ce que Chroniques ?**

Elles définissent :

- les systèmes ;
- les mécaniques ;
- les règles ;
- les comportements ;
- les interactions ;
- les concepts ;
- les philosophies de conception.

Les GDB ne décrivent jamais leur implémentation technique.

---

# Responsabilité

Chaque GDB possède une responsabilité unique.

Un document ne traite qu'un seul concept.

Lorsqu'un sujet dépend d'un autre document, il y fait référence sans en recopier le contenu.

Chaque information officielle possède une seule source de vérité.

---

# Organisation

Les GDB sont regroupées par séries.

Chaque série traite un domaine particulier du jeu.

```
GDB
│
├── GDB-001
├── GDB-002
├── GDB-003
...
└── GDB-030
```

Chaque dossier possède son propre README décrivant son objectif.

---

# Structure d'une série

Une série contient plusieurs documents complémentaires.

Exemple :

```
GDB-006

README

GDB-006A
GDB-006B
GDB-006C
...
GDB-006J
```

Les documents d'une même série abordent différents aspects d'un même thème.

---

# Cycle documentaire

Une idée suit toujours le même cycle.

```
MASTER
      ↓
GDB
      ↓
TECH
      ↓
Code
```

Les GDB définissent le comportement attendu.

Les documents TECH expliquent ensuite comment ce comportement est implémenté.

---

# Convention de nommage

Toutes les GDB respectent la convention suivante.

```
GDB-XXX
```

ou

```
GDB-XXXA
```

où :

- XXX représente la série.
- A à J représentent les sous-parties de la série.

Cette convention garantit une organisation cohérente et évolutive.

---

# Création d'une nouvelle GDB

Avant de créer un document, vérifier :

- Le sujet existe-t-il déjà ?
- Une GDB répond-elle déjà à cette question ?
- Le document apporte-t-il une nouvelle connaissance ?
- Le concept mérite-t-il un document dédié ?

Si la réponse est non, il est préférable d'enrichir un document existant.

---

# Modification d'une GDB

Une GDB peut évoluer.

Toute modification doit :

- préserver la cohérence du projet ;
- respecter les MASTER ;
- éviter les duplications ;
- conserver une responsabilité unique.

---

# Relations entre les séries

Les séries sont indépendantes mais liées.

Une GDB peut référencer une autre série lorsqu'un concept est partagé.

Elle ne doit jamais recopier son contenu.

---

# Bibliothèque actuelle

| Série | Domaine |
|--------|----------|
| GDB-001 | Fondations |
| GDB-002 | ... |
| GDB-003 | ... |
| GDB-004 | ... |
| GDB-005 | ... |
| GDB-006 | ... |
| GDB-007 | ... |
| GDB-008 | ... |
| GDB-009 | ... |
| GDB-010 | ... |
| GDB-011 | ... |
| GDB-012 | ... |
| ... | ... |
| GDB-030 | ... |

(Cet index est maintenu à jour au fur et à mesure de l'évolution du projet.)

---

# Philosophie

Les GDB privilégient :

- la clarté ;
- la précision ;
- la modularité ;
- la cohérence ;
- la non-redondance ;
- la pérennité.

Chaque document doit pouvoir être lu indépendamment tout en s'intégrant naturellement à l'ensemble de la bibliothèque.

---

# Objectif

Construire une base documentaire capable de décrire intégralement Chroniques tout en restant lisible, cohérente et évolutive sur plusieurs années de développement.

---

Version : 1.0

Statut : Officiel
