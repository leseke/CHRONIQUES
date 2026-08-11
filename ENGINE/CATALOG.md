# ENGINE — Catalogue

> Version : 1.15
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (`CHRONIQUES-ENGINE`), TECH, QA

---

# Objectif

Ce catalogue est la source canonique pour la bibliothèque ENGINE.

ENGINE décrit l'architecture fonctionnelle et technique attendue du moteur. Les règles métier restent définies dans leurs bibliothèques d'autorité, notamment CORE, GDB et ACT.

---

# Documents existants

```text
ENGINE-000  Principes d'architecture                  Stable
ENGINE-001  Journal d'événements du World            Stable
ENGINE-002  Kernel                                   Stable
ENGINE-003  Scheduler et boucle de simulation        Stable
ENGINE-004  Systems de simulation                    Stable
ENGINE-005  Persistence et Serialization             Stable
ENGINE-006  Action Pipeline                          Validée / M4
ENGINE-007  Resource Manager                         Réservé / non créé
ENGINE-008  Systems de population                    Validée / M4
ENGINE-009  Boucle de vie minimale                   Validée / M4
ENGINE-010  Orchestration habitants autonomes        Validée / M4
ENGINE-011  Décision autonome par besoins            Validée / M4
ENGINE-012  Alimentation autonome minimale           Validée / M4
ENGINE-013  Production autonome minimale             Validée / M4
```

---

# ENGINE-006 — Action Pipeline

Validation acquise.

```text
Intent
↓
Planner
↓
Plan
↓
Action Instance
↓
Execution Engine
↓
Outcome
↓
Effects
↓
World
```

---

# ENGINE-010 à ENGINE-012 — Bloc autonomie par besoins consolidé

Le bloc déjà consolidé permet :

```text
Scheduler
↓
AutonomousActionSystem
↓
Intent autonome
↓
Repos ou Alimentation
↓
World
```

Validation de référence du point de consolidation :

```text
178 / 178 tests réussis
```

Ce bloc est documenté par TECH-003 et TECH-004.

---

# ENGINE-013 — Production autonome minimale

Statut : Validée.

Maturité : 4.

ENGINE-013 ouvre le premier socle productif réel de v0.4.

Autorités métier :

```text
GDB-004A v1.1
GDB-005C v1.2
GDB-012B v1.1
GDB-012E v1.1
```

Autorités ACT validées :

```text
Transformation
↓
PAT-003 Production
↓
VERB-003 Produire une denrée
```

Flux validé :

```text
NeedsIntentSource
↓ si aucun entretien exécutable
ProductiveActivityIntentSource
↓
Intent produire_denree
↓
ProductionPlanner
↓
entrée ResourceStock
+
sortie FoodProduct
↓
ProductionExecutionEngine
↓
ProductionActionEffectApplicator
↓
stock entrée ↓
portions sortie ↑
provenance persistante
```

ENGINE-013 introduit notamment :

- `ResourceStockComponent` ;
- `ProductionOperation` ;
- `ProductionProvenanceComponent` ;
- `IProductiveActivityResolver` ;
- `ProductiveActivityIntentSource` ;
- `CompositeAutonomousIntentSource` ;
- `ProduireDenreeDefinition` ;
- `ProductionPlanner` ;
- `CompositePlanner` ;
- `ProductionExecutionEngine` ;
- `CompositeExecutionEngine` ;
- `ProductionActionEffectApplicator` ;
- persistance des stocks et de la provenance.

Le `PipelineRunner` n'est pas spécialisé pour VERB-003 : la nouvelle capacité entre par les interfaces déjà présentes.

---

# Scénario d'intégration validé

```text
Tick N
Acteur affamé
+
aucune nourriture disponible
+
opération productive exécutable
↓
produire_denree
↓
une portion alimentaire apparaît par transformation réelle

Tick N+1
↓
manger
↓
portion consommée
+
Faim restaurée
```

Ce scénario fonctionne sans entrée joueur.

---

# Validation technique

Le fichier ENGINE-013 contient **23 nouveaux tests**.

Base validée avant ce lot :

```text
178 / 178
```

Validation locale communiquée le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 201 / 201 tests réussis
→ 0 échec
```

Le précédent total attendu de 200 provenait d'un comptage erroné de 22 nouveaux tests ; le fichier `Engine013ProductionTests.cs` contient bien 23 `[Fact]`.

---

# Frontière avec l'économie commerciale

ENGINE-013 ne simule pas encore :

- monnaie ;
- prix ;
- salaire ;
- vente ;
- marché ;
- offre et demande ;
- entreprise.

GDB-019 reste l'autorité sur ces mécanismes, mais ses documents actuels demeurent trop principiels pour justifier une formule de marché dans le moteur.

Le socle productif peut donc progresser indépendamment sans inventer ces règles.

---

# ENGINE-007 — Resource Manager

ENGINE-007 reste réservé aux ressources **techniques** du moteur. Il ne désigne pas les ressources économiques de GDB-005 et ne doit pas être réutilisé pour ENGINE-013.

---

# Convention de nommage

Le catalogue canonique unique est :

```text
ENGINE/CATALOG.md
```

---

# Historique

## Version 1.15

- ENGINE-013 passe à **Validée / Maturité 4** ;
- PAT-003 / VERB-003 confirmés comme autorités ACT validées ;
- suite globale portée à **201 / 201 tests réussis** ;
- correction du comptage ENGINE-013 : 23 nouveaux tests, et non 22 ;
- scénario autonome production au Tick N → alimentation au Tick N+1 confirmé ;
- stocks et provenance persistante validés ;
- économie commerciale maintenue hors périmètre ;
- aucune consolidation TECH/roadmap/README déclenchée automatiquement.

## Version 1.14

- création d'ENGINE-013 — Production autonome minimale en Proposition / Maturité 2 ;
- ouverture de PAT-003 / VERB-003 dans le chemin ENGINE ;
- ajout du stock matériel et de la provenance minimale ;
- composition ordonnée entretien → production ;
- composition des Planners et Execution Engines ;
- scénario cible production au Tick N → alimentation au Tick N+1 ;
- couverture QA ajoutée ;
- économie commerciale explicitement laissée hors périmètre.

## Version 1.13

- ENGINE-012 validée / Maturité 4 ;
- suite portée à 178 / 178.

## Version 1.12

- création d'ENGINE-012.

## Versions 1.9 à 1.11

- création, validation et renforcement multi-Tick d'ENGINE-011.

## Version 1.8

- ENGINE-010 validée ; 146 / 146 ; ENGINE-C06 résolue.

## Versions 1.0 à 1.7

- création et consolidation des fondations ENGINE jusqu'à ENGINE-010.
