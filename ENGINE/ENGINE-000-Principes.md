# ENGINE-000 — Principes d'architecture

> Version : 1.0
> Statut : Stable
> Famille : ENGINE

⸻

# 1. Objectif

Définir les principes fondamentaux qui gouvernent l'architecture du moteur Chroniques.

Ces principes constituent les règles communes à l'ensemble des composants du moteur.

Tout document de la bibliothèque ENGINE est réputé respecter ces principes, sauf mention explicite contraire.

---

# 2. Philosophie

Le moteur Chroniques est développé selon une approche **Documentation First**.

L'architecture est définie avant l'implémentation.

Le code constitue l'application d'une spécification validée.

Les tests vérifient la conformité du code à cette spécification.

---

# 3. Hiérarchie documentaire

Le développement du moteur suit l'ordre documentaire suivant.

```text
MASTER

↓

CORE

↓

ACT

↓

ENGINE

↓

Code

↓

Tests

↓

TECH
```

Chaque niveau dépend uniquement des niveaux précédents.

Aucun niveau ne doit modifier rétroactivement une spécification déjà validée sans justification explicite.

---

# 4. Déterminisme

Le moteur est déterministe.

À état initial identique et à entrées identiques, la simulation doit toujours produire exactement le même résultat.

Le déterminisme constitue une propriété fondamentale du moteur.

---

# 5. Séparation des responsabilités

Chaque composant possède une responsabilité unique.

Un composant ne doit jamais remplir simultanément plusieurs rôles indépendants.

Les responsabilités sont réparties entre les composants spécialisés.

---

# 6. Faible couplage

Les composants communiquent uniquement par des contrats clairement définis.

Ils ne doivent jamais dépendre directement de l'implémentation interne d'un autre composant.

Les dépendances circulaires sont interdites.

---

# 7. Contrats

Chaque composant possède un contrat décrivant :

- son objectif ;
- ses responsabilités ;
- ses entrées ;
- ses sorties ;
- ses invariants.

L'implémentation doit respecter ce contrat.

---

# 8. Infrastructure indépendante

Les composants d'infrastructure ne contiennent aucune logique métier.

Ils fournissent uniquement les mécanismes nécessaires au fonctionnement du moteur.

Ils sont notamment indépendants :

- du gameplay ;
- de la narration ;
- des règles de simulation ;
- des comportements des personnages.

---

# 9. Immutabilité

Lorsqu'un objet représente un fait historique ou un message, il est immuable.

Cette règle concerne notamment :

- les événements ;
- les snapshots ;
- les messages internes.

---

# 10. Tests

Toute nouvelle fonctionnalité importante doit être couverte par des tests unitaires.

Les tests sont dérivés directement des contrats définis dans ENGINE.

Ils constituent la preuve de conformité de l'implémentation.

---

# 11. Documentation technique

La bibliothèque TECH décrit uniquement du code effectivement implémenté.

Aucune fonctionnalité non développée ne doit apparaître dans TECH.

ENGINE décrit le comportement attendu.

TECH décrit le comportement réalisé.

---

# 12. Évolution

Les composants doivent pouvoir évoluer sans remettre en cause l'architecture générale du moteur.

Toute évolution majeure doit préserver la compatibilité avec les principes définis dans ce document.

Lorsqu'un principe ne peut plus être respecté, une Architecture Decision Record (ADR) doit être rédigée avant toute modification.

---

# 13. Validation

Une évolution du moteur est considérée conforme si :

- elle respecte les principes définis dans ce document ;
- elle respecte les contrats des composants concernés ;
- elle est couverte par des tests ;
- elle ne remet pas en cause le déterminisme du moteur.

---

# Historique

## Version 1.0

- Création des principes d'architecture de la bibliothèque ENGINE.
- Formalisation de la méthode Documentation → Code → Tests → TECH.
- Définition des principes communs applicables à l'ensemble du moteur.
