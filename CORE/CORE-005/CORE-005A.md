# CORE-005-A — Mission

> Version : 1.0
>
> Statut : Fondation
>
> Type : Mission
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir officiellement la primitive **State**.

Un State représente la condition d'une Entity ou d'un Component à un instant donné.

---

# 2. Mission

Le State décrit une situation observable.

Il permet de représenter les informations susceptibles d'évoluer au cours du temps.

---

# 3. Principe

Le State ne définit pas les causes de son évolution.

Il représente uniquement la condition actuelle.

---

# 4. Portée

Un State peut représenter :

- une condition ;
- une situation ;
- une configuration ;
- un statut.

Ces catégories sont conceptuelles et non limitatives.

---

# 5. Responsabilités

Un State :

- décrit une condition ;
- peut évoluer ;
- peut être observé.

Il ne contient aucune logique métier.

---

# 6. Validation

Un State est conforme si :

✓ il représente une condition ;

✓ il reste indépendant des mécanismes qui le modifient ;

✓ il est descriptif.

---

# Historique

Version 1.0
