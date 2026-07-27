# CORE-001-A — Mission

Version : 1.0

Statut : Fondation

Type : Mission

Bibliothèque : CORE

---

# Objectif

Définir les principes fondamentaux constituant le noyau conceptuel de Chroniques.

CORE est la source officielle des concepts primitifs utilisés par l'ensemble du projet.

Aucune autre bibliothèque ne redéfinit ces concepts.

---

# Mission

CORE fournit le langage universel utilisé par :

- GDB
- ACT
- PLN
- TECH
- QA
- UX
- LORE

Chaque bibliothèque construit ses propres modèles à partir des concepts de CORE.

---

# Responsabilités

CORE définit uniquement les primitives.

CORE ne décrit jamais :

- une mécanique ;
- une civilisation ;
- un personnage ;
- une interface ;
- une implémentation.

---

# Philosophie

Plus le noyau est petit,

plus le projet est stable.

Chaque nouveau concept doit démontrer qu'il ne peut être exprimé à partir des primitives existantes.

---

# Contrat

Toute nouvelle bibliothèque dépend de CORE.

CORE ne dépend d'aucune bibliothèque métier.

---

# Validation

CORE est valide si :

✓ chaque concept est universel ;

✓ chaque concept est indépendant ;

✓ aucune primitive ne peut être exprimée par une autre.

---

# Historique

Version 1.0
Création de la bibliothèque CORE.
