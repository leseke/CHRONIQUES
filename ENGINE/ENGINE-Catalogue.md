# ENGINE — Catalogue

> Version : 1.2
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (CHRONIQUES-ENGINE), TECH, QA

---

# Objectif

Ce catalogue référence l'ensemble des documents constituant la
bibliothèque ENGINE, introduite par PROD-005 (Feuille de Route v2.2).

ENGINE décrit l'architecture fonctionnelle et technique du moteur ---
jamais les règles métier, qui appartiennent à CORE et ACT.

Comme pour ACT/CATALOG.md, ce catalogue distingue explicitement ce qui
existe dans le dépôt de ce qui est planifié mais non encore créé, et
signale les documents rédigés rétroactivement (le code existait avant
la spécification) plutôt que dans l'ordre prescrit par ENGINE-000,
section 3.

---

# Documents existants

## ENGINE-000 --- Principes d'architecture

Statut : Stable. Rédigé avant tout code ENGINE --- respecte l'ordre
Documentation First prescrit par lui-même.

## ENGINE-001 --- Journal d'événements du World

Statut : Stable (v2.0). Rédigé avant le code sous une forme
(Subscribe/Handler) jamais construite, puis révisé pour refléter le
mécanisme réellement implémenté (simple accumulation sur `World`). Voir
son Historique pour le détail de cette divergence et sa résolution.

## ENGINE-002 --- Kernel

Statut : Stable. **Rédigé rétroactivement** --- implémenté dès la v0.1
du moteur, avant la création de la bibliothèque ENGINE.

## ENGINE-003 --- Scheduler et boucle de simulation

Statut : Stable. **Rédigé rétroactivement** --- implémenté depuis la
v0.2 du moteur.

## ENGINE-004 --- Systems de simulation

Statut : Stable. **Rédigé rétroactivement** --- implémenté depuis la
v0.2 du moteur. Couvre `NeedsDecaySystem`, `AgingSystem`,
`CalendrierSimule`.

## ENGINE-005 --- Persistence et Serialization

Statut : Stable. **Rédigé rétroactivement** --- implémenté depuis la
v0.1 (World vide) et étendu en v0.2 (Components, Lifecycle).

## ENGINE-006 --- Action Pipeline

Statut : Validée, Maturité 4. Rédigé avant tout code (Maturité 2),
implémenté et testé (91/91 tests, 4 d'intégration de bout en bout via
un Verbe de démonstration), puis validé par le porteur du projet ---
vérification identifiant pour identifiant sans écart trouvé. Voir son
Historique v1.3.

## ENGINE-008 --- Systems de population (Relations, Compétences, Héritage)

Statut : Proposition, Maturité 2. Rédigé avant tout code, comme
ENGINE-006 --- traduit GDB-004C, GDB-004H et GDB-004J en architecture
concrète, condition préalable à la cible v0.3 de PROD/FeuilleDeRoute.md
(« relations, mémoire, compétences, héritage minimal »). Numéroté 008 et
non 007 --- 007 reste réservé au Resource Manager (voir ci-dessous),
sans rapport avec ce document.

---

# Chapitres planifiés, non créés

Annoncés par PROD-005 et par ENGINE-000/Readme, mais sans code ni
spécification existants --- rien à documenter rétroactivement, et
aucune spécification prématurée n'est rédigée par anticipation
(MASTER-006).

## ENGINE-007 --- Resource Manager

Gestion des ressources (mémoire, contenu externe chargé). Aucun code
existant à ce jour.

---

# Note sur la consolidation par rapport à l'organisation initiale

ENGINE-000, section 5, suggérait une organisation en documents séparés
pour EventBus, Scheduler, **Simulation Loop**, Action Pipeline,
Persistence, **Serialization**, Resource Manager. La documentation
rétroactive a consolidé :

- **Simulation Loop** dans ENGINE-003, aux côtés du Scheduler --- le
  code n'a jamais séparé les deux : `Scheduler.Tick` fait avancer le
  World *et* invoque les Systems, c'est la boucle elle-même ;
- **Serialization** dans ENGINE-005, aux côtés de la Persistence --- le
  code n'a jamais séparé les deux : `WorldRepository` sérialise et
  persiste dans la même classe, avec le même contrat.

Cette consolidation reflète le code existant (Maturité 3 exige une
correspondance identifiant pour identifiant) --- elle n'est pas un choix
arbitraire de ce catalogue. Si Simulation Loop ou Serialization
devenaient un jour des responsabilités réellement distinctes dans le
code, elles seraient alors séparées en documents propres, avec une
justification explicite tracée ici.

---

# Historique

## Version 1.2

- `ENGINE-006` (Action Pipeline) validé par le porteur du projet
  (v1.3, Statut Validée, Maturité 4) --- première spécification ENGINE à
  parcourir tout le cycle Spécification → Implémentation → Tests →
  Validation (ENGINE-000, section 8).
- `ENGINE-008` (Systems de population --- Relations, Compétences,
  Héritage) créé --- traduit GDB-004C, GDB-004H et GDB-004J en
  architecture concrète, condition préalable à la cible v0.3 de
  PROD/FeuilleDeRoute.md. Numéroté 008, pas 007 : 007 reste réservé au
  Resource Manager, toujours non créé (voir « Chapitres planifiés »).
  Deuxième document ENGINE rédigé avant tout code, comme ENGINE-006.
  Première dépendance ENGINE explicite envers GDB plutôt que ACT seul ---
  dépendance ajoutée à l'en-tête du catalogue.

## Version 1.1

- `ENGINE-006` (Action Pipeline) créé --- traduit ACT-002-D à J et
  ACT-004-A à ACT-010-A en architecture concrète, maintenant qu'ACT-001
  à ACT-010 sont tous créés. Premier document ENGINE rédigé avant tout
  code (Maturité 2), à la différence d'ENGINE-002 à 005.

## Version 1.0

- Création du catalogue, à l'occasion de la documentation rétroactive
  d'ENGINE-002 à ENGINE-005 (Kernel, Scheduler, Systems, Persistence),
  suite à la découverte que ces composants, déjà codés, n'avaient
  jamais reçu de spécification ENGINE.
