# CORE-005-J — Gouvernance

> Version : 1.0
>
> Statut : Fondation
>
> Type : Gouvernance
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les règles d'évolution de la primitive State.

---

# 2. Principe

La définition d'un State doit rester universelle et indépendante des mécaniques métier.

---

# 3. Évolution

Toute évolution doit :

- préserver les responsabilités ;
- respecter les invariants ;
- être documentée ;
- être validée par une ADR.

---

# 4. Compatibilité

Les évolutions ne doivent pas modifier le rôle des autres primitives.

---

# 5. Dépréciation

Une propriété peut être dépréciée.

La primitive State ne peut être supprimée.

---

# 6. Validation

Toute modification doit préserver la cohérence du Kernel.

---

# Historique

Version 1.0
