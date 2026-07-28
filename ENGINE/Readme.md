# ENGINE

> Version : 1.0
> Statut : Stable
> Famille : ENGINE

⸻

# 1. Objectif

La bibliothèque **ENGINE** décrit l'architecture fonctionnelle et technique du moteur de simulation de Chroniques.

Elle constitue le lien entre les spécifications conceptuelles (MASTER, CORE, ACT...) et leur implémentation dans le dépôt **CHRONIQUES-ENGINE**.

ENGINE définit les responsabilités des différents sous-systèmes du moteur, leurs interactions, leurs invariants ainsi que les contrats qu'ils doivent respecter.

Elle ne contient aucun code source.

---

# 2. Position dans l'architecture documentaire

Le projet Chroniques suit une approche **Documentation First**.

Chaque niveau documentaire possède une responsabilité clairement définie.

```text
MASTER
│
├── Vision
├── Principes
└── Architecture globale

        │
        ▼

CORE
│
├── Concepts fondamentaux
├── Monde
├── Entités
├── États
└── Relations

        │
        ▼

ACT
│
├── Intent
├── Plan
├── Action
└── Outcome

        │
        ▼

ENGINE
│
├── Architecture du moteur
├── Scheduler
├── EventBus
├── Pipeline
├── Persistence
└── Infrastructure

        │
        ▼

CHRONIQUES-ENGINE
(Code)

        │
        ▼

TECH
(Documenté à partir du code)
```

---

# 3. Responsabilités

ENGINE décrit uniquement les mécanismes internes du moteur.

Exemples :

- EventBus
- Scheduler
- Tick Loop
- Pipeline d'exécution
- Persistance
- Sérialisation
- Gestion des ressources
- Boucle de simulation
- Infrastructure ECS
- Cycle de vie du monde

ENGINE ne décrit jamais :

- les règles métier ;
- les comportements des personnages ;
- les mécaniques de jeu ;
- les concepts narratifs.

Ces sujets appartiennent respectivement à CORE et ACT.

---

# 4. Philosophie

ENGINE suit les principes suivants.

## Documentation First

Toute fonctionnalité importante du moteur doit être documentée avant son implémentation.

---

## Contrat avant implémentation

Chaque composant possède un contrat décrivant :

- ses responsabilités ;
- ses entrées ;
- ses sorties ;
- ses invariants ;
- ses conditions de validation.

Le code implémente ce contrat.

---

## Implémentation indépendante

Les documents ENGINE restent indépendants du langage utilisé.

Ils décrivent des comportements.

Ils ne décrivent pas du code C#.

---

## Tests dérivés

Les tests unitaires sont directement dérivés des contrats définis dans ENGINE.

Le comportement attendu est donc défini avant l'implémentation.

---

## Documentation TECH

Une fois le composant implémenté et validé, sa documentation technique est produite dans la bibliothèque TECH.

TECH décrit le code existant.

ENGINE décrit le comportement attendu.

---

# 5. Organisation

Chaque document ENGINE décrit un composant unique.

Structure recommandée :

```
ENGINE-001 — EventBus

↓

ENGINE-002 — Scheduler

↓

ENGINE-003 — Simulation Loop

↓

ENGINE-004 — Action Pipeline

↓

ENGINE-005 — Persistence

↓

ENGINE-006 — Serialization

↓

ENGINE-007 — Resource Manager

↓

...
```

Chaque document suit la même structure documentaire.

---

# 6. Structure type

Chaque document ENGINE contient les sections suivantes.

1. Objectif

2. Principe

3. Responsabilités

4. Architecture

5. Flux

6. Contrat

7. Invariants

8. Validation

9. Historique

---

# 7. Relation avec le dépôt moteur

ENGINE documente le dépôt :

```
CHRONIQUES-ENGINE
```

Il constitue la référence utilisée pendant le développement.

Toute évolution importante du moteur doit d'abord être décrite dans ENGINE avant d'être implémentée.

---

# 8. Cycle de développement

Chaque composant suit le cycle suivant.

```text
Spécification ENGINE

↓

Validation

↓

Tests

↓

Implémentation

↓

Validation

↓

Documentation TECH
```

Ce processus garantit la cohérence entre la documentation et le moteur.

---

# 9. Évolution

La bibliothèque ENGINE est amenée à évoluer tout au long du développement.

Elle reste volontairement indépendante de toute implémentation particulière afin de permettre l'évolution du moteur sans remettre en cause son architecture documentaire.

---

# Historique

## Version 1.0

- Création de la bibliothèque ENGINE.
- Définition de son rôle dans l'architecture documentaire.
- Formalisation du processus Documentation → Tests → Implémentation → TECH.
