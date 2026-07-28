# CORE-010-J — Gouvernance

> Version : 1.0
>
> Statut : Fondation
>
> Type : Gouvernance
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les règles d'évolution de la primitive Lifecycle.

---

# 2. Principe

Lifecycle doit rester une primitive universelle de représentation de la continuité.

Il ne doit jamais évoluer vers un mécanisme d'exécution ou de décision.

---

# 3. Évolution

Toute évolution doit :

- préserver les invariants ;
- respecter la neutralité conceptuelle ;
- être documentée ;
- être validée par une ADR.

---

# 4. Compatibilité

Les évolutions ne doivent pas remettre en cause les responsabilités des autres primitives du Kernel.

---

# 5. Dépréciation

Une propriété peut être dépréciée.

La primitive Lifecycle ne peut être supprimée.

---

# 6. Validation

Toute modification doit préserver le rôle de Lifecycle comme représentation descriptive d'une continuité.

---

# Historique

Version 1.0
