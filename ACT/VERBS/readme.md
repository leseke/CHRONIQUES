# VERBS — Catalogue des Verbes d'Actions

> Version : 1.1
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

# Identifiants

Les Verbes utilisent des identifiants :

```text
VERB-001
VERB-002
VERB-003
...
```

Un identifiant est attribué uniquement à la création effective d'un Verbe.

Les anciens exemples du catalogue ACT n'étaient pas des réservations numériques.

---

# Verbes actuels

## VERB-001 — Se reposer

Statut : Officiel.

Maturité : 4.

Validation de référence : `161 / 161` tests réussis.

Chaîne :

```text
Principe Entretien
↓
PAT-001 Repos
↓
VERB-001 Se reposer
↓
Action exécutée
```

Origine métier : GDB-004B.

Intent associé :

```text
se_reposer
```

---

## VERB-002 — Manger

Statut : Proposition.

Maturité : 2.

Origine métier : GDB-004B v1.2 et GDB-005E v1.1.

Chaîne proposée :

```text
Principe Entretien
↓
PAT-002 Alimentation
↓
VERB-002 Manger
↓
Action exécutée
```

Intent associé :

```text
manger
```

VERB-002 exige une Cible-produit alimentaire accessible. Une réussite réduit réellement la disponibilité du produit et augmente la satisfaction de Faim de l'Acteur.

La Cible concrète appartient au Plan/Action, jamais à l'Intent.

---

# Frontière avec le moteur

VERBS décrit la capacité et son contrat conceptuel.

Le moteur peut utiliser un identifiant technique compatible, mais l'implémentation ne devient pas l'autorité sur le sens du Verbe.

Une valeur de tuning présente dans le code n'est pas automatiquement une règle VERBS.

VERB-002 n'impose notamment aucun système technique d'inventaire : il exige uniquement qu'une future implémentation puisse résoudre une nourriture réellement accessible conformément à GDB-005E.

---

# État actuel

```text
VERB-001  Se reposer  Officiel / Maturité 4
VERB-002  Manger      Proposition / Maturité 2
```

---

# Critère de validation

Chaque Verbe catalogué répond-il à un besoin GDB réel, spécialise-t-il exactement un Pattern et possède-t-il une définition suffisamment précise pour produire des Actions sans ambiguïté ni duplication ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# Historique

## Version 1.1

- synchronisation de VERB-001 avec sa validation Officiel / Maturité 4 ;
- création et enregistrement de VERB-002 — Manger en Proposition / Maturité 2 ;
- rattachement à PAT-002 — Alimentation ;
- exigence d'une Cible alimentaire accessible et réellement consommée.

## Version 1.0

- création de la sous-bibliothèque VERBS ;
- attribution du premier identifiant réel `VERB-001` ;
- enregistrement de `VERB-001 — Se reposer`.

---

Fin du document
