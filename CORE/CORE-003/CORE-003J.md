# CORE-003-J — Gouvernance

> Version : 1.0
>
> Statut : Fondation
>
> Type : Gouvernance
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les règles d'évolution de la primitive Component.

---

# 2. Principe

La définition d'un Component doit rester stable et indépendante de toute implémentation.

---

# 3. Évolution

Toute évolution doit :

- préserver la compatibilité conceptuelle ;
- respecter les invariants ;
- être documentée ;
- être validée par une ADR.

---

# 4. Dépréciation

Une propriété peut être dépréciée.

La primitive Component ne peut être supprimée.

---

# 5. Validation

Toute modification doit démontrer qu'elle améliore le modèle sans remettre en cause les autres primitives.

---

# Historique

Version 1.0
