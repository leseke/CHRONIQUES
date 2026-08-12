# Chroniques

**Chaque vie raconte une Chronique.**

> Version : 1.5  
> Statut : Officiel  
> Bibliothèque racine : CHRONIQUES

---

# Présentation

Ce dépôt constitue la base documentaire officielle de **Chroniques**.

Le code exécutable vit dans :

```text
CHRONIQUES-ENGINE
```

Chroniques suit une approche **Documentation First** : les règles métier, contrats d'Actions et architectures attendues sont définis dans leurs autorités avant implémentation, sauf documentation ENGINE explicitement rétroactive d'un code historique.

---

# Hiérarchie de travail

```text
MASTER
↓
CORE
↓
GDB
↓
ACT
↓
ENGINE
↓
CHRONIQUES-ENGINE
↓
Tests
↓
TECH
```

Aucune couche aval ne doit contredire une autorité amont applicable.

---

# Validation et consolidation

MASTER-006 v1.1 distingue :

```text
validation courante
≠
consolidation documentaire
```

Le jalon courant constitue un point de consolidation significatif : le moteur a fermé un bloc cohérent allant de la **production autonome** aux **Ambitions génériques**.

---

# Architecture documentaire

```text
CHRONIQUES/
│
├── MASTER/   gouvernance
├── CORE/     primitives
├── GDB/      règles de simulation
├── ACT/      langage des Actions
├── ENGINE/   architecture attendue
├── TECH/     implémentation validée
├── QA/
├── PROD/     roadmap
├── AUDIT/
├── ADR/
├── UX/
├── LORE/
├── ART/
├── AUDIO/
├── MKT/
└── README.md
```

---

# État ENGINE actuel

```text
ENGINE-006  Action Pipeline                          ✅ M4
ENGINE-008  Systems de population                    ✅ M4
ENGINE-009  Boucle de vie minimale                   ✅ M4
ENGINE-010  Orchestration habitants autonomes        ✅ M4
ENGINE-011  Décision autonome par besoins            ✅ M4
ENGINE-012  Alimentation autonome minimale           ✅ M4
ENGINE-013  Production autonome minimale             ✅ M4
ENGINE-014  Circulation autonome minimale            ✅ M4
ENGINE-015  Observation de l'exécution autonome      ✅ M4
ENGINE-016  Habitudes génériques minimales           ✅ M4
ENGINE-017  Ambitions génériques minimales           ✅ M4
```

`ENGINE-007` reste réservé au Resource Manager technique et n'est pas créé.

---

# ACT concret validé

Quatre chaînes concrètes sont désormais officielles :

```text
Entretien
↓
PAT-001 — Repos
↓
VERB-001 — Se reposer
```

```text
Entretien
↓
PAT-002 — Alimentation
↓
VERB-002 — Manger
```

```text
Transformation
↓
PAT-003 — Production
↓
VERB-003 — Produire une denrée
```

```text
Échange
↓
PAT-004 — Transfert
↓
VERB-004 — Donner une denrée
```

Habitudes et Ambitions n'ajoutent pas de Verbe par elles-mêmes : elles produisent des Intents dirigés vers des Actions déjà traitables.

---

# État moteur validé

Validation de référence au **12 août 2026** :

```text
dotnet build
→ succès

dotnet test
→ 291 / 291 tests réussis
→ 0 échec
```

Le moteur contient maintenant notamment :

```text
Kernel / World / Entity / Components
Lifecycle / Scheduler / Persistence
Action Pipeline
Relations / Compétences / Héritage
LifeSession
AutonomousActionSystem
CompositeAutonomousIntentSource
NeedsIntentSource
VoluntaryFoodTransferIntentSource
ProductiveActivityIntentSource
HabitIntentSource
AmbitionIntentSource
PipelineAutonomousIntentExecutor
HabitLearningObserver
HabitEvolutionSystem
AmbitionEvolutionSystem
```

---

# v0.4 — Le monde vivant

Le monde peut désormais produire une décision autonome suivant l'ordre défini par GDB-004A v1.3 :

```text
besoins physiologiques
↓
transfert volontaire
↓
production
↓
Habitudes
↓
Ambitions
↓
aucun Intent
```

La première famille capable de produire un Intent exécutable gagne.

