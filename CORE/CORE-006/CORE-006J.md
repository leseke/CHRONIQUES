# CORE-006-J — Gouvernance

> Version : 1.0
>
> Statut : Fondation
>
> Type : Gouvernance
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les règles d'évolution de la primitive Relation.

---

# 2. Principe

La définition d'une Relation doit rester universelle.

Elle ne doit jamais dépendre d'un domaine métier particulier.

---

# 3. Évolution

Toute évolution doit :

- préserver les responsabilités ;
- respecter les invariants ;
- être documentée ;
- être validée par une ADR.

---

# 4. Compatibilité

Les évolutions ne doivent pas remettre en cause les autres primitives du Kernel.

---

# 5. Dépréciation

Une propriété peut être dépréciée.

La primitive Relation ne peut être supprimée.

---

# 6. Validation

Toute évolution doit améliorer le modèle sans rompre sa cohérence.

---

# Historique

Version 1.0
