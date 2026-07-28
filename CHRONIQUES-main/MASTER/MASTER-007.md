# MASTER-007 --- Standards de Qualité

> Version : 1.0
> Statut : Officiel
> Type : Qualité
> Maturité : 1
> Bibliothèque : MASTER

---

# Objectif

Définir à quelles conditions un document est considéré comme terminé.

Sans définition du terminé, un document reste indéfiniment ouvert, ou est déclaré fini sans l'être.

---

# Ce que qualité ne signifie pas

La qualité d'un document ne se mesure ni à sa longueur, ni à son exhaustivité.

Un document court qui tranche vaut mieux qu'un document long qui décrit.

Un document qui énumère des possibilités sans en retenir aucune n'est pas terminé : il est en attente de décision.

---

# Critères d'un document terminé

Un document est terminé lorsqu'il satisfait les huit critères suivants.

## 1. Identifiant

Le document porte un identifiant unique, conforme aux conventions.

## 2. En-tête

Titre, version, statut, type, maturité et bibliothèque sont renseignés, conformément à MASTER-004.

## 3. Objectif

Le document énonce ce qu'il définit et, lorsque la confusion est possible, ce qu'il ne définit pas.

## 4. Décisions tranchées

Aucune question ouverte ne subsiste dans le corps du document.

Une question qui ne peut pas être tranchée est explicitement ajournée et rattachée à une phase.

## 5. Absence de contradiction

Le document ne contredit aucun document de rang supérieur.

## 6. Absence de redondance

Le document ne réécrit pas un sujet traité ailleurs. Il s'y réfère.

## 7. Références déclarées

Toute dépendance à un autre document est déclarée par un marqueur de référence.

## 8. Critère de validation

Le document se termine par une question opposable permettant de juger toute évolution future.

---

# Exigences par niveau de maturité

Les huit critères s'appliquent à tous les niveaux. S'y ajoutent des exigences propres.

| Niveau | Exigence supplémentaire |
|--------|-------------------------|
| 1 --- Fondations | Le document énonce des principes, non des solutions. |
| 2 --- Spécification | Le comportement décrit est suffisamment précis pour être implémenté sans interprétation. |
| 3 --- Implémentation | Le document correspond au code existant, identifiant pour identifiant. |
| 4 --- Validation | Le comportement décrit a été observé lors d'un test. |

---

# Revue

Un document est relu avant d'être déclaré terminé.

La revue porte sur les huit critères, dans l'ordre. Elle ne porte pas sur le style.

Un document qui échoue à un critère n'est pas corrigé par son relecteur : il est retourné avec le critère manquant.

---

# Dette documentaire

Un document déclaré terminé puis invalidé par un enseignement devient une dette.

Une dette est visible : son statut passe à *À réviser*, et le motif est inscrit dans le document.

Une dette non visible est le seul défaut réellement dangereux, car elle se propage aux documents qui s'y réfèrent.

Un document officiel qui ne respecte pas le critère 2 (en-tête complet, conforme à MASTER-004) est une dette non visible par nature : rien dans sa lecture ne signale le manque tant que personne ne le compare à la convention.

---

# Critère de validation

Avant de déclarer un document terminé :

Ce document permettrait-il à quelqu'un qui découvre le projet de savoir quoi faire, sans poser de question ?

Si la réponse est non, il n'est pas terminé.

---

Fin du document

Statut : Validé --- Référence officielle.
