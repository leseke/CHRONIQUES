# ENGINE

> Version : 1.2
> Statut : Stable
> Maturité : 1
> Bibliothèque : ENGINE

⸻

# 1. Objectif

La bibliothèque **ENGINE** décrit l'architecture fonctionnelle et technique du moteur de simulation de Chroniques.

Elle constitue le lien entre les spécifications conceptuelles (MASTER, CORE, GDB, ACT...) et leur implémentation dans le dépôt **CHRONIQUES-ENGINE**.

ENGINE définit les responsabilités des différents sous-systèmes du moteur, leurs interactions, leurs invariants ainsi que les contrats qu'ils doivent respecter.

Elle peut contenir des esquisses de code (types, signatures, exemples courts) lorsqu'elles sont nécessaires pour exprimer un contrat avec précision. Ces esquisses sont des spécifications, pas des implémentations compilables — elles n'ont pas vocation à être copiées directement dans le dépôt moteur.

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

## Implémentation concrète, pas agnostique

Les documents ENGINE sont orientés vers l'implémentation C# du dépôt moteur.

Ils peuvent exprimer leurs contrats sous forme d'esquisses de types ou de signatures lorsque c'est la formulation la plus précise disponible.

Ils décrivent des comportements et des contrats, pas une implémentation complète ou compilable.

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

Structure actuelle :

```
ENGINE-000 — Fondations et gouvernance ENGINE
ENGINE-001 — Journal d'événements (World.Events)
ENGINE-002 — Kernel (primitives)
ENGINE-003 — Scheduler
ENGINE-004 — Systems (NeedsDecay, Aging, CalendrierSimule)
ENGINE-005 — Persistence
ENGINE-006 — Action Pipeline ✅ Validé
ENGINE-007 — Resource Manager (planifié, non créé)
ENGINE-008 — Systems de population (Relations, Compétences, Héritage)
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

## Version 1.2

- Correction de la doctrine « ne contient aucun code source » : ENGINE
  peut désormais contenir des esquisses de code (types, signatures) lorsqu'elles
  sont nécessaires pour exprimer un contrat avec précision. Ce changement
  entérine la pratique déjà établie par ENGINE-006 et ENGINE-008, et résout
  ENGINE-C07 (constat d'incohérence documentaire ouvert dans AUDIT-GLOBALE.md).
- Section « Implémentation indépendante » renommée « Implémentation concrète,
  pas agnostique » et mise en cohérence avec la pratique réelle.
- Section 5 (Organisation) mise à jour pour refléter la structure réelle de la
  bibliothèque ENGINE (ENGINE-000 à ENGINE-008), qui ne correspondait plus à la
  numérotation d'origine depuis ENGINE-000.
- Dépendances GDB ajoutées à l'objectif (ENGINE-008 introduit la première
  dépendance explicite vers GDB).

## Version 1.1

- audit formel (méthodologie MASTER-008) : mêmes corrections de
  conformité MASTER-004 qu'ENGINE-000 v1.1 --- `Famille` renommé
  `Bibliothèque`, `Maturité` ajouté (1, Fondations).

## Version 1.0

- Création de la bibliothèque ENGINE.
- Définition de son rôle dans l'architecture documentaire.
- Formalisation du processus Documentation → Tests → Implémentation → TECH.
