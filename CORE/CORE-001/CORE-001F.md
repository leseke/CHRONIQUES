# CORE-001-F — Dépendances

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les dépendances autorisées pour la bibliothèque CORE.

---

# 2. Dépendances entrantes

CORE dépend uniquement de :

- MASTER
- STANDARDS

Aucune autre bibliothèque ne peut être une dépendance de CORE.

---

# 3. Dépendances sortantes

Les bibliothèques suivantes dépendent de CORE :

- GDB
- ACT
- PLN
- TECH
- QA
- UX
- LORE

---

# 4. Principe

Les dépendances suivent toujours un sens unique.

MASTER

↓

STANDARDS

↓

CORE

↓

Bibliothèques métier

↓

TECH

---

# 5. Dépendances interdites

CORE ne peut jamais dépendre :

- de GDB ;
- d'ACT ;
- de PLN ;
- de TECH ;
- de QA ;
- d'UX.

---

# 6. Validation

Le modèle est conforme si :

✓ aucune dépendance circulaire n'existe ;

✓ toutes les dépendances sont descendantes ;

✓ CORE reste indépendant des concepts métier.

---

# Historique

Version 1.0

Création du modèle officiel de dépendances de CORE.
