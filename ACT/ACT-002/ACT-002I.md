# ACT-002-I — Plan

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# 1. Objectif

Définir le Plan comme représentation structurée permettant de transformer une intention en une séquence cohérente d'actions.

---

# 2. Définition

Un Plan représente une stratégie d'exécution.

Il ne modifie jamais directement le monde.

Il décrit uniquement l'organisation des actions nécessaires pour satisfaire un Intent.

---

# 3. Position

Intent

↓

Planner

↓

Plan

↓

Action Definitions

↓

Action Instances

---

# 4. Composition

Un Plan est composé de :

- objectifs ;
- étapes ;
- dépendances ;
- contraintes ;
- critères de réussite.

---

# 5. Étapes

Chaque étape référence une ou plusieurs Action Definitions.

Une étape peut :

- être séquentielle ;
- être parallèle ;
- être optionnelle ;
- être conditionnelle.

---

# 6. Dépendances

Une étape peut dépendre :

- d'une autre étape ;
- d'un événement ;
- d'une condition ;
- d'une ressource.

Les dépendances circulaires sont interdites.

---

# 7. Réévaluation

Un Plan peut être :

- suspendu ;
- adapté ;
- abandonné ;
- reconstruit.

Cette décision appartient exclusivement au Planner.

---

# 8. Échec

L'échec d'une Action Instance n'implique pas nécessairement l'échec du Plan.

Le Planner peut :

- réessayer ;
- choisir une autre Action Definition ;
- modifier l'ordre des étapes ;
- abandonner le Plan.

---

# 9. Responsabilités

Le Plan :

- organise ;

- ne décide pas ;

- n'exécute pas.

---

# 10. Contrat

Le Plan ne connaît jamais les implémentations TECH.

Il manipule uniquement des concepts ACT.

---

# 11. Validation

Un Plan est valide si :

✓ chaque étape est cohérente ;

✓ les dépendances sont acycliques ;

✓ les critères de réussite sont définis.

---

# Historique

Version 1.0
