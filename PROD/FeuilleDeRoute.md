# Chroniques — Feuille de Route V2.6

> Version : 2.6
> Statut : Officiel
> Type : Roadmap
> Maturité : 2
> Bibliothèque : PROD

---

# Vision

Chroniques est un moteur de simulation narratif sur lequel un jeu est construit.

Le développement suit une approche **Documentation First** : toute règle ou architecture structurante est reliée à une autorité documentaire avant son implémentation, sauf documentation ENGINE explicitement rétroactive d'un code historique existant.

Conformément à MASTER-006 v1.1, les incréments validés sont distingués des points de consolidation documentaire : TECH, roadmap, README et audit transverse sont synchronisés lorsqu'un jalon significatif le justifie.

---

# Ce qui change par rapport à la V2.5

La V2.6 enregistre le premier bloc consolidé de **décision autonome par besoins** de v0.4 — Le monde vivant.

Principales évolutions depuis V2.5 :

- `ENGINE-011 — Décision autonome par besoins` validée / Maturité 4 ;
- `ENGINE-012 — Alimentation autonome minimale` validée / Maturité 4 ;
- première politique concrète `NeedsIntentSource` ;
- repos autonome piloté par Fatigue ;
- alimentation autonome pilotée par Faim et disponibilité réelle d'une nourriture accessible ;
- création et validation de `PAT-001 — Repos` / `VERB-001 — Se reposer` ;
- création et validation de `PAT-002 — Alimentation` / `VERB-002 — Manger` ;
- arbitrage déterministe entre Faim et Fatigue ;
- Cibles concrètes désormais portées par le Plan ;
- produit alimentaire minimal persisté ;
- séparation du `PipelineRunner` et des applicateurs d'Effects ;
- validation technique portée à **178 / 178 tests réussis** ;
- création de `TECH-004 — Décision autonome par besoins` ;
- création d'un contrôle de concordance de jalon dans `AUDIT/AUDIT-AUTONOMIE-BESOINS-Consolidation.md` ;
- formalisation dans MASTER-006 v1.1 de la distinction entre validation courante et consolidation documentaire.

v0.4 reste ouverte : le monde ne sait pas encore travailler, produire, échanger, mémoriser ou évoluer sur plusieurs générations de manière autonome complète.

---

# Principes de développement

## 1. Le code suit les spécifications

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

## 2. Validation et consolidation

Une fonctionnalité structurante suit :

```text
spécification
↓
implémentation
↓
build
↓
tests
↓
validation
```

Les documents directement concernés sont synchronisés immédiatement.

La consolidation transverse est déclenchée à un jalon significatif conformément à MASTER-006 v1.1.

## 3. Data-driven

Les données métier spécifiques ont vocation à être externalisées lorsqu'elles peuvent l'être.

## 4. Déterminisme

À état, seed, entrées et ordre identiques, la simulation doit produire le même résultat.

## 5. Séparation des responsabilités

- MASTER : gouvernance ;
- CORE : primitives ;
- GDB : règles et modèles de simulation ;
- ACT : langage universel des Actions ;
- ENGINE : architecture attendue ;
- CHRONIQUES-ENGINE : implémentation exécutable ;
- TECH : documentation de l'implémentation validée.

---

# Architecture moteur actuelle

```text
World
│
├── Kernel
├── World.Events
├── Scheduler / Simulation Loop
├── Systems
├── Action Pipeline
├── Session / boucle de vie minimale
├── Autonomy
│   ├── orchestration habitants
│   └── décision par besoins
├── Persistence / Serialization
└── Resource Management futur
```

## World.Events

`World.Events` reste un journal d'observabilité, jamais un EventBus entre Systems.

## Scheduler

Le Scheduler reste l'autorité sur l'avancement du Tick et l'ordre des Systems.

## LifeSession

`LifeSession` orchestre le personnage contrôlé et la continuité minimale avec l'héritier.

## Autonomy

L'autonomie dispose maintenant de deux couches validées :

```text
Scheduler
↓
AutonomousActionSystem
↓
NeedsIntentSource
↓
Intent?
↓
IAutonomousIntentExecutor
↓
NeedsPlanner
↓
PipelineRunner
↓
World
```

La décision métier actuellement couverte reste volontairement minimale :

