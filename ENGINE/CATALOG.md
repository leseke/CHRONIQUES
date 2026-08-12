# ENGINE — Catalogue

> Version : 1.27
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
ENGINE-018  Personnalité générique minimale          Proposition / M2
```

---

# Validation courante

Base localement validée avant ENGINE-018 :

```text
dotnet build
→ succès

dotnet test
→ 291 / 291 tests réussis
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

TECH-006 — Cognition autonome générique
```

---

# ENGINE-018 — Personnalité générique minimale

Statut : Proposition / Maturité 2.

Spécification : `ENGINE-018 v1.1`.

Autorité principale :

```text
GDB-004D v1.3
```

Briques candidates :

```text
PersonalityComponent
PersonalityTraitState
PersonalityInflexionTrace
PersonalityInflexionKind
PersonalityTraitCreationCandidate
PersonalityInflexion
IPersonalityTraitRule
IPersonalityStabilizationParameterResolver
PersonalityEvolutionSystem
```

Flux candidat :

```text
règle de Trait injectée
↓
formation déterministe
↓
Valeur + Poids de référence
↓
Inflexion identifiable ?
├── oui → déplacement + trace persistante
└── non → stabilisation vers la référence
```

Invariants :

- aucun Trait métier concret par défaut ;
- Valeur et Poids bornés `[0,100]` ;
- aucune duplication de Trait ;
- pas de stabilisation au Tick de création ;
- convergence sans dépassement ;
- cause obligatoire pour toute Inflexion ;
- même cause appliquée une seule fois au même Trait ;
- Inflexion légère : référence inchangée ;
- Inflexion profonde : nouvelle référence durable ;
- aucune lecture automatique de `World.Events` ;
- aucun mapping Trait/Habitude ou Trait/Ambition ;
- aucune source d'Intent ;
- aucun nouveau Pattern ou Verbe ACT.

Persistance candidate étendue :

```text
EntitySnapshot.Personality
WorldRepository
```

---

# Couverture QA ENGINE-018

```text
Engine018PersonalityTests.cs
→ 22 tests

Engine018PersonalityInvariantTests.cs
→ 17 tests
```

Nouveaux tests : **39**.

Base :

```text
291 / 291
```

Total attendu avant validation locale :

```text
330 / 330
```

Aucun passage M4 ne sera enregistré avant confirmation locale.

---

# Persistance étendue

Le World persiste maintenant ou, pour ENGINE-018, candidate à persister :

```text
FoodProductComponent
ResourceStockComponent
ProductionProvenanceComponent
HabitComponent
AmbitionComponent
PersonalityComponent
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

ENGINE-015 à 018 n'ajoutent aucun Pattern ou Verbe.

---

# Frontières restantes

Ne sont toujours pas autorisés par ENGINE-018 :

- catalogue concret de Traits ;
- mapping Trait/Habitude ;
- mapping Trait/Ambition ;
- états émotionnels ;
- score psychologique global ;
- Habitudes narratives concrètes ;
- Types d'Ambitions concrets ;
- prix, monnaie, vente et marché ;
- Mémoire du Monde opérationnelle ;
- fairness inter-familles ;
- autonomie crédible sur plusieurs générations achevée.

ENGINE-007 reste réservé au Resource Manager technique et demeure non créé.

---

# Historique

## Version 1.27

- création et enregistrement d'ENGINE-018 en Proposition / M2 ;
- framework générique de Personnalité implémenté en candidate ;
- Traits, stabilisation, Inflexions et causalité persistante couverts ;
- 39 tests ajoutés ;
- total attendu fixé à **330 / 330** ;
- aucun Trait concret, mapping cognitif ou nouveau Verbe introduit.

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
