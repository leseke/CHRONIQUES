# VERBS — Catalogue des Verbes d'Actions

> Version : 1.0
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

Statut : Proposition.

Maturité : 2.

Premier Verbe concret officiellement catalogué.

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

Intent actuellement associé :

```text
se_reposer
```

---

# Frontière avec le moteur

VERBS décrit la capacité et son contrat conceptuel.

Le moteur peut utiliser un identifiant technique compatible, mais l'implémentation ne devient pas l'autorité sur le sens du Verbe.

Une valeur de tuning présente dans le code n'est pas automatiquement une règle VERBS.

---

# État actuel

```text
VERB-001  Se reposer  Proposition / Maturité 2
```

---

# Critère de validation

Chaque Verbe catalogué répond-il à un besoin GDB réel, spécialise-t-il exactement un Pattern et possède-t-il une définition suffisamment précise pour produire des Actions sans ambiguïté ni duplication ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# Historique

## Version 1.0

- création de la sous-bibliothèque VERBS ;
- attribution du premier identifiant réel `VERB-001` ;
- enregistrement de `VERB-001 — Se reposer`.

---

Fin du document
