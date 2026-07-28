# CORE-006-D — Composition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir la composition d'une Relation.

---

# 2. Principe

Une Relation relie deux ou plusieurs Entities.

Elle peut également posséder son propre State.

---

# 3. Composition

Une Relation est composée de :

- participants ;
- State ;
- Values ;
- References.

---

# 4. State

Le State décrit la condition actuelle de la Relation.

Exemples conceptuels :

- active ;
- suspendue ;
- terminée.

Ces exemples sont illustratifs.

---

# 5. Évolution

Le State d'une Relation peut évoluer sans modifier les Entities concernées.

---

# 6. Séparation des responsabilités

Les informations concernant le lien appartiennent à la Relation.

Les informations concernant une Entity appartiennent à cette Entity.

---

# 7. Validation

Une Relation est conforme si :

✓ elle relie explicitement plusieurs Entities ;

✓ son State décrit uniquement le lien ;

✓ aucune logique métier n'est embarquée.

---

# Historique

Version 1.0