```text
Fatigue → Se reposer
Faim + nourriture accessible → Manger
```

---

# Feuille de route par versions

# v0.1 — Le noyau

Fondations :

- Entity ;
- Component ;
- State ;
- Value ;
- Relation ;
- World ;
- Tick ;
- Lifecycle ;
- RNG déterministe ;
- première sérialisation.

Statut architectural : ✅

---

# v0.2 — Infrastructure de simulation

Infrastructure :

- `World.Events` ;
- Scheduler ;
- Systems ;
- Persistence / Serialization ;
- besoins ;
- vieillissement ;
- cycle de vie.

Statut architectural : ✅

---

# v0.3 — Une vie entière

Objectif : assembler les briques nécessaires à une continuité minimale d'une vie contrôlée.

## État validé

```text
Action Pipeline                ✅ ENGINE-006
Relations                      ✅ ENGINE-008
Compétences                    ✅ ENGINE-008
Héritage minimal               ✅ ENGINE-008
LifeSession                    ✅ ENGINE-009
Mort → héritier → continuité   ✅ ENGINE-009
```

Documentation TECH :

```text
TECH-001 — Systems de population
TECH-002 — Boucle de vie minimale
```

Validation de référence :

```text
134 / 134 tests réussis
```

---

# v0.4 — Le monde vivant

Objectif : donner au monde une existence indépendante de l'intervention permanente du joueur.

Cible de phase :

- habitants autonomes ;
- économie qui évolue ;
- événements du monde ;
- Mémoire du Monde ;
- évolution crédible sur plusieurs générations.

## Lot 1 — Orchestration autonome

Statut : ✅ Validé

Spécification :

```text
ENGINE-010 — Orchestration des habitants autonomes
```

Implémentation principale :

```text
IAutonomousIntentSource
IAutonomousIntentExecutor
AutonomousActionSystem
```

Validation initiale :

```text
146 / 146 tests réussis
```

Documentation :

```text
TECH-003 — Orchestration des habitants autonomes
```

Constat historique :

```text
ENGINE-C06
→ Clos
```

---

## Lot 2 — Décision autonome minimale par besoins

Statut : ✅ Validé et consolidé

Spécifications :

```text
ENGINE-011 — Décision autonome par besoins
ENGINE-012 — Alimentation autonome minimale
```

Autorités métier et ACT principales :

```text
GDB-004B v1.2
GDB-005E v1.1
PAT-001 / VERB-001
PAT-002 / VERB-002
```

Capacités obtenues :

```text
Fatigue sous seuil
↓
Intent se_reposer
↓
VERB-001
↓
Fatigue restaurée
```

et :

```text
Faim sous seuil
+
nourriture accessible
↓
Intent manger
↓
VERB-002
↓
portion consommée
+
Faim restaurée
```

Lorsque les deux besoins sont actionnables :

```text
satisfaction la plus basse
→ retenue

égalité
→ Faim avant Fatigue
```

Le tie-break est technique et déterministe, pas narratif.

Validation consolidée :

```text
dotnet build
→ succès

dotnet test
→ 178 / 178 tests réussis
→ 0 échec
```

Documentation technique :

```text
TECH-004 — Décision autonome par besoins
```

Audit de jalon :

```text
AUDIT/AUDIT-AUTONOMIE-BESOINS-Consolidation.md
→ Clos
```

---

## Ce que Lot 2 ne ferme pas

Le moteur ne possède toujours pas :

- inventaire général ;
- propriété ;
- travail autonome ;
- économie autonome complète ;
- production alimentaire autonome ;
- achat/vente autonomes ;
- personnalité pondérée ;
- habitudes pondérées ;
- ambitions pondérées ;
- interactions sociales autonomes complètes ;
- événements du monde autonomes ;
- Mémoire du Monde opérationnelle.

---

## Prochaine frontière de v0.4

Le prochain lot doit augmenter la capacité du monde à vivre **sans intervention du joueur**, pas seulement ajouter un troisième besoin physiologique.

Priorité d'audit recommandée :

```text
travail autonome
+
économie autonome minimale
```

Pourquoi :

