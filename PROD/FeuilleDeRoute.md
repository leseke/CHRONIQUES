# Chroniques — Feuille de Route V2.7

> Version : 2.7
> Statut : Officiel
> Type : Roadmap
> Maturité : 2
> Bibliothèque : PROD

---

# Vision

Chroniques est un moteur de simulation narratif sur lequel un jeu est construit.

Le développement suit une approche **Documentation First** : les règles et architectures structurantes sont reliées à leurs autorités avant implémentation, sauf documentation ENGINE explicitement rétroactive d'un code historique.

Conformément à MASTER-006 v1.1 :

```text
validation courante
≠
consolidation documentaire
```

La V2.7 correspond à un nouveau point de consolidation significatif de **v0.4 — Le monde vivant**.

---

# Ce qui change par rapport à V2.6

V2.6 s'arrêtait à l'autonomie physiologique minimale à `178 / 178`.

Depuis, Chroniques a obtenu deux nouveaux blocs cohérents.

## Substrat économique matériel

```text
ENGINE-013 — Production autonome minimale
ENGINE-014 — Circulation autonome minimale
```

Capacité :

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
consommation
```

Nouvelles chaînes ACT validées :

```text
Transformation
↓
PAT-003 Production
↓
VERB-003 Produire une denrée
```

```text
Échange
↓
PAT-004 Transfert
↓
VERB-004 Donner une denrée
```

## Substrat cognitif générique

```text
ENGINE-015 — Observation de l'exécution autonome
ENGINE-016 — Habitudes génériques minimales
ENGINE-017 — Ambitions génériques minimales
```

Capacité :

```text
Intent / Action / Outcome observables
↓
formation et évolution d'Habitudes
↓
création et progression d'Ambitions
↓
Intents cognitifs
↓
ACT
```

Validation globale :

```text
dotnet build
→ succès

dotnet test
→ 291 / 291 tests réussis
→ 0 échec
```

Consolidation :

```text
TECH-005 — Production et circulation autonomes
TECH-006 — Cognition autonome générique
AUDIT/AUDIT-MONDE-VIVANT-AUTONOMIE-Consolidation.md
```

---

# Principes de développement

## Documentation First

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

## Déterminisme

À état, seed, configuration et ordre identiques, la simulation produit le même résultat observable.

## Composition

Les nouvelles capacités s'intègrent par Components, Systems, resolvers, rules, planners, execution engines et applicateurs injectés plutôt que par un contrôleur métier central.

## Frontières explicites

Un framework générique ne transforme jamais un exemple documentaire en comportement canonique.

---

# Architecture moteur actuelle

```text
World
│
├── Kernel
├── World.Events
├── Scheduler
├── Systems
├── Persistence
├── Action Pipeline
├── Session / LifeSession
└── Autonomy
    ├── besoins
    ├── transfert volontaire
    ├── production
    ├── observation d'exécution
    ├── Habitudes génériques
    └── Ambitions génériques
```

Ordre autonome courant, défini par GDB-004A v1.3 :

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

Aucun score universel inter-familles n'est introduit.

---

# Feuille de route par versions

# v0.1 — Le noyau

```text
Entity / Component / State / Value
Relation / World / Tick / Lifecycle
RNG déterministe / première sérialisation
```

Statut architectural : ✅

---

# v0.2 — Infrastructure de simulation

```text
World.Events
Scheduler
Systems
Persistence
Besoins
Vieillissement
Cycle de vie
```

Statut architectural : ✅

---

# v0.3 — Une vie entière

```text
ENGINE-006 Action Pipeline            ✅
ENGINE-008 Population                  ✅
ENGINE-009 LifeSession                 ✅
Mort → héritier → continuité           ✅
```

Validation de référence du jalon : `134 / 134`.

TECH : `TECH-001`, `TECH-002`.

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

```text
ENGINE-010
→ AutonomousActionSystem
→ 146 / 146 à validation
→ TECH-003
```

Statut : ✅ Validé

## Lot 2 — Besoins autonomes

```text
ENGINE-011 / ENGINE-012
→ repos + alimentation
→ 178 / 178 à consolidation
→ TECH-004
```

Statut : ✅ Validé et consolidé

## Lot 3 — Production et circulation

```text
ENGINE-013
→ production réelle
→ 201 / 201

ENGINE-014
→ transfert volontaire entre habitants
→ 224 / 224
```

Capacité de référence :

```text
A produit
↓
A donne à B
↓
B consomme
```

TECH : `TECH-005`.

Statut : ✅ Validé et consolidé

## Lot 4 — Cognition autonome générique

```text
ENGINE-015
→ observation d'exécution
→ 233 / 233

