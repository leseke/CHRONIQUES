# CORE-003-D — Composition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir la composition interne d'un Component.

---

# 2. Principe

Un Component est composé exclusivement d'informations conceptuelles.

Il ne contient aucun comportement.

---

# 3. Composition

Un Component peut contenir :

- une ou plusieurs Values ;
- un ou plusieurs States ;
- des References.

---

# 4. Évolution

Le contenu d'un Component peut évoluer.

Son rôle reste inchangé.

---

# 5. Minimalisme

Un Component contient uniquement les informations nécessaires à sa responsabilité.

Toute information sans lien direct avec cette responsabilité doit appartenir à un autre Component.

---

# 6. Validation

La composition est conforme si :

✓ elle reste cohérente ;

✓ elle respecte le principe de responsabilité unique ;

✓ elle ne contient aucune logique.

---

# Historique

Version 1.0
