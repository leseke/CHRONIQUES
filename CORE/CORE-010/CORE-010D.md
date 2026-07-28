# CORE-010-D — Composition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir la composition conceptuelle de Lifecycle.

---

# 2. Principe

Lifecycle représente une continuité unique.

Il organise les éléments décrivant son évolution au cours du Time.

---

# 3. Composition

Un Lifecycle peut référencer :

- une primitive évolutive ;
- plusieurs States ;
- plusieurs Events ;
- le Time.

CORE n'impose aucun mode de représentation.

---

# 4. Continuité

Tous les éléments référencés appartiennent à une même continuité.

Ils ne peuvent appartenir simultanément à plusieurs Lifecycles.

---

# 5. Neutralité

Lifecycle ne définit :

- aucun stockage ;
- aucune structure interne ;
- aucun mécanisme de calcul.

---

# 6. Validation

Lifecycle est conforme si :

✓ il représente une seule continuité ;

✓ tous les éléments appartiennent à cette continuité ;

✓ aucune implémentation n'est imposée.

---

# Historique

Version 1.0