ENGINE-016
→ Habitudes génériques
→ 260 / 260

ENGINE-017
→ Ambitions génériques
→ 291 / 291
```

TECH : `TECH-006`.

Statut : ✅ Validé et consolidé

---

# Ce que v0.4 sait désormais faire

```text
habitant autonome
↓
répondre à un besoin
ou
transférer une ressource
ou
produire
ou
agir selon une Habitude
ou
poursuivre une Ambition
↓
Intent
↓
Action Pipeline
↓
World
```

Le World conserve également l'état matériel et cognitif minimal nécessaire : stocks, provenance, Habitudes et Ambitions.

---

# Ce que v0.4 ne sait pas encore faire complètement

- personnalité générique opérationnelle ;
- mapping Trait/Habitude ;
- mapping Trait/Ambition ;
- Habitudes narratives canoniques ;
- Types d'Ambitions canoniques ;
- économie commerciale : monnaie, prix, vente, marché ;
- professions/carrières complètes ;
- Mémoire du Monde opérationnelle ;
- événements mondiaux autonomes complets ;
- interactions sociales autonomes suffisamment riches ;
- crédibilité multi-générations démontrée de bout en bout.

---

# Prochaine frontière immédiate

Le bloc cognitif possède Habitudes et Ambitions, tandis que GDB-004D définit déjà un modèle générique de Personnalité suffisamment précis pour être audité côté ENGINE.

Prochaine opération recommandée :

```text
AUDIT GDB-004D
↓
contrat ENGINE Personality
↓
PersonalityComponent
+
évolution des Traits
+
frontières de modulation explicites
```

Aucun mapping Trait/Habitude ou Trait/Ambition ne devra être inventé sans règle concrète.

---

# Frontière économique parallèle

Le substrat matériel existe, mais l'économie commerciale reste bloquée tant que GDB-019 ne définit pas suffisamment :

```text
prix
monnaie
marchés
échanges commerciaux
formules déterministes applicables
```

ENGINE ne doit pas inventer ces mécanismes.

---

# Critère de sortie v0.4

Le monde évolue de façon crédible pendant plusieurs générations sans intervention permanente du joueur.

À `291 / 291`, Chroniques possède désormais :

```text
autonomie physiologique
+
substrat économique matériel
+
substrat cognitif générique
```

Ce résultat est majeur mais ne satisfait pas encore le critère multi-générations complet.

v0.4 reste ouverte.

---

# v0.5 — La profondeur

Après v0.4, approfondissements possibles selon autorités :

- économie avancée ;
- métiers ;
- médecine ;
- justice ;
- crime ;
- politique ;
- religion ;
- combat ;
- patrimoine avancé.

Critère : des parcours radicalement différents produisent des histoires profondément différentes.

---

# v0.6 — Les outils

- éditeur de contenu ;
- debugger de simulation ;
- inspection du World ;
- diagnostics déterministes ;
- outils de production.

---

# v1.0 — Première alpha

- boucle complète ;
- sauvegarde versionnée ;
- équilibrage ;
- interface aboutie ;
- direction artistique ;
- stabilité ;
- diagnostics suffisants.

---

# Workflow

```text
GDB / ACT
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
point de consolidation significatif
↓
TECH / AUDIT / catalogues / roadmap / README concernés
```

---

# Historique

## Version 2.7

- ENGINE-013 à ENGINE-017 enregistrés comme bloc consolidé ;
- production et circulation autonomes documentées par TECH-005 ;
- observation, Habitudes et Ambitions documentées par TECH-006 ;
- validation globale portée à 291 / 291 ;
- audit de jalon autonomie productive et cognitive créé ;
- prochaine frontière immédiate fixée à l'audit de la Personnalité générique ;
- économie commerciale et critère multi-générations maintenus ouverts.

## Version 2.6

- ENGINE-011/012 consolidées à 178 / 178 ;
- TECH-004 créé ;
- autonomie par besoins validée ;
- frontière suivante orientée vers production/économie.

## Version 2.5

- ENGINE-010 validée à 146 / 146 ; TECH-003 créé.

## Version 2.4

- ENGINE-009 validée à 134 / 134 ; TECH-002 créé.

## Version 2.3

- ENGINE-008 validée ; cible v0.3 clarifiée.

## Version 2.2

- introduction de la bibliothèque ENGINE et du workflow Documentation → Code → Tests → TECH.

## Version 2.1

- ordre des phases aligné sur MASTER-005.

## Version 2.0

- remplacement de la V1 et intégration des décisions architecturales initiales.
