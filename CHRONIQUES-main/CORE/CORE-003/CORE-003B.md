# CORE-003-B — Définition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Définition
>
> Bibliothèque : CORE

---

# 1. Définition

Un Component est une primitive attachée à une Entity afin de décrire une partie de sa composition.

---

# 2. Nature

Un Component n'existe jamais seul.

Il est toujours associé à une Entity.

---

# 3. Contenu

Un Component contient des données conceptuelles.

Il peut être constitué de :

- Values ;
- States ;
- références vers d'autres primitives.

---

# 4. Neutralité

Un Component ne contient :

- aucune logique métier ;
- aucun algorithme ;
- aucune règle de décision.

---

# 5. Réutilisation

Le même type de Component peut être utilisé par plusieurs catégories d'Entities.

---

# 6. Validation

La définition est conforme si :

✓ le Component reste indépendant ;

✓ il est exclusivement descriptif ;

✓ il est composable.

---

# Historique

Version 1.0

Première définition normative du Component.
