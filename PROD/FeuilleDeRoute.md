# Chroniques — Feuille de Route V2.8

> Version : 2.8
> Statut : Officiel
> Type : Roadmap
> Maturité : 2
> Bibliothèque : PROD

---

# Vision

Chroniques est un moteur de simulation narratif construit selon une approche Documentation First.

Chaîne d'autorité :

```text
MASTER → CORE → GDB → ACT → ENGINE → CHRONIQUES-ENGINE → Tests → TECH
```

MASTER-006 distingue validation courante et consolidation documentaire. La V2.8 correspond à la consolidation du bloc **cognition durable + Mémoire du Monde + continuité générationnelle**.

---

# État validé

```text
dotnet build
→ succès

dotnet test
→ 380 / 380 tests réussis
→ 0 échec
```

## Lots v0.4 validés

```text
ENGINE-010                 orchestration autonome
ENGINE-011 / 012           besoins autonomes
ENGINE-013 / 014           production + circulation
ENGINE-015 / 016 / 017     observation + Habitudes + Ambitions
ENGINE-018                 Personnalité générique
ENGINE-019                 Mémoire du Monde générique
ENGINE-020                 continuité générationnelle explicite
```

Consolidations :

```text
TECH-003 / 004
TECH-005 — Production et circulation autonomes
TECH-006 — Cognition autonome générique
TECH-007 — Cognition durable, Mémoire et continuité générationnelle
```

---

# Capacités actuelles

Le moteur sait désormais faire coexister :

```text
habitants autonomes
+
production et transfert matériels
+
Habitudes
+
Ambitions
+
Personnalité persistante
+
Mémoire narrative du monde
+
continuité de lignée persistante
```

La Mémoire du Monde peut évoluer selon le marqueur générationnel d'une continuité identifiée, sans compteur global du World et sans conversion arbitraire Tick → génération.

---

# v0.4 — Le monde vivant

Objectif de phase : faire évoluer le monde de manière crédible sans intervention permanente du joueur.

## Capacités validées

- autonomie physiologique ;
- production et circulation matérielles ;
- cognition générique ;
- Personnalité générique ;
- Mémoire du Monde générique ;
- continuité générationnelle explicite.

## Capacités encore manquantes ou incomplètes

- démonstration multi-générations complète de bout en bout ;
- événements mondiaux autonomes complets ;
- interactions sociales autonomes suffisamment riches ;
- Types concrets de Mémoire ;
- comportements cognitifs narratifs concrets ;
- économie commerciale complète ;
- mappings Trait/Habitude et Trait/Ambition.

---

# Critère de sortie v0.4

```text
Le monde évolue de façon crédible pendant plusieurs générations
sans intervention permanente du joueur.
```

À 380 / 380, les briques nécessaires à une vraie continuité historique existent désormais, mais la démonstration intégrée sur plusieurs générations n'est pas encore réalisée.

v0.4 reste donc **ouverte**.

---

# Prochaine frontière immédiate

Construire une démonstration déterministe de bout en bout :

```text
Génération 0
↓
actions autonomes
↓
faits qualifiés / Mémoire
↓
mort + héritage
↓
continuité GenerationIndex +1
↓
Génération 1
↓
Mémoire réévaluée
↓
nouvelle vie autonome
↓
seconde transmission
↓
Génération 2
```

Cette démonstration doit réutiliser les Systems et contrats existants plutôt qu'introduire une nouvelle règle métier artificielle.

---

# Frontières parallèles

L'économie commerciale reste bloquée tant que les autorités correspondantes ne définissent pas suffisamment monnaie, prix, vente et marché.

Les mappings psychologiques concrets restent également bloqués tant qu'un Trait et un comportement concret n'ont pas été canonisés ensemble.

---

# Versions suivantes

## v0.5 — La profondeur

Économie avancée, métiers, médecine, justice, crime, politique, religion, combat et patrimoine avancé selon autorités.

## v0.6 — Les outils

Éditeur de contenu, debugger de simulation, inspection du World et diagnostics déterministes.

## v1.0 — Première alpha

Boucle complète, sauvegarde versionnée, équilibrage, interface, stabilité et diagnostics suffisants.

---

# Historique

## Version 2.8

- ENGINE-018 à ENGINE-020 consolidés ;
- validation portée à 380 / 380 ;
- TECH-007 et audit Mémoire + Générations ajoutés ;
- Mémoire du Monde reliée à une continuité générationnelle explicite ;
- prochaine frontière fixée à la démonstration multi-générations intégrée.

## Version 2.7

- production/circulation et cognition autonome consolidées à 291 / 291.

---

Fin du document
