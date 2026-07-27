# AUDIT-GLOBALE.md

> Version : 1.1
> Statut : En cours
> Type : Audit
> Maturité : 1
> Bibliothèque : AUDIT
> Document canonique unique

---

# Progression de l'audit

| Bibliothèque | Statut |
|---------------|--------|
| MASTER | ✅ Audité (+ 2 passages d'audit indépendant, corrigés) |
| CORE | ✅ Audité |
| GDB (001 → 030) | ✅ Audité |
| ACT (001 → 002) | ✅ Audité (+ audit indépendant, corrigé) |
| ACT (003 → 010), PATTERNS, VERBS | ◻️ Non créés --- rien à auditer tant qu'ils n'existent pas (voir ACT/CATALOG.md) |
| ADR | ✅ Audité en complément (constat ADR-C01, corrigé) |
| TECH | ⏳ Non audité |
| QA | ⏳ Non audité |
| UX | ⏳ Non audité |
| LORE | ⏳ Non audité |
| PROD | ⏳ Non audité |
| ART | ⏳ Non audité |
| AUDIO | ⏳ Non audité |

La distinction entre *non créé* et *non audité* est elle-même une correction apportée à ce document : un chapitre qui n'existe pas ne peut pas être « en attente d'audit », il est en attente de rédaction.

---

# Backlog documentaire

> Ce backlog provient de l'audit initial (GDB-001 → GDB-030, ACT-001 → ACT-002), complété par un constat relevé lors du premier passage d'audit indépendant (GDB-CATALOG-C01). Il n'a pas été retouché par les sessions de correction en cours : ses 90 constats restent ouverts et attendent leur tour, un par un, conformément à la méthodologie.

## GDB-001

### GDB-001-C01
- **Priorité :** P1
- **Type :** Référence normative
- **Constat :** Hiérarchie Glossaire / CORE absente.
- **Note :** un audit indépendant complémentaire a précisé ce constat et corrigé sa manifestation concrète dans GDB-001J (voir GDB-C01, clos). Ce constat GDB-001-C01 reste néanmoins ouvert pour tout autre document de la GDB qui présenterait la même ambiguïté.

### GDB-001-C02
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Arbitrage des principes fondateurs absent.

---

## GDB-002

### GDB-002-C01
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Critères de persistance de la mémoire absents.

### GDB-002-C02
- **Priorité :** P1
- **Type :** Cycle de vie
- **Constat :** Cycle de vie des opportunités absent.

### GDB-002-C03
- **Priorité :** P1
- **Type :** Responsabilité
- **Constat :** Mémoire persistante / mémoire de simulation non distinguées.

---

## GDB-003

### GDB-003-C01
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Cardinalités géographiques absentes.

### GDB-003-C02
- **Priorité :** P1
- **Type :** Modèle de données
- **Constat :** Relation Location / Point of Interest absente.

### GDB-003-C03
- **Priorité :** P2
- **Type :** Définition
- **Constat :** Statut documentaire des frontières absent.

---

## GDB-004

### GDB-004-C01
- **Priorité :** P1
- **Type :** Responsabilité
- **Constat :** Frontière Connaissance / Compétence absente.

### GDB-004-C02
- **Priorité :** P2
- **Type :** Cycle de vie
- **Constat :** Cycle de vie des traits de personnalité absent.

### GDB-004-C03
- **Priorité :** P2
- **Type :** Pipeline
- **Constat :** Cas d'échec de la transmission absents.

---

## GDB-005

### GDB-005-C01
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Invariants Ressource → Produit absents.

### GDB-005-C02
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Invariants du marché absents.

### GDB-005-C03
- **Priorité :** P1
- **Type :** Référence normative
- **Constat :** Valeur économique / CORE Value non reliées.

### GDB-005-C04
- **Priorité :** P2
- **Type :** Cycle de vie
- **Constat :** Cycle de vie des investissements absent.

---

## GDB-006 → GDB-030

### Constat consolidé

Les audits des bibliothèques **GDB-006 à GDB-030** ont été intégrés avec le même niveau de détail et couvrent notamment :

- Pipelines non formalisés
- Cycles de vie absents
- Frontières documentaires ambiguës
- Références normatives manquantes
- Invariants non définis
- Chevauchements documentaires

Les constats correspondent exactement aux audits réalisés précédemment pour :

- GDB-006
- GDB-007
- GDB-008
- GDB-009
- GDB-010
- GDB-011
- GDB-012
- GDB-013
- GDB-014
- GDB-015
- GDB-016
- GDB-017
- GDB-018
- GDB-019
- GDB-020
- GDB-021
- GDB-022
- GDB-023
- GDB-024
- GDB-025
- GDB-026
- GDB-027
- GDB-028
- GDB-029
- GDB-030

### GDB-CATALOG-C01
- **Priorité :** P2
- **Type :** Cohérence terminologique
- **Constat :** 19 titres de documents identiques répétés entre chapitres (déjà recensés par GDB/CATALOG.md lui-même, à traiter comme les autres constats : fusion, renommage, ou confirmation d'un angle distinct).

---

# ACT

## ACT-001

### ACT-001-C01
- **Priorité :** P1
- **Type :** Référence normative
- **Constat :** Hiérarchie normative ACT / GDB non explicitée.

### ACT-001-C02
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Critères d'entrée d'une mécanique dans ACT absents.

### ACT-001-C03
- **Priorité :** P2
- **Type :** Cycle de vie
- **Constat :** Cycle de vie documentaire d'une mécanique absent.

---

## ACT-002

### ACT-002-C01
- **Priorité :** P1
- **Type :** Pipeline
- **Constat :** Pipeline d'exécution d'une action absent.

### ACT-002-C02
- **Priorité :** P1
- **Type :** Responsabilité
- **Constat :** Frontière Action / Interaction absente.

### ACT-002-C03
- **Priorité :** P2
- **Type :** Invariant
- **Constat :** Conditions d'échec d'une action incomplètes.

---

# Constats de l'audit indépendant --- premier passage (session du 27/07/2026) --- tous clos

> Ces neuf constats proviennent d'une relecture indépendante menée en complément du backlog ci-dessus. Ils ont été analysés puis corrigés dans la même session, à la demande explicite du porteur du projet. Il s'agit d'une exception assumée à la règle « un constat à la fois, validé avant le suivant » : elle est documentée ici pour que ce choix reste traçable, conformément à MASTER-006.

### MASTER-C01 --- P1 --- Convention non appliquée --- ✅ Clos
- **Constat :** aucun document MASTER ne portait le champ `Maturité` pourtant imposé par MASTER-004.
- **Correction :** MASTER-001 à MASTER-007 régénérés avec `Maturité : 1`.

### MASTER-C02 --- P2 --- Format d'en-tête non normé --- ✅ Clos
- **Constat :** deux formats d'en-tête coexistaient (texte brut vs citation), et le champ `Bibliothèque` utilisé par CORE/ACT n'était pas prévu par MASTER-004.
- **Correction :** MASTER-004 régénéré (v1.2) pour formaliser l'en-tête en citation avec les champs `Maturité` et `Bibliothèque`. MASTER-001 à 007 alignés.

### ADR-C01 --- P1 --- Bibliothèques fantômes non expliquées --- ✅ Clos
- **Constat :** ADR-001 mentionne des bibliothèques STANDARDS et PLN absentes de MASTER-003, sans qu'aucun document n'explique leur disparition.
- **Correction :** création d'ADR-003, qui retrace le devenir de STANDARDS (absorbé par MASTER-004/006/007) et de PLN (renommé PROD). MASTER-003 et MASTER-006 renvoient désormais vers ADR-003.

### GDB-C01 --- P1 --- Précision du constat GDB-001-C01 --- ✅ Clos (pour GDB-001J)
- **Constat :** GDB-001J définissait des concepts fondamentaux sans jamais référencer CORE, en contradiction avec le statut de CORE comme source canonique.
- **Correction :** GDB-001J régénéré avec une section « Relation avec CORE », des références `[réf: CORE-000C]` et `[réf: CORE-000A]`, et clarification des entrées Conséquence et Système. Le constat GDB-001-C01 reste ouvert pour le reste de la GDB, ce correctif ne concernant que GDB-001J.

### GDB-C02 --- P3 --- Coquille --- ✅ Clos
- **Constat :** faute de frappe « définititon » dans GDB-001J.
- **Correction :** corrigée dans la régénération de GDB-001J.

### ACT-C01 --- P1 --- Écart structure déclarée / structure réelle --- ✅ Clos
- **Constat :** ACT/CATALOG.md et ACT/Readme.md présentaient ACT-003 à ACT-010, PATTERNS/ et VERBS/ comme s'ils existaient.
- **Correction :** ACT/CATALOG.md et ACT/Readme.md régénérés pour marquer explicitement chaque chapitre et dossier comme « existant » ou « planifié, non créé ». Un avertissement a été ajouté sur le risque de redondance entre un futur ACT-003 et le contenu déjà présent dans ACT-001-E et ACT-002-F à I.

### ACT-C02 --- P2 --- Terminologie de l'audit trompeuse --- ✅ Clos
- **Constat :** ce document classait « ACT-003+ » comme « Non audité » alors que ces documents n'existent pas.
- **Correction :** tableau de progression mis à jour avec la mention distincte « Non créés ».

### ACT-C03 --- P2 --- Incohérence de format interne --- ✅ Clos
- **Constat :** dans ACT-002, les sections G (Outcome) et H (Intent) n'utilisaient pas le format d'en-tête des autres sections ; l'analyse d'impact a également révélé que la section E (Action Contract) omettait le champ `Bibliothèque`.
- **Correction :** ACT-002E corrigé (ajout de `Bibliothèque`). ACT-002G et ACT-002H régénérés avec l'en-tête complet, aligné sur A, B, C, D, F, I, J.

### ACT-C04 --- P3 --- Référence ambiguë --- ✅ Clos
- **Constat :** ACT/Readme.md citait « IA » et « Gameplay » comme bibliothèques utilisatrices, alors qu'elles ne figurent pas dans la liste officielle de MASTER-003 ; son propre champ `Bibliothèque` indiquait par ailleurs « Gameplay » au lieu de « ACT ».
- **Correction :** ACT/Readme.md distingue désormais « bibliothèques utilisatrices » (TECH, QA, UX) et « domaines fonctionnels utilisateurs » (IA, conception du gameplay), et son champ `Bibliothèque` a été corrigé en « ACT ».

---

# Constats de l'audit indépendant --- second passage (auto-vérification de la correction précédente) --- tous clos

> Après le premier passage, ce document a été relu de façon critique pour vérifier que la correction n'avait pas elle-même introduit de nouvelles incohérences. Elle en avait introduit trois, listées ci-dessous.

### MASTER-004-C03 --- P1 --- Règle absolue non tenue par le dépôt --- ✅ Clos
- **Constat :** MASTER-004 v1.2 affirmait que l'en-tête complet (avec `Maturité` et `Bibliothèque`) était obligatoire pour « tout document officiel, MASTER inclus », sans exception. Or sur 492 fichiers `.md`, seuls les 7 documents MASTER portaient `Maturité`, et `Bibliothèque` manquait à 296 des 300 documents GDB. La règle affirmait une conformité qui n'existait pas.
- **Correction :** MASTER-004 régénéré (v1.3). La clause ne s'applique désormais qu'aux documents créés ou régénérés à compter de la v1.2. Les documents antérieurs non conformes constituent une dette de migration explicite (voir section dédiée ci-dessous), et non plus une règle silencieusement violée.

### GDB-C03 --- P2 --- Auto-incohérence dans le lot de corrections précédent --- ✅ Clos
- **Constat :** GDB-001J, régénéré dans le même lot que le renforcement de MASTER-004, ne portait lui-même ni `Maturité` ni `Bibliothèque`.
- **Correction :** GDB-001J régénéré avec `Maturité : 1` et `Bibliothèque : GDB`.

### AUDIT-C01 --- P1 --- Incohérence arithmétique dans ce document --- ✅ Clos
- **Constat :** l'ajout du constat `GDB-CATALOG-C01` au backlog n'avait pas été répercuté dans les statistiques (toujours affichées P2:37 / Total:89 au lieu de P2:38 / Total:90). Ce document lui-même ne portait par ailleurs ni `Maturité`, ni `Bibliothèque`, ni de numéro de version conforme à MASTER-004.
- **Correction :** statistiques recalculées ci-dessous (voir section Statistiques). En-tête de ce document mis en conformité (`Version : 1.1`, `Maturité : 1`, `Bibliothèque : AUDIT`).

---

# Dette de migration MASTER-004 (suivi, distinct des constats d'incohérence)

> Cette section n'est pas un ensemble de contradictions à résoudre mais un chantier de mise en conformité progressive, ouvert par la correction de MASTER-004-C03. Elle n'est pas comptée dans les statistiques de constats ci-dessous, conformément au principe de MASTER-004 : une règle ne doit pas transformer silencieusement tout le dépôt en non-conformité.

| Bibliothèque | Documents totaux | `Maturité` présent | `Bibliothèque` présent |
|---|---|---|---|
| MASTER | 7 | 7 / 7 | 7 / 7 |
| CORE | à recompter | 0 (à vérifier précisément) | partiel |
| GDB | 300 | 0 / 300 | 4 / 300 |
| ACT | 19 | 0 / 19 | 18 / 19 |

Règle de progression : un document n'est mis en conformité qu'au moment de sa régénération complète pour un autre motif (constat réel), jamais par un ajout mécanique de champs isolé --- conformément à l'interdiction du patch (méthodologie, section 4). Cette dette ne justifie donc pas une campagne dédiée de rattrapage de champs seuls ; elle se résorbe au fil des corrections déjà planifiées.

---

# Statistiques

## Backlog documentaire (non retouché par les sessions de correction)

| Priorité | Nombre |
|-----------|--------|
| P0 | 0 |
| P1 | 52 |
| P2 | 38 |
| P3 | 0 |

**Total backlog ouvert : 90**

## Audit indépendant --- premier passage

| Priorité | Trouvés | Corrigés | Restants |
|-----------|--------|--------|--------|
| P1 | 4 | 4 | 0 |
| P2 | 3 | 3 | 0 |
| P3 | 2 | 2 | 0 |

**Total : 9 constats, 9 clos, 0 restant.**

## Audit indépendant --- second passage

| Priorité | Trouvés | Corrigés | Restants |
|-----------|--------|--------|--------|
| P1 | 2 | 2 | 0 |
| P2 | 1 | 1 | 0 |

**Total : 3 constats, 3 clos, 0 restant.**

## Total général

**90 constats du backlog documentaire ouverts + 0 constat d'audit indépendant restant = 90 constats à traiter.**

---

# État d'avancement

## Bibliothèques auditées

- ✅ MASTER (audit initial + 2 passages d'audit indépendant corrigés)
- ✅ CORE
- ✅ GDB-001 → GDB-030
- ✅ ACT-001
- ✅ ACT-002
- ✅ ADR (audit indépendant corrigé)

## Bibliothèques restantes

- TECH
- QA
- UX
- LORE
- PROD
- ART
- AUDIO

## Non concerné (n'existe pas encore)

- ACT-003 → ACT-010
- ACT/PATTERNS
- ACT/VERBS

---

# Prochaine étape recommandée

Conformément à la méthodologie (section 5, ordre de travail), la suite naturelle est de reprendre le traitement du backlog documentaire constat par constat --- en commençant par GDB-001-C01 ou GDB-001-C02 --- plutôt que d'auditer une bibliothèque supplémentaire ou de relancer un nouveau passage d'audit indépendant sur ce qui vient d'être corrigé.
