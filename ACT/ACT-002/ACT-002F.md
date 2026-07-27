# ACT-002-F — Modèle d'exécution

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# 1. Objectif

Définir le modèle officiel d'exécution des actions.

Ce modèle garantit que toutes les actions suivent le même processus, indépendamment de leur nature.

---

# 2. Principe

Une Action Instance n'exécute aucune logique.

Elle représente uniquement un état.

L'exécution est assurée par un moteur spécialisé.

---

# 3. Chaîne d'exécution

Action Definition

↓

Action Contract

↓

Action Instance

↓

Execution Engine

↓

Effects

↓

Events

↓

World Update

---

# 4. Responsabilités

Action Definition

Décrit.

Action Contract

Spécifie.

Action Instance

Représente.

Execution Engine

Interprète.

World

Évolue.

---

# 5. Immutabilité

Pendant son exécution :

- la définition reste immuable ;
- le contrat reste immuable.

Seule l'instance évolue.

---

# 6. Séparation

Le moteur d'exécution ne connaît pas :

- les interfaces utilisateur ;
- les animations ;
- les effets visuels ;
- le réseau.

Il applique uniquement les règles du contrat.

---

# 7. Déterminisme

À contexte identique,

une même Action Definition,

avec les mêmes paramètres,

doit produire le même résultat.

Les exceptions (aléatoire, physique, intervention externe) doivent être explicitement documentées dans le contrat.

---

# 8. Gestion des erreurs

Le moteur peut interrompre une action si :

- une précondition devient fausse ;
- une contrainte est violée ;
- l'acteur disparaît ;
- la cible devient invalide.

L'interruption doit produire un événement.

---

# 9. Contrat

Le moteur ne peut jamais modifier une Action Definition.

Il ne manipule que des Action Instances.

---

# 10. Validation

Le modèle est conforme si :

✓ les responsabilités sont séparées ;

✓ le moteur reste générique ;

✓ toutes les actions suivent le même pipeline.

---

# Historique

Version 1.0
