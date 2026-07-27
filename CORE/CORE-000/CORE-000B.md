# CORE-000B — Vision

> Version : 1.1
>
> Statut : Fondation
>
> Type : Vision
>
> Bibliothèque : CORE

---

# 1. Vision

Chroniques repose sur un Kernel documentaire minimal, stable et universel.

Le Kernel constitue la base conceptuelle de l'ensemble du projet.

Chaque concept fondamental possède une responsabilité unique et clairement définie.

Les primitives décrivent le monde ; elles n'en décrivent pas les comportements.

Les comportements, mécanismes et implémentations sont définis dans les bibliothèques spécialisées.

Cette séparation garantit la stabilité du modèle conceptuel malgré l'évolution des domaines métier.

---

# 2. Objectifs

Le Kernel doit rester :

- universel ;
- cohérent ;
- stable ;
- extensible ;
- indépendant des implémentations ;
- indépendant des technologies ;
- indépendant des domaines métier ;
- indépendant des choix de Game Design.

---

# 3. Position dans l'architecture

CORE constitue le niveau le plus fondamental de Chroniques.

Toutes les bibliothèques spécialisées héritent des concepts définis par CORE.

Les dépendances suivent exclusivement le sens suivant :

```text
CORE
    ↓
Bibliothèques spécialisées
    ↓
Documents métier
```

Aucune dépendance inverse n'est autorisée.

---

# 4. Vision documentaire

La documentation est organisée selon les principes suivants :

- une seule définition canonique par concept ;
- aucune duplication volontaire ;
- aucune contradiction entre bibliothèques ;
- spécialisation plutôt que redéfinition ;
- responsabilités clairement séparées.

Chaque document doit pouvoir être lu indépendamment tout en restant cohérent avec l'ensemble du dépôt.

---

# 5. Invariants

Les invariants suivants s'appliquent à toute la documentation Chroniques :

- CORE définit les concepts fondamentaux ;
- les bibliothèques spécialisées appliquent ces concepts ;
- une spécialisation ne modifie jamais la définition de son concept parent ;
- une définition canonique n'existe qu'à un seul endroit ;
- toute divergence est résolue au profit de CORE.

---

# 6. Évolution

Le Kernel est conçu pour évoluer lentement.

Toute modification d'un concept fondamental doit :

1. préserver la cohérence globale ;
2. maintenir la compatibilité documentaire ;
3. limiter les impacts sur les bibliothèques spécialisées ;
4. respecter les responsabilités établies.

---

# 7. Résultat attendu

Cette vision permet :

- un langage documentaire unique ;
- une architecture extensible ;
- une maintenance simplifiée ;
- une réduction des redondances ;
- une meilleure traçabilité des concepts ;
- une cohérence durable entre toutes les bibliothèques.

---

# Historique

## Version 1.1

- formalisation de la vision du Kernel ;
- ajout de la hiérarchie documentaire ;
- ajout des invariants de dépendance ;
- clarification des responsabilités entre CORE et les bibliothèques spécialisées ;
- définition des principes de gouvernance documentaire.

## Version 1.0

- Création du document.
