# CORE-003-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes auxquelles tout Component doit se conformer.

---

# 2. Dépendance

Un Component ne peut exister sans être associé à une Entity.

---

# 3. Responsabilité

Chaque Component possède une responsabilité unique.

Cette responsabilité ne doit pas être partagée avec un autre Component.

---

# 4. Neutralité

Un Component ne contient aucune logique métier.

Il ne prend aucune décision et n'exécute aucun traitement.

---

# 5. Cohérence

Les informations contenues dans un Component doivent être cohérentes avec sa responsabilité.

---

# 6. Évolution

Le contenu d'un Component peut évoluer.

Sa responsabilité reste stable.

---

# 7. Validation

Un Component est conforme si :

✓ il possède une responsabilité unique ;

✓ il est rattaché à une Entity ;

✓ il ne contient aucune logique.

---

# Historique

Version 1.0
