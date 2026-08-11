# ENGINE-C06 — Clôture du constat d'orchestration Scheduler / Actions autonomes

> Version : 1.0
> Statut : Clos
> Type : Audit de concordance
> Maturité : 4
> Bibliothèque : AUDIT
> Constat source : ENGINE-C06
> Résolution : ENGINE-010

---

# 1. Objet

Clore formellement le constat `ENGINE-C06`, historiquement conservé dans `AUDIT-GLOBALE.md`.

Ce constat identifiait une lacune d'architecture : le moteur disposait d'un Scheduler et d'un Action Pipeline, mais aucun mécanisme ne permettait encore à des habitants autonomes d'initier des Actions pendant la simulation sans intervention du joueur.

---

# 2. Historique du constat

ENGINE-C06 avait été volontairement différé.

La décision était de ne pas anticiper une orchestration autonome tant que le projet n'était pas entré dans :

```text
MASTER-005
Phase 3 — Le monde vivant
```

Cette condition a été atteinte après validation de la boucle de vie minimale v0.3.

---

# 3. Réouverture

À l'ouverture de v0.4, le besoin a été réexaminé à partir de :

```text
MASTER-005
GDB-004A
GDB-004B
ACT-002-H
ACT-004-A
ENGINE-003
ENGINE-006
```

Le besoin réel identifié était limité à l'orchestration.

Aucune politique métier complète de décision n'était suffisamment définie pour justifier une IA générale.

---

# 4. Résolution

La résolution est portée par :

```text
ENGINE-010 — Orchestration des habitants autonomes
```

Architecture obtenue :

```text
Scheduler.Tick
↓
AutonomousActionSystem
↓
IAutonomousIntentSource
↓
Intent?
↓
IAutonomousIntentExecutor
↓
ENGINE-006
↓
World
```

---

# 5. Implémentation réelle

`CHRONIQUES-ENGINE` contient désormais :

```text
IAutonomousIntentSource
IAutonomousIntentExecutor
AutonomousActionSystem
```

Le System :

- traite uniquement des Acteurs explicitement enregistrés ;
- ignore les Entities absentes ;
- ignore les Entities mortes ;
- conserve un ordre déterministe ;
- demande au maximum un Intent par Acteur et par invocation ;
- rejette un Intent attribué à un autre Acteur ;
- ne connaît aucun Verbe concret ;
- ne fait jamais avancer le Tick lui-même ;
- délègue l'exécution à ENGINE-006.

---

# 6. Validation

Validation confirmée par le porteur du projet le 11 août 2026 :

```text
dotnet build
→ succès

dotnet test
→ 146 / 146 tests réussis
→ 0 échec
```

Le lot ENGINE-010 ajoute 12 tests.

Un test d'intégration démontre réellement :

```text
Scheduler
↓
Autonomie
↓
Intent
↓
PipelineRunner
↓
Action Archived
↓
Outcome réussi
↓
World modifié
```

---

# 7. Décision de clôture

Les conditions historiques de clôture sont désormais remplies :

```text
Phase 3 ouverte                ✅
Spécification ENGINE créée     ✅
Implémentation réalisée        ✅
Compilation réussie            ✅
Tests passants                 ✅
Intégration ENGINE-006 prouvée ✅
Validation du porteur          ✅
Documentation TECH             ✅ TECH-003
```

Décision :

```text
ENGINE-C06
→ CLOS
```

---

# 8. Limite de la clôture

Cette clôture résout exclusivement :

```text
lacune d'orchestration Scheduler / Actions autonomes
```

Elle ne signifie pas que sont terminés :

- la politique de décision des habitants ;
- la hiérarchisation des besoins ;
- les Habitudes ;
- les Ambitions ;
- la Mémoire du Monde ;
- l'économie autonome ;
- les métiers autonomes ;
- le catalogue complet de Verbes.

Ces sujets devront suivre leurs propres chaînes documentaires.

---

# 9. Relation avec AUDIT-GLOBALE.md

`AUDIT-GLOBALE.md` conserve l'historique du constat et de son ajournement.

Le présent document constitue l'enregistrement de clôture postérieur et fait autorité sur l'état courant d'ENGINE-C06.

Toute régénération future d'`AUDIT-GLOBALE.md` devra intégrer cette clôture et ne plus présenter ENGINE-C06 comme ouvert.

---

# 10. Traçabilité

```text
AUDIT-GLOBALE / ENGINE-C06
↓
MASTER-005 Phase 3
↓
ENGINE-010
↓
CHRONIQUES-ENGINE / Autonomy
↓
AutonomousActionSystemTests
↓
146 / 146
↓
TECH-003
↓
ENGINE-C06-Cloture
```

---

# Historique

## Version 1.0

- clôture formelle d'ENGINE-C06 ;
- validation ENGINE-010 enregistrée ;
- résultat global 146 / 146 enregistré ;
- distinction explicite entre orchestration autonome résolue et politique de décision encore future.
