# CORE-005-B — Définition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Définition
>
> Bibliothèque : CORE

---

# 1. Définition

Un State est une représentation cohérente de la condition actuelle d'une Entity ou d'un Component.

---

# 2. Nature

Un State est descriptif.

Il ne possède aucun comportement.

---

# 3. Composition

Un State est constitué d'une ou plusieurs Values.

CORE n'impose aucune structure particulière.

---

# 4. Temporalité

Un State est toujours valable pour un instant donné.

Lorsque les informations évoluent, un nouveau State remplace le précédent.

---

# 5. Neutralité

Le State ne contient :

- aucune logique ;
- aucune règle ;
- aucune décision.

---

# 6. Validation

La définition est conforme si :

✓ le State représente une condition ;

✓ il est composé de Values ;

✓ il reste indépendant de son implémentation.

---

# Historique

Version 1.0
