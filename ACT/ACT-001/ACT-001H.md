# ACT-001-H — Terminologie officielle

> Version : 1.0
>
> Statut : Fondation
>
> Type : Glossaire de référence
>
> Bibliothèque : ACT
>
> Références :
> - MASTER
> - GDB
> - TECH
> - QA

---

# 1. Objectif

Définir la terminologie officielle utilisée dans la bibliothèque ACT.

Chaque terme possède une seule définition officielle.

Les documents ACT, TECH, QA et les commentaires de code doivent utiliser cette terminologie.

---

# 2. Principes

Un terme :

- possède une définition unique ;
- possède un sens unique ;
- ne peut pas être utilisé pour désigner plusieurs concepts.

Deux concepts différents ne doivent jamais partager le même terme.

---

# 3. Glossaire

## Action

Tentative entreprise par un acteur afin de produire un ou plusieurs effets.

---

## Acteur

Entité capable d'initier une action.

---

## Cible

Entité concernée par une action.

Une action peut posséder plusieurs cibles.

---

## Intention

Décision préalable motivant l'exécution d'une action.

Une intention n'est pas une action.

---

## Pattern

Modèle générique de gameplay partagé par plusieurs verbes.

---

## Verbe

Action fondamentale documentée dans ACT.

Chaque verbe appartient à un seul pattern.

---

## Effet

Résultat direct produit par une action.

Un effet décrit un changement potentiel.

Il ne modifie pas directement le monde.

---

## Événement

Notification émise à la suite d'un ou plusieurs effets.

Les événements permettent aux systèmes de réagir.

---

## Conséquence

Modification durable ou temporaire de l'état du monde après l'application des effets.

---

## Contexte

Ensemble des informations influençant une action.

---

## Condition

Prérequis nécessaire à l'exécution d'une action.

---

## Déclencheur

Élément provoquant le début d'une action.

---

## Transition

Passage d'un état d'action vers un autre.

---

## Cycle de vie

Succession des états traversés par une action.

---

## État

Situation courante d'une action.

---

## Résolution

Étape déterminant le résultat final d'une action.

---

## Composition

Association de plusieurs actions pour former une action plus complexe.

---

## Traçabilité

Capacité à suivre une action depuis son intention jusqu'à son archivage.

---

## Contrat

Ensemble des règles qu'une implémentation doit respecter.

---

## Simulation

Exécution cohérente des actions, effets, événements et modifications du monde.

---

# 4. Termes réservés

Les termes suivants sont réservés :

- Action
- Acteur
- Cible
- Pattern
- Verbe
- Effet
- Événement
- Contrat
- Transition
- Simulation

Ils ne doivent pas être utilisés avec un autre sens dans la documentation ou le code.

---

# 5. Conventions de nommage

Les noms doivent être :

- explicites ;
- stables ;
- indépendants du contexte métier ;
- compréhensibles sans ambiguïté.

Les synonymes sont à éviter dans les documents techniques.

---

# 6. Évolution

Toute création d'un nouveau terme doit :

- être justifiée ;
- être ajoutée à ce glossaire ;
- ne pas entrer en conflit avec un terme existant.

---

# 7. Contrat TECH

Les développeurs doivent utiliser les termes officiels dans :

- le code ;
- les commentaires ;
- les API ;
- les journaux ;
- les tests.

---

# 8. Contrat QA

Les scénarios de test doivent employer exclusivement la terminologie définie dans ce document.

---

# 9. Critères de validation

Le document est conforme si :

✓ chaque terme possède une définition unique ;

✓ aucune ambiguïté terminologique n'existe ;

✓ tous les documents ACT utilisent ce glossaire.

---

# 10. Historique

Version 1.0

Création du glossaire officiel de la bibliothèque ACT.
