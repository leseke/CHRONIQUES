# CORE-002-B — Définition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Définition
>
> Bibliothèque : CORE

---

# 1. Définition

Une Entity est une primitive représentant un élément identifiable pouvant exister dans la simulation.

Elle constitue le point d'ancrage de toutes les informations qui lui sont associées.

---

# 2. Caractéristiques

Une Entity :

- possède une identité stable ;
- peut recevoir des Components ;
- peut participer à des Relations ;
- peut être la source ou la cible d'Events ;
- possède un Lifecycle.

---

# 3. Neutralité

Une Entity ne possède aucune signification métier intrinsèque.

Sa nature est déterminée exclusivement par les Components qui lui sont associés.

---

# 4. Composition

Une Entity peut être composée de zéro, un ou plusieurs Components.

L'absence d'un Component ne remet pas en cause son existence.

---

# 5. Persistance

Une Entity conserve son identité durant toute son existence.

Ses Components peuvent être ajoutés, modifiés ou supprimés selon les règles métier.

---

# 6. Validation

La définition est conforme si :

✓ l'Entity reste indépendante ;

✓ les comportements sont externalisés ;

✓ la composition est privilégiée à l'héritage.

---

# Historique

Version 1.0

Première définition normative d'une Entity.
