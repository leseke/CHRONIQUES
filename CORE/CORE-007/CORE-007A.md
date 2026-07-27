# CORE-007-A — Mission

> Version : 1.0
>
> Statut : Fondation
>
> Type : Mission
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir officiellement la primitive **Event**.

Un Event représente un fait ayant eu lieu dans la simulation.

---

# 2. Mission

L'Event documente une évolution du monde.

Il constitue une trace observable d'un changement.

---

# 3. Principe

Un Event ne provoque jamais un changement.

Il représente le fait que ce changement a eu lieu.

---

# 4. Portée

Un Event peut concerner :

- une Entity ;
- une Relation ;
- un State ;
- plusieurs éléments simultanément.

---

# 5. Responsabilités

Un Event :

- décrit un fait ;
- possède une temporalité ;
- peut être référencé.

Il ne contient aucune logique métier.

---

# 6. Validation

Un Event est conforme si :

✓ il décrit un fait observable ;

✓ il ne réalise aucune action ;

✓ il reste indépendant de son implémentation.

---

# Historique

Version 1.0