Aucun score universel ne compare ces familles.

---

# Substrat économique matériel

Le moteur sait démontrer :

```text
ressource réelle
↓
production autonome
↓
stock A
↓
transfert volontaire A → B
↓
stock B
↓
consommation par B
```

Cette capacité repose principalement sur ENGINE-013/014 et est consolidée dans :

```text
TECH-005 — Production et circulation autonomes
```

Elle ne constitue pas encore une économie commerciale complète.

Restent notamment absents : monnaie, prix, vente, marché, salaire, employeur et formule offre/demande.

---

# Substrat cognitif générique

Le moteur sait également :

```text
observer Intent → Action → Outcome
↓
former des Habitudes par répétition
↓
les persister / sélectionner / renforcer / éroder
```

et :

```text
créer des Ambitions via des Types injectés
↓
évaluer leur Progrès
↓
les accomplir / abandonner
↓
les sélectionner par Intensité → Progrès → ancienneté
```

Cette capacité repose sur ENGINE-015/016/017 et est consolidée dans :

```text
TECH-006 — Cognition autonome générique
```

Aucune Habitude narrative concrète ni Type d'Ambition narratif n'est fourni par défaut.

---

# Persistance actuelle

Le World persiste notamment :

```text
FoodProductComponent
ResourceStockComponent
ProductionProvenanceComponent
HabitComponent
AmbitionComponent
```

Les règles et services runtime restent injectés et ne sont pas sérialisés.

---

# TECH actuel

```text
TECH-001 — Systems de population
TECH-002 — Boucle de vie minimale
TECH-003 — Orchestration des habitants autonomes
TECH-004 — Décision autonome par besoins
TECH-005 — Production et circulation autonomes
TECH-006 — Cognition autonome générique
```

---

# Audit de jalon courant

La progression ENGINE-013 à ENGINE-017 est contrôlée dans :

```text
AUDIT/AUDIT-MONDE-VIVANT-AUTONOMIE-Consolidation.md
→ Clos / M4
```

Le contrôle confirme la concordance GDB → ACT → ENGINE → code → tests → TECH à **291 / 291**.

`AUDIT-GLOBALE.md` conserve une synthèse historique ancienne et ne doit pas être interprété comme l'état courant tant qu'un audit global complet n'a pas réconcilié son en-tête sans écraser son backlog.

---

# Roadmap

La roadmap officielle est désormais :

```text
PROD/FeuilleDeRoute.md
→ V2.7
```

v0.4 reste ouverte : le critère de sortie exige encore une évolution crédible du monde sur plusieurs générations sans intervention permanente du joueur.

---

# Prochaine frontière

Le prochain bloc cognitif naturel est l'audit de :

```text
GDB-004D — Les Personnalités
```

Objectif potentiel :

```text
PersonalityComponent
+
Traits 0..100
+
Poids de référence
+
Inflexions identifiables
```

sans encore inventer de mapping Trait/Habitude ou Trait/Ambition concret.

En parallèle, l'économie commerciale reste bloquée tant que GDB-019 ne fournit pas des contrats déterministes suffisants pour prix, monnaie et marchés.

---

# Objectif long terme

Construire un moteur capable de faire vivre un monde autonome où :

- chaque personnage poursuit ses propres objectifs ;
- les relations évoluent ;
- l'économie fonctionne indépendamment du joueur ;
- les générations se succèdent ;
- le monde conserve une mémoire narrative ;
- les événements émergent de la simulation.

---

# Historique

## Version 1.5

- état moteur porté à 291 / 291 ;
- ENGINE-013 à ENGINE-017 intégrés au README ;
- production, circulation, observation, Habitudes et Ambitions consolidées ;
- TECH-005 et TECH-006 ajoutés ;
- audit de jalon autonomie productive et cognitive enregistré ;
- roadmap V2.7 enregistrée ;
- prochaine frontière identifiée : Personnalité générique.

## Version 1.4

- autonomie par besoins ENGINE-011/012 consolidée à 178 / 178 ;
- TECH-004 ajouté ;
- MASTER-006 v1.1 enregistré.

## Version 1.3

- ENGINE-010 validée à 146 / 146 ; TECH-003 ajouté.

## Version 1.2

- ENGINE-009 validée à 134 / 134 ; TECH-002 ajouté.
