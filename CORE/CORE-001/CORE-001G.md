# CORE-001-G — Invariants

> Version : 1.0
>
> Statut : Fondation
>
> Type : Invariants
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les propriétés fondamentales qui demeurent vraies pour l'ensemble des primitives de CORE.

Ces invariants garantissent la stabilité du noyau conceptuel de Chroniques.

---

# 2. Invariant 1 — Universalité

Toute primitive définie dans CORE est universelle.

Elle ne dépend :

- ni d'une époque ;
- ni d'une civilisation ;
- ni d'un gameplay ;
- ni d'une implémentation.

---

# 3. Invariant 2 — Responsabilité unique

Chaque primitive possède une responsabilité unique.

Une primitive ne doit jamais remplir plusieurs rôles conceptuels.

---

# 4. Invariant 3 — Non-duplication

Une primitive ne peut être définie qu'une seule fois.

Les autres bibliothèques la référencent sans la redéfinir.

---

# 5. Invariant 4 — Indépendance

Les primitives sont indépendantes des mécaniques métier.

Aucune primitive ne contient une règle de gameplay.

---

# 6. Invariant 5 — Composition

Les modèles complexes sont obtenus par composition de primitives.

Ils ne créent jamais de nouvelles primitives implicites.

---

# 7. Invariant 6 — Traçabilité

Toute donnée manipulée dans Chroniques doit pouvoir être reliée à une ou plusieurs primitives de CORE.

---

# 8. Invariant 7 — Cohérence

Les primitives doivent pouvoir coexister sans contradiction.

Toute évolution doit préserver cette cohérence.

---

# 9. Contrat

Aucun document ne peut modifier ces invariants sans décision d'architecture documentée.

---

# 10. Validation

CORE respecte ses invariants si :

✓ chaque primitive reste universelle ;

✓ aucune duplication n'apparaît ;

✓ la cohérence conceptuelle est maintenue.

---

# Historique

Version 1.0

Première définition officielle des invariants de CORE.
