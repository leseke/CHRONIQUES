# CORE-007-J — Gouvernance

> Version : 1.0
>
> Statut : Fondation
>
> Type : Gouvernance
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les règles d'évolution de la primitive Event.

---

# 2. Principe

La définition d'un Event doit rester descriptive.

Elle ne doit jamais évoluer vers un mécanisme d'exécution.

---

# 3. Évolution

Toute évolution doit :

- préserver l'immutabilité ;
- respecter les invariants ;
- être documentée ;
- être validée par une ADR.

---

# 4. Compatibilité

Les évolutions ne doivent pas remettre en cause les autres primitives.

---

# 5. Dépréciation

Une propriété peut être dépréciée.

La primitive Event ne peut être supprimée.

---

# 6. Validation

Toute évolution doit préserver le rôle d'Event comme représentation immuable d'un fait.

---

# Historique

Version 1.0
