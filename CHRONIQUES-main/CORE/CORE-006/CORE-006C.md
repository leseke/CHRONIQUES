# CORE-006-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives de la primitive Relation.

---

# 2. Responsabilité principale

Une Relation décrit un lien entre plusieurs Entities.

---

# 3. Responsabilités autorisées

Une Relation peut :

- connecter plusieurs Entities ;
- être créée ;
- évoluer ;
- être supprimée ;
- être référencée.

---

# 4. Responsabilités interdites

Une Relation ne doit jamais :

- modifier une Entity ;
- produire un Event ;
- prendre une décision ;
- exécuter une logique.

---

# 5. Principe

Une Relation décrit uniquement l'existence d'un lien.

La signification métier de ce lien appartient aux bibliothèques spécialisées.

---

# 6. Validation

Une Relation est conforme si :

✓ elle reste purement descriptive ;

✓ elle possède une responsabilité unique ;

✓ elle demeure indépendante du métier.

---

# Historique

Version 1.0
