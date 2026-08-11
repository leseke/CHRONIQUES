# VERBS — Catalogue des Verbes d'Actions

> Version : 1.4
> Statut : Active
> Type : Sous-bibliothèque ACT
> Maturité : 2
> Bibliothèque : ACT

---

# Objectif

Référencer les Verbes concrets réellement nécessaires aux mécaniques de Chroniques.

Un Verbe représente une capacité exprimable située entre un Pattern et une Action exécutée conformément à [réf: ACT-002-B] et [réf: ACT-002-C].

```text
Pattern
↓
Verbe
↓
Action
```

VERBS est pilotée par les besoins GDB et respecte les critères de création définis par [réf: ACT-008-A].

---

# Règle fondamentale

Aucun Verbe n'est créé pour compléter une liste théorique.

Un Verbe n'existe que lorsqu'un besoin réel :

- est défini par une autorité GDB applicable ;
- ne peut pas être couvert par simple paramétrage d'un Verbe existant ;
- ne peut pas être couvert par composition de Verbes existants ;
- peut être rattaché sans ambiguïté à exactement un Pattern.

---

# Verbes actuels

## VERB-001 — Se reposer

Statut : Officiel.

Maturité : 4.

Validation de référence : `161 / 161`.

```text
Entretien → Repos → Se reposer
```

Intent : `se_reposer`.

---

## VERB-002 — Manger

Statut : Officiel.

Maturité : 4.

Validation de référence : `178 / 178`.

```text
Entretien → Alimentation → Manger
```

Intent : `manger`.

Une réussite consomme un produit alimentaire accessible et restaure Faim.

---

## VERB-003 — Produire une denrée

Statut : Officiel.

Maturité : 4.

Validation de référence : `201 / 201`.

Origine métier : GDB-004A v1.1, GDB-005C v1.2, GDB-012B v1.1 et GDB-012E v1.1.

```text
Transformation
↓
PAT-003 Production
↓
VERB-003 Produire une denrée
↓
Action exécutée
```

Intent associé :

```text
produire_denree
```

Le contrat validé utilise une entrée matérielle et une sortie alimentaire. Une réussite diminue réellement l'entrée, augmente réellement les portions de sortie et conserve une provenance.

VERB-003 ne définit ni métier, ni salaire, ni prix, ni marché.

---

# Frontière avec le moteur

VERBS décrit les capacités et leurs contrats conceptuels.

Le moteur peut utiliser des identifiants techniques compatibles, mais l'implémentation ne devient jamais l'autorité sur leur sens.

Les valeurs de tuning et opérations concrètes restent configurables selon les autorités GDB/ENGINE applicables.

---

# État actuel

```text
VERB-001  Se reposer            Officiel / Maturité 4
VERB-002  Manger                Officiel / Maturité 4
VERB-003  Produire une denrée   Officiel / Maturité 4
```

La sous-bibliothèque VERBS reste ouverte.

---

# Critère de validation

Chaque Verbe catalogué répond-il à un besoin GDB réel, spécialise-t-il exactement un Pattern et possède-t-il une définition suffisamment précise pour produire des Actions sans ambiguïté ni duplication ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# Historique

## Version 1.4

- `VERB-003 — Produire une denrée` passe à **Officiel / Maturité 4** ;
- validation locale portée à **201 / 201 tests réussis** ;
- scénario production → alimentation sans entrée joueur confirmé ;
- VERBS reste ouverte.

## Version 1.3

- création et enregistrement de `VERB-003 — Produire une denrée` en Proposition / Maturité 2 ;
- rattachement unique à PAT-003 — Production ;
- objectif d'Intent `produire_denree` ;
- séparation explicite avec métier, salaire et marché.

## Version 1.2

- `VERB-002 — Manger` passe à Officiel / Maturité 4 ;
- validation locale portée à 178 / 178.

## Version 1.1

- synchronisation de VERB-001 avec sa validation ;
- création de VERB-002.

## Version 1.0

- création de la sous-bibliothèque VERBS ;
- attribution du premier identifiant réel `VERB-001`.

---

Fin du document
