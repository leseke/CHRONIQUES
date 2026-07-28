# ACT-002-D — Définition et instanciation des actions

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# 1. Objectif

Séparer la définition d'une action de son exécution afin de garantir la stabilité, la réutilisabilité et la traçabilité du modèle d'action.

---

# 2. Principe

Une action est composée de deux niveaux distincts :

- une définition ;
- une ou plusieurs instances.

La définition est immuable.

Les instances sont éphémères.

---

# 3. Action Definition

Une Action Definition décrit ce qui peut être exécuté.

Elle contient notamment :

- le Verbe associé ;
- les paramètres requis ;
- les acteurs autorisés ;
- les cibles compatibles ;
- les préconditions ;
- les postconditions ;
- les effets potentiels ;
- les événements produits.

Elle ne représente jamais une exécution.

---

# 4. Action Instance

Une Action Instance représente une exécution réelle.

Elle possède :

- un identifiant ;
- un instant de création ;
- un état ;
- un contexte ;
- des acteurs réels ;
- des cibles réelles ;
- des valeurs de paramètres ;
- un historique.

Chaque instance est indépendante.

---

# 5. Relation

Une Action Definition peut produire un nombre illimité d'instances.

Une instance provient toujours d'une seule définition.

---

# 6. Cycle de vie

Action Definition

↓

Création d'une instance

↓

Validation

↓

Planification

↓

Préparation

↓

Exécution

↓

Résolution

↓

Archivage

---

# 7. Immutabilité

Une Action Definition validée ne peut être modifiée pendant l'exécution d'une instance.

Toute évolution crée une nouvelle version de la définition.

---

# 8. Traçabilité

Chaque instance conserve une référence vers :

- sa définition ;
- son Verbe ;
- son Pattern ;
- son Principe.

La chaîne documentaire reste complète.

---

# 9. Responsabilités

Action Definition :

décrit.

Action Instance :

exécute.

Cette responsabilité ne peut être inversée.

---

# 10. Validation

Le document est conforme si :

✓ une définition peut être réutilisée ;

✓ plusieurs instances peuvent coexister ;

✓ aucune instance ne modifie sa définition.

---

# 11. Historique

Version 1.0

Première séparation officielle entre définition et instance d'action.
