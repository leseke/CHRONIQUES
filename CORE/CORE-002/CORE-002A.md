# CORE-002-A — Mission

> Version : 1.0
>
> Statut : Fondation
>
> Type : Mission
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir officiellement le concept d'Entity.

L'Entity constitue la primitive représentant tout élément pouvant exister dans Chroniques.

---

# 2. Mission

Une Entity fournit un support stable auquel peuvent être associés :

- des Components ;
- des Relations ;
- des Events ;
- un Lifecycle.

Une Entity ne porte aucune logique métier.

---

# 3. Portée

Une Entity peut représenter :

- un être vivant ;
- un objet ;
- un lieu ;
- une organisation ;
- un phénomène ;
- un concept abstrait ;
- un système du monde.

Cette liste est illustrative et non limitative.

---

# 4. Principe

Une Entity existe indépendamment de ses états.

Les changements affectent ses Components ou ses Relations, sans remettre en cause son identité.

---

# 5. Responsabilités

L'Entity :

- existe ;
- est identifiable ;
- est composable ;
- peut être référencée.

Elle ne décide pas, ne calcule pas et n'exécute aucune logique.

---

# 6. Validation

Une Entity est conforme si :

✓ elle possède une identité stable ;

✓ elle peut recevoir des Components ;

✓ elle reste indépendante de toute logique métier.

---

# Historique

Version 1.0

Première définition officielle de la primitive Entity.
