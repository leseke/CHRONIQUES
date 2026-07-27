# CORE-008-J — Gouvernance

> Version : 1.0
>
> Statut : Fondation
>
> Type : Gouvernance
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les règles d'évolution de la primitive Time.

---

# 2. Principe

Time doit rester une primitive universelle.

Il ne doit jamais dépendre d'un calendrier, d'une horloge ou d'une technologie.

---

# 3. Évolution

Toute évolution doit :

- préserver les invariants ;
- respecter la neutralité conceptuelle ;
- être documentée ;
- être validée par une ADR.

---

# 4. Compatibilité

Les évolutions ne doivent pas remettre en cause les autres primitives du Kernel.

---

# 5. Dépréciation

Une propriété peut être dépréciée.

La primitive Time ne peut être supprimée.

---

# 6. Validation

Toute modification doit renforcer la stabilité conceptuelle du Kernel.

---

# Historique

Version 1.0
