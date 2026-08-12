# ENGINE — Catalogue

> Version : 1.26
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
```

---

# Validation courante

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

Le moteur possède désormais les briques correspondant à chacune de ces familles sans score universel inter-familles.

---

# Bloc économique matériel

## ENGINE-013 — Production autonome minimale

```text
ressource réelle
↓
ProductionOperation
↓
produire_denree
↓
stock alimentaire
+
provenance
```

Validation initiale : `201 / 201`.

## ENGINE-014 — Circulation autonome minimale

```text
stock A
↓
donner_denree
↓
stock B
↓
manger
```

Validation initiale : `224 / 224`.

Documentation TECH consolidée :

```text
TECH-005 — Production et circulation autonomes
```

---

# Bloc cognitif générique

## ENGINE-015 — Observation de l'exécution autonome

```text
Intent
↓
BeforeExecution
↓
Action / Outcome
↓
AfterExecution ou ExecutionAborted
```

Validation initiale : `233 / 233`.

## ENGINE-016 — Habitudes génériques minimales

Le moteur sait former, persister, sélectionner, activer, renforcer et éroder des Habitudes à partir de règles injectées, sans Habitude métier canonique.

Validation initiale : `260 / 260`.

## ENGINE-017 — Ambitions génériques minimales

Le moteur sait créer, persister, évaluer, accomplir/abandonner et sélectionner des Ambitions à partir de Types injectés, sans Type métier canonique.

Validation initiale : `291 / 291`.

Documentation TECH consolidée :

```text
TECH-006 — Cognition autonome générique
```

---

# Persistance étendue

Le World persiste maintenant notamment :

```text
FoodProductComponent
ResourceStockComponent
ProductionProvenanceComponent
HabitComponent
AmbitionComponent
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

ENGINE-015/016/017 n'ajoutent aucun Pattern ou Verbe : Habitudes et Ambitions produisent des Intents dirigés vers les Actions déjà traitables.

---

# Point de consolidation

Le jalon ENGINE-013 à ENGINE-017 est consolidé par :

```text
TECH-005
TECH-006
AUDIT/AUDIT-MONDE-VIVANT-AUTONOMIE-Consolidation.md
```

Le contrôle confirme la concordance GDB → ACT → ENGINE → code → tests → TECH.

---

# Frontières restantes

Ne sont pas encore implémentés comme capacités génériques validées :

- `PersonalityComponent` et évolution des Traits ;
- mappings Trait/Habitude et Trait/Ambition ;
- Habitudes narratives concrètes ;
- Types d'Ambitions concrets ;
- prix, monnaie, vente et marché ;
- Mémoire du Monde opérationnelle ;
- événements mondiaux autonomes complets ;
- fairness inter-familles ;
- autonomie crédible sur plusieurs générations achevée.

ENGINE-007 reste réservé au Resource Manager technique et demeure non créé.

---

# Historique

## Version 1.26

- consolidation documentaire du jalon ENGINE-013 à ENGINE-017 ;
- enregistrement de TECH-005 et TECH-006 ;
- audit de jalon autonomie productive et cognitive ajouté ;
- validation courante confirmée à 291 / 291 ;
- prochaine frontière cognitive identifiée : personnalité générique, après audit de GDB-004D.

## Version 1.25

- ENGINE-017 validée / M4 à 291 / 291 ;
- Habitudes + Ambitions génériques présentes dans le moteur.

## Version 1.24

- ENGINE-017 ouverte en Proposition / M2.

## Version 1.23

- ENGINE-016 validée / M4 à 260 / 260.

## Version 1.22

- ENGINE-016 ouverte.

## Version 1.21

- ENGINE-015 validée / M4 à 233 / 233.

## Version 1.20

- ENGINE-015 ouverte.

## Versions 1.0 à 1.19

- construction progressive des fondations et de l'autonomie jusqu'à la circulation économique minimale.

---

Fin du document
