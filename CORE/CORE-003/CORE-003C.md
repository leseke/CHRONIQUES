# CORE-003-C — Responsabilités

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les responsabilités exclusives d'un Component.

---

# 2. Responsabilité principale

Un Component décrit une partie de la composition d'une Entity.

Il constitue un conteneur conceptuel de données.

---

# 3. Responsabilités autorisées

Un Component peut :

- décrire une propriété ;
- porter des Values ;
- porter un State ;
- être référencé ;
- évoluer au cours du Lifecycle de son Entity.

---

# 4. Responsabilités interdites

Un Component ne doit jamais :

- prendre une décision ;
- exécuter une logique ;
- déclencher directement un Event ;
- modifier un autre Component.

Ces responsabilités appartiennent aux Systems.

---

# 5. Principe

Chaque Component possède une responsabilité unique.

Deux Components ne doivent pas décrire la même information.

---

# 6. Validation

Un Component est conforme si :

✓ sa responsabilité est clairement définie ;

✓ aucune logique n'y est implémentée ;

✓ il participe uniquement à la composition de son Entity.

---

# Historique

Version 1.0
