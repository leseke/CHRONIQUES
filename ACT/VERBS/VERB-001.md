# VERB-001 — Se reposer

> Version : 1.0
> Statut : Proposition
> Type : Verbe d'Action
> Maturité : 2
> Bibliothèque : ACT
> Dépendances : GDB-004B, ACT-002-B, ACT-002-C, ACT-002-E, ACT-008-A, PAT-001

---

# 1. Objectif

Définir le Verbe concret `Se reposer`, première capacité officiellement cataloguée dans VERBS.

VERB-001 spécialise PAT-001 afin de fournir une capacité exécutable répondant au besoin de repos défini par GDB-004B.

---

# 2. Chaîne de spécialisation

```text
Principe : Entretien
↓
PAT-001 : Repos
↓
VERB-001 : Se reposer
↓
Action exécutée
```

VERB-001 n'appartient à aucun autre Pattern.

---

# 3. Origine métier

GDB-004B définit le premier contrat autonome implémentable :

```text
Fatigue < seuil configuré
↓
Intent : se_reposer
```

VERB-001 représente la capacité ACT permettant de traiter cet Intent.

La règle de seuil reste en GDB/ENGINE et ne fait pas partie du Verbe.

---

# 4. Identifiants

Nom conceptuel :

```text
Se reposer
```

Identifiant VERBS :

```text
VERB-001
```

Objectif d'Intent actuellement associé :

```text
se_reposer
```

Identifiant technique d'Action Definition actuellement compatible :

```text
SeReposer
```

Ces formes servent des couches différentes et ne doivent pas être confondues.

---

# 5. Action Contract

VERB-001 respecte la structure de PAT-001 et ACT-002-E.

## Inputs

- un `Acteur` identifiable.

## Cible

Dans l'implémentation courante, l'Acteur est aussi la cible principale de l'effet de récupération.

Cela ne transforme pas VERB-001 en Interaction : aucune seconde Entity active ne produit une Action en réponse.

## Preconditions

Aucune Precondition métier supplémentaire n'est définie dans cette version.

L'éligibilité générale de l'Acteur reste soumise aux contrats ACT et ENGINE applicables.

## Constraints

Aucune Constraint métier supplémentaire n'est définie dans cette version.

## Costs

Aucun Cost universel n'est défini dans cette version.

## Effects

Après résolution réussie :

```text
satisfaction du besoin de repos
↑
```

Dans le modèle moteur actuel, cette satisfaction est représentée par :

```text
NeedsComponent.Fatigue
```

L'augmentation reste bornée par la plage GDB `0..100`.

## Events

L'implémentation actuelle publie le fait observable :

```text
besoin.fatigue.restauree
```

Cet Event décrit un fait produit par l'Action ; il n'est pas utilisé comme canal de coordination entre Systems.

---

# 6. Valeur de récupération

VERB-001 ne fixe pas dans cette version une quantité universelle de récupération.

Le moteur historique utilise actuellement une valeur concrète de restauration afin de rendre l'Action exécutable et testable.

Cette valeur relève du tuning tant qu'aucune autorité GDB ne la fixe comme règle de gameplay.

Ainsi :

```text
VERB-001
≠
constante universelle +20
```

---

# 7. Application des quatre tests ACT-008-A

## 1. Paramétrage

Aucun Verbe existant ne pouvait être paramétré pour répondre au besoin, puisque VERB-001 est le premier Verbe catalogué.

Résultat : non couvert.

## 2. Composition

Aucun ensemble de Verbes existants ne pouvait être composé pour produire le repos.

Résultat : non couvert.

## 3. Pattern existant

PAT-001 est créé pour la mécanique générique de Repos et VERB-001 en constitue la première spécialisation.

Résultat : VERB-001 appartient à PAT-001.

## 4. Nouveau Pattern

Le besoin de repos ne correspondait à aucun Pattern réel déjà catalogué.

La création de PAT-001 était donc nécessaire avant VERB-001.

---

# 8. Frontière avec ENGINE-011

ENGINE-011 décide si l'Intent `se_reposer` doit être produit à partir de la Fatigue.

VERB-001 ne décide jamais quand il faut se reposer.

```text
ENGINE-011
= décision

VERB-001
= capacité
```

---

# 9. Frontière avec le Planner

Le Planner transforme un Intent en Plan contenant une Action Definition correspondant à VERB-001.

VERB-001 ne définit pas :

- l'algorithme du Planner ;
- l'ordre global des Actions ;
- la fréquence de décision ;
- la relation entre Action et Tick.

---

# 10. Non-objectifs

VERB-001 ne définit pas :

- Dormir ;
- Faire une sieste ;
- Louer une chambre ;
- récupérer de la Santé ;
- récupérer du Moral ;
- consommer un objet ;
- une durée universelle de repos ;
- une qualité de sommeil.

Ces concepts ne doivent pas être ajoutés par extension implicite du mot « repos ».

---

# 11. Invariants

- VERB-001 spécialise exactement PAT-001.
- VERB-001 conserve le sens du Pattern Repos.
- L'Action possède un Acteur identifiable.
- L'effet principal contribue à restaurer le besoin de repos.
- Le Verbe ne fixe aucun seuil d'activation autonome.
- Le Verbe ne produit aucune mutation avant résolution réussie de l'Action.
- Le Verbe ne transforme pas un Event en mécanisme de coordination.
- La valeur numérique de récupération n'est pas une loi ACT dans cette version.

---

# 12. Contrat QA

La validation devra pouvoir démontrer au minimum :

1. la traçabilité complète `Principe → PAT-001 → VERB-001 → Action` ;
2. l'appartenance de VERB-001 à un seul Pattern ;
3. la compatibilité du contrat avec l'Action Definition existante ;
4. l'exécution d'un Intent `se_reposer` jusqu'à un Outcome résolu ;
5. la restauration effective de Fatigue après réussite ;
6. la publication du fait observable attendu ;
7. l'absence de mutation avant passage dans le pipeline d'Actions.

---

# 13. Critère de validation

VERB-001 permet-il de représenter sans ambiguïté la capacité « Se reposer » conformément à GDB-004B, PAT-001 et ACT, tout en restant distinct de la décision autonome qui choisit de l'utiliser ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# Historique

## Version 1.0

- création du premier Verbe concret officiel de Chroniques ;
- spécialisation de PAT-001 ;
- rattachement au contrat autonome `Fatigue → se_reposer` de GDB-004B ;
- séparation explicite entre capacité ACT, décision ENGINE et tuning d'implémentation.

---

Fin du document
