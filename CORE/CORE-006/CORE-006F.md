# CORE-006-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes applicables à la primitive Relation.

---

# 2. Participants

Une Relation doit relier au minimum deux Entities.

Le nombre maximal de participants n'est pas limité par CORE.

---

# 3. Nature

Une Relation ne peut relier que des Entities.

Elle ne relie jamais directement :

- des Components ;
- des Values ;
- des States.

---

# 4. Responsabilité

Une Relation décrit uniquement le lien existant entre ses participants.

---

# 5. Évolution

Une Relation peut apparaître, évoluer ou disparaître.

Ces évolutions n'affectent pas directement les Entities concernées.

---

# 6. Neutralité

Une Relation ne contient :

- aucune logique métier ;
- aucune décision ;
- aucun comportement.

---

# 7. Validation

Une Relation est conforme si :

✓ elle relie explicitement plusieurs Entities ;

✓ elle respecte le principe de responsabilité unique ;

✓ elle reste purement descriptive.

---

# Historique

Version 1.0
