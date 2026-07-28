# CORE-002-E — Lifecycle

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir le cycle de vie d'une Entity.

---

# 2. Principe

Toute Entity possède un Lifecycle.

Le Lifecycle décrit les différentes phases de son existence.

---

# 3. Existence

Une Entity peut :

- être créée ;
- évoluer ;
- être désactivée ;
- être supprimée ou archivée selon les règles du système.

---

# 4. Continuité

L'identité de l'Entity reste inchangée durant tout son Lifecycle.

Les modifications concernent uniquement sa composition, son état ou ses relations.

---

# 5. Transitions

Les transitions du Lifecycle sont provoquées par des Events.

Une transition ne peut jamais être implicite.

---

# 6. Validation

Le Lifecycle est conforme si :

✓ chaque transition est explicite ;

✓ l'identité reste stable ;

✓ les transitions sont traçables.

---

# Historique

Version 1.0

Première définition du Lifecycle d'une Entity.
