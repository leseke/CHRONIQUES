# CORE-002-C — Identité

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir l'identité d'une Entity.

L'identité permet de distinguer une Entity de toutes les autres durant toute son existence.

---

# 2. Principe

Toute Entity possède une identité.

Deux Entities distinctes ne peuvent jamais partager la même identité.

---

# 3. Stabilité

L'identité est immuable.

Elle ne change jamais durant le Lifecycle de l'Entity.

Les états, composants et relations peuvent évoluer.

L'identité demeure.

---

# 4. Unicité

Une identité est unique dans son domaine de validité.

Cette unicité garantit :

- la traçabilité ;
- les références ;
- la persistance ;
- les relations.

---

# 5. Neutralité

L'identité ne possède aucune signification métier.

Elle ne décrit :

- ni le type ;
- ni le rôle ;
- ni les propriétés.

Elle sert uniquement à identifier.

---

# 6. Utilisation

L'identité est utilisée pour :

- référencer une Entity ;
- établir des Relations ;
- produire des Events ;
- assurer la persistance.

---

# 7. Contraintes

Une identité :

- ne peut être réutilisée ;
- ne peut être modifiée ;
- ne peut être dupliquée.

---

# 8. Validation

Une identité est conforme si :

✓ elle est unique ;

✓ elle est stable ;

✓ elle est indépendante des données métier.

---

# Historique

Version 1.0

Première définition officielle de l'identité d'une Entity.
