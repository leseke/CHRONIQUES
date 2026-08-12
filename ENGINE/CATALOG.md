# ENGINE — Catalogue

> Version : 1.29
> Statut : Foundation
> Maturité : 1
> Bibliothèque : ENGINE
> Dépendances : MASTER, CORE, GDB, ACT
> Utilisée par : Implémentation (`CHRONIQUES-ENGINE`), TECH, QA

---

# Objectif

Ce catalogue est la source canonique de la bibliothèque ENGINE.

ENGINE décrit l'architecture attendue du moteur. Les règles métier restent définies dans leurs autorités amont.

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
ENGINE-014  Circulation autonome minimale            Validée / M4
ENGINE-015  Observation de l'exécution autonome      Validée / M4
ENGINE-016  Habitudes génériques minimales           Validée / M4
ENGINE-017  Ambitions génériques minimales           Validée / M4
ENGINE-018  Personnalité générique minimale          Validée / M4
ENGINE-019  Mémoire du Monde minimale                Proposition / M2
```

---

# Validation courante

Base localement validée avant ENGINE-019 :

```text
dotnet build
→ succès

dotnet test
→ 330 / 330 tests réussis
→ 0 échec
```

---

# Chaîne autonome consolidée

GDB-004A v1.3 fait autorité sur l'ordre courant :

```text
besoins physiologiques actionnables
↓
transfert volontaire exécutable
↓
activité productive exécutable
↓
Habitudes actives
↓
Ambitions candidates
↓
aucun Intent
```

La Personnalité n'est pas une famille d'Intent. Elle reste en amont de cette chaîne conformément à GDB-004D.

---

# Bloc économique matériel validé

```text
ENGINE-013 — Production autonome minimale
→ 201 / 201 à validation

ENGINE-014 — Circulation autonome minimale
→ 224 / 224 à validation

TECH-005 — Production et circulation autonomes
```

---

# Bloc cognitif générique validé

```text
ENGINE-015 — Observation de l'exécution autonome
→ 233 / 233 à validation

ENGINE-016 — Habitudes génériques minimales
→ 260 / 260 à validation

ENGINE-017 — Ambitions génériques minimales
→ 291 / 291 à validation

ENGINE-018 — Personnalité générique minimale
→ 330 / 330 à validation
```

`ENGINE-018` ajoute Traits, Poids de référence, stabilisation, Inflexions et causalité persistante sans mapping cognitif concret.

---

# ENGINE-019 — Mémoire du Monde minimale

Statut : Proposition / Maturité 2.

Spécification : `ENGINE-019 v1.1`.

Autorité principale :

```text
GDB-002B v1.3
```

Audit préalable :

```text
AUDIT/AUDIT-MEMOIRE-DU-MONDE-Implementabilite.md
→ Clos / M4
```

Briques candidates :

```text
WorldMemoryComponent
WorldMemoryTier
WorldMemoryTransitionTrace
WorldMemoryCreationCandidate
WorldMemoryGenerationEvidence
IWorldMemoryRule
IWorldMemoryGenerationResolver
WorldMemoryEvolutionSystem
```

Architecture candidate :

```text
fait qualifié par une règle concrète
↓
Entity + WorldMemoryComponent
↓
Anecdote
↓
preuves générationnelles injectées
↓
Souvenir / Légende / Tradition / oublié
```

Invariants :

- `World` reste sans donnée métier de mémoire ;
- aucun Event n'est mémorisé automatiquement ;
- aucun score universel de significativité ;
- toute mémoire possède Type + Key + sources stables ;
- tout nouvel élément commence Anecdote active ;
- aucun saut de palier ;
- une transition maximum par génération ;
- générations sautées rejouées une par une ;
- règle absente : mémoire persistée mais non évoluée ;
- oubli conservé comme trace technique inactive ;
- aucune durée `N Ticks = génération` inventée ;
- aucun Type concret de mémoire fourni par défaut.

Persistance candidate :

```text
EntitySnapshot.WorldMemory
WorldRepository
```

---

# Couverture QA ENGINE-019

```text
Engine019WorldMemoryTests.cs
→ 24 tests

Engine019WorldMemoryInvariantTests.cs
→ 16 tests
```

Nouveaux tests : **40**.

Base :

```text
330 / 330
```

Total attendu avant validation locale :

```text
370 / 370
```

Aucun passage M4 ne sera enregistré avant confirmation locale.

---

# Persistance étendue

Le World persiste maintenant ou, pour ENGINE-019, candidate à persister :

```text
FoodProductComponent
ResourceStockComponent
ProductionProvenanceComponent
HabitComponent
AmbitionComponent
PersonalityComponent
WorldMemoryComponent
```

Les resolvers, rules, policies et registres runtime restent hors sauvegarde.

---

# ACT concret validé

```text
Entretien → PAT-001 Repos → VERB-001 Se reposer
Entretien → PAT-002 Alimentation → VERB-002 Manger
Transformation → PAT-003 Production → VERB-003 Produire une denrée
Échange → PAT-004 Transfert → VERB-004 Donner une denrée
```

ENGINE-015 à 019 n'ajoutent aucun Pattern ou Verbe.

---

# Frontières restantes

Ne sont toujours pas autorisés ou implémentés comme capacités validées :

- Type concret de Mémoire du Monde ;
- génération universelle intégrée ;
- événements mondiaux autonomes complets ;
- catalogue concret de Traits ;
- mapping Trait/Habitude ;
- mapping Trait/Ambition ;
- états émotionnels ;
- score psychologique global ;
- Habitudes narratives concrètes ;
- Types d'Ambitions concrets ;
- prix, monnaie, vente et marché ;
- fairness inter-familles ;
- autonomie crédible sur plusieurs générations achevée.

ENGINE-007 reste réservé au Resource Manager technique et demeure non créé.

---

# Historique

## Version 1.29

- audit d'implémentabilité de GDB-002B/C/D réalisé ;
- GDB-002B porté à v1.3 pour rendre significativité, preuves, générations et transitions déterministes ;
- création et enregistrement d'ENGINE-019 en Proposition / M2 ;
- framework générique de Mémoire du Monde implémenté en candidate ;
- persistance `WorldMemoryComponent` ajoutée ;
- 40 tests candidats ajoutés ;
- total attendu fixé à **370 / 370** ;
- aucun Type concret de mémoire ni durée arbitraire de génération introduits.

## Version 1.28

- ENGINE-018 passe à Validée / Maturité 4 ;
- suite globale portée à 330 / 330 tests réussis ;
- 39 tests ENGINE-018 validés.

## Version 1.27

- création et enregistrement d'ENGINE-018 en Proposition / M2.

## Version 1.26

- consolidation documentaire du jalon ENGINE-013 à ENGINE-017 ;
- enregistrement de TECH-005 et TECH-006 ;
- audit de jalon autonomie productive et cognitive ajouté ;
- validation courante confirmée à 291 / 291.

## Version 1.25

- ENGINE-017 validée / M4 à 291 / 291.

## Versions 1.20 à 1.24

- construction et validation progressive de l'observation autonome, des Habitudes et des Ambitions génériques.

## Versions 1.0 à 1.19

- construction progressive des fondations et de l'autonomie jusqu'à la circulation économique minimale.

---

Fin du document
