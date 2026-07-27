# ACT-002-F — Modèle d'exécution

> Version : 1.1
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Maturité : 2
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

# 3bis. Pipeline complet, intégrant Intent, Plan et Outcome

La chaîne de la section 3 ne montre que la partie « exécution ». Le pipeline
complet, référencé notamment par la GDB [réf: GDB-002E], est le suivant :

Intent [réf: ACT-002-H]

↓ (un Planner sélectionne une ou plusieurs Action Definitions)

Plan [réf: ACT-002-I]

↓ (chaque étape du Plan instancie une Action)

Action Instance (voir chaîne d'exécution, section 3)

↓

Execution Engine → Effects → Events → World Update

↓ (le résultat observé est produit en parallèle de World Update)

Outcome [réf: ACT-002-G]

Un Intent ne produit jamais directement un Outcome : il doit toujours
traverser un Plan, au moins une Action Instance, et le moteur d'exécution.
Un Outcome ne remonte jamais vers l'Intent qui l'a motivé --- l'Intent ne
connaît pas les Outcomes qu'il a produits [réf: ACT-002-H, section
Indépendance] ; seul un nouvel Intent, éventuellement motivé par cet
Outcome, peut relancer le pipeline.

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

# 8bis. Taxonomie complète des conditions d'échec

Les quatre causes ci-dessus se répartissent dans trois catégories, qui ne se
résolvent pas de la même manière :

- **Échec d'invalidité interne** (précondition devenue fausse, contrainte
  violée) : l'Action Instance n'aurait jamais dû atteindre RUNNING. Elle
  passe directement à FAILED [réf: ACT-001-F] sans production d'Effects.
- **Échec de disparition** (acteur ou cible disparu) : l'Action Instance
  était valide à sa Préparation mais son environnement a changé pendant
  l'exécution. Les Effects déjà produits avant la disparition restent
  valides ; ceux qui en dépendaient sont annulés.
- **Échec de ressources** (une Ressource requise [réf: GDB-005B] n'est plus
  disponible au moment de l'Exécution, alors qu'elle l'était à la
  Préparation) : cas non couvert par la liste initiale. L'Action Instance
  passe à FAILED ; les ressources déjà réservées sont libérées.

Invariant commun aux trois catégories : un échec produit toujours au moins
un Event [réf: ACT-001-C, section 7], et ne laisse jamais le monde dans un
état où des ressources restent réservées sans qu'aucune Action Instance ne
les détienne encore.

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

Version 1.1 : ajout du pipeline complet intégrant Intent, Plan et Outcome
(section 3bis, corrige ACT-002-C01) et de la taxonomie complète des conditions
d'échec (section 8bis, corrige ACT-002-C03). En-tête mis en conformité avec
MASTER-004.

Version 1.0