- MASTER-005 Phase 3 exige explicitement que les habitants travaillent ;
- la nourriture vient désormais d'une ressource réelle, ce qui rend naturel le prochain lien vers production, disponibilité et échange ;
- répéter simplement `Santé → se_soigner` ou `Moral → ...` augmenterait le catalogue de comportements sans encore faire vivre l'économie du monde.

Autorités à contrôler avant code :

```text
GDB-004A — Habitants du Monde
GDB-004B — Besoins
GDB-005 — Économie
GDB-012 — Métiers et activités
GDB-019 — Mécanismes économiques et commerciaux
ACT/PATTERNS
ACT/VERBS
```

Si les règles de décision professionnelle ou de production ne sont pas assez précises, elles devront être définies en GDB avant ENGINE.

---

## Critère de sortie v0.4

Le monde évolue de façon crédible pendant plusieurs générations sans intervention permanente du joueur.

Avec 178 / 178, Chroniques possède maintenant une **autonomie physiologique minimale**, mais pas encore un monde économiquement et socialement autonome.

v0.4 reste donc ouverte.

---

# v0.5 — La profondeur

Ajouts possibles selon les autorités :

- économie avancée ;
- métiers ;
- médecine ;
- justice ;
- crime ;
- politique ;
- religion ;
- combat ;
- patrimoine avancé.

Critère : trois parcours radicalement différents produisent des histoires profondément différentes.

---

# v0.6 — Les outils

Ajouts visés :

- éditeur de contenu ;
- debugger de simulation ;
- inspection du World ;
- diagnostics déterministes ;
- outils de production.

---

# v1.0 — Première alpha

Objectifs :

- boucle complète ;
- sauvegarde versionnée ;
- équilibrage ;
- interface aboutie ;
- direction artistique ;
- stabilité ;
- diagnostics suffisants.

---

# Workflow de développement

```text
MASTER / CORE / GDB / ACT
↓
ENGINE
↓
Implémentation
↓
Build
↓
Tests
↓
Validation courante
↓
point de consolidation si jalon significatif
↓
TECH / AUDIT / roadmap / README concernés
```

Aucun document TECH ne doit inventer une fonctionnalité inexistante.

Aucun code structurant ne doit introduire une règle sans autorité documentaire correspondante.

---

# Objectif long terme

Construire un moteur de simulation capable de faire vivre un monde autonome où :

- chaque personnage poursuit ses propres objectifs ;
- les relations évoluent naturellement ;
- l'économie fonctionne indépendamment du joueur ;
- les générations se succèdent ;
- le monde conserve une mémoire narrative ;
- les événements émergent de la simulation.

---

# Historique

## Version 2.6

- ENGINE-011 et ENGINE-012 validées / Maturité 4 ;
- suite globale portée à **178 / 178 tests réussis** ;
- PAT-001 / VERB-001 et PAT-002 / VERB-002 validés ;
- décision autonome repos + alimentation consolidée ;
- arbitrage déterministe Faim/Fatigue enregistré ;
- produit alimentaire minimal et consommation réelle validés ;
- création de TECH-004 ;
- création de l'audit de consolidation du bloc ;
- MASTER-006 v1.1 formalise validation courante vs consolidation documentaire ;
- prochaine frontière v0.4 recentrée sur travail autonome et économie minimale plutôt que sur l'ajout mécanique d'un troisième besoin.

## Version 2.5

- ENGINE-010 validée / Maturité 4 ;
- premier raccordement d'habitants autonomes au Scheduler validé ;
- suite globale portée à 146 / 146 ;
- création de TECH-003 ;
- clôture d'ENGINE-C06 ;
- politique de décision laissée comme prochaine frontière.

## Version 2.4

- ENGINE-009 validée / Maturité 4 ;
- boucle de vie minimale v0.3 validée ;
- suite portée à 134 / 134 ;
- création de TECH-002 ;
- ouverture de la préparation v0.4.

## Version 2.3

- alignement de la roadmap sur l'architecture documentaire et moteur ;
- ENGINE-008 validée ;
- cible v0.3 clarifiée.

## Version 2.2

- introduction de la bibliothèque ENGINE et du workflow Documentation → Code → Tests → TECH.

## Version 2.1

- ordre des phases aligné sur MASTER-005 ;
- suppression des duplications de décisions techniques.

## Version 2.0

- remplace la V1 et intègre les décisions architecturales initiales.
