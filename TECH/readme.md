# TECH

> Version : 1.5  
> Statut : Active  
> Type : Bibliothèque  
> Maturité : 2  
> Bibliothèque : TECH

---

## Rôle

Le dossier **TECH** documente les implémentations techniques réellement présentes et validées dans `CHRONIQUES-ENGINE`.

TECH décrit l'implémentation ; il ne crée jamais une règle métier.

Position documentaire :

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

Conformément à MASTER-006 v1.1, TECH est consolidé lorsqu'un jalon significatif est atteint et peut regrouper plusieurs lots ENGINE cohérents.

---

# Documents actuels

## TECH-001 — Systems de population

```text
ENGINE-008
→ relations + compétences + héritage minimal
→ validation initiale 122 / 122
```

Statut : Validé / M4.

## TECH-002 — Boucle de vie minimale

```text
ENGINE-009
→ LifeSession + mort + héritier + continuité
→ validation initiale 134 / 134
```

Statut : Validé / M4.

## TECH-003 — Orchestration des habitants autonomes

```text
ENGINE-010
→ IAutonomousIntentSource
→ IAutonomousIntentExecutor
→ AutonomousActionSystem
→ validation initiale 146 / 146
```

Statut : Validé / M4.

## TECH-004 — Décision autonome par besoins

```text
ENGINE-011 / ENGINE-012
→ repos + alimentation + arbitrage par besoins
→ validation de consolidation 178 / 178
```

Statut : Validé / M4.

## TECH-005 — Production et circulation autonomes

```text
ENGINE-013 / ENGINE-014
→ production réelle
→ provenance
→ transfert volontaire entre habitants
→ production → transfert → consommation
```

Repères de validation :

```text
ENGINE-013 → 201 / 201
ENGINE-014 → 224 / 224
suite au point de consolidation → 291 / 291
```

Statut : Validé / M4.

## TECH-006 — Cognition autonome générique

```text
ENGINE-015 / ENGINE-016 / ENGINE-017
→ observation Intent → Action → Outcome
→ Habitudes génériques
→ Ambitions génériques
```

Repères de validation :

```text
ENGINE-015 → 233 / 233
ENGINE-016 → 260 / 260
ENGINE-017 → 291 / 291
```

Statut : Validé / M4.

---

# État technique consolidé

La suite de référence au 12 août 2026 est :

```text
dotnet build
→ succès

dotnet test
→ 291 / 291 tests réussis
→ 0 échec
```

Le moteur relie désormais :

```text
besoins
↓
production
↓
circulation entre habitants
↓
consommation
+
observation d'exécution
↓
Habitudes
↓
Ambitions
```

Cette chaîne ne signifie pas que tous les comportements concrets sont définis : les frameworks Habitudes/Ambitions restent génériques et les règles concrètes doivent être autorisées en GDB avant spécialisation.

---

# Traçabilité courante

```text
GDB / ACT
↓
ENGINE-013 à ENGINE-017
↓
CHRONIQUES-ENGINE
↓
291 / 291
↓
TECH-005 / TECH-006
```

`TECH-005` couvre le substrat économique matériel.

`TECH-006` couvre le substrat cognitif générique.

---

# Frontières maintenues

TECH ne devient pas l'autorité sur :

- prix, monnaie ou marché ;
- métiers et carrières concrets ;
- Habitudes narratives concrètes ;
- Types d'Ambitions concrets ;
- personnalité ;
- mémoire narrative du monde ;
- règles de Game Design nouvelles.

Ces sujets restent soumis à leurs autorités amont.

---

# Contenu futur

Les prochains documents seront créés lorsqu'une nouvelle capacité technique cohérente atteint un point de consolidation pertinent.

```text
TECH-007
TECH-008
...
```

Aucun sujet n'est réservé à l'avance.

---

# État actuel

```text
Documents numérotés : 6

TECH-001  ✅ Systems de population
TECH-002  ✅ Boucle de vie minimale
TECH-003  ✅ Orchestration autonome
TECH-004  ✅ Décision autonome par besoins
TECH-005  ✅ Production et circulation autonomes
TECH-006  ✅ Cognition autonome générique
```

---

# Historique

## Version 1.5

- ajout de TECH-005 et TECH-006 au point de consolidation suivant ENGINE-017 ;
- documentation des lots ENGINE-013 à ENGINE-017 jusque-là non consolidés dans TECH ;
- validation globale de référence portée à 291 / 291 ;
- nombre de documents numérotés porté à 6.

## Version 1.4

- ajout de TECH-004 ;
- consolidation ENGINE-011/012 à 178 / 178 ;
- prise en compte de MASTER-006 v1.1.

## Version 1.3

- ajout de TECH-003 ; validation ENGINE-010 à 146 / 146.

## Version 1.2

- ajout de TECH-002 ; validation ENGINE-009 à 134 / 134.

## Version 1.1

- activation de la bibliothèque et création de TECH-001.

## Version 1.0

- création de la bibliothèque TECH.
