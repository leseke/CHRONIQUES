# CORE-005-E — Évolution

> Version : 1.0
>
> Statut : Fondation
>
> Type : Cycle conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir l'évolution d'un State.

---

# 2. Principe

Un State représente une condition à un instant donné.

Lorsque cette condition change, le State évolue.

---

# 3. Causes

CORE ne définit pas les causes de cette évolution.

Les causes appartiennent aux Events et aux Systems.

---

# 4. Continuité

L'évolution d'un State ne modifie pas :

- l'identité de l'Entity ;
- la responsabilité du Component.

Elle modifie uniquement la condition représentée.

---

# 5. Traçabilité

Toute évolution doit pouvoir être observée.

Le mode de traçabilité est défini par les bibliothèques spécialisées.

---

# 6. Validation

L'évolution est conforme si :

✓ elle conserve la responsabilité du State ;

✓ elle ne modifie pas l'identité de l'Entity ;

✓ elle reste indépendante de son implémentation.

---

# Historique

Version 1.0
