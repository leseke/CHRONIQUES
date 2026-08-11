# PATTERNS — Catalogue des Patterns d'Actions

> Version : 1.0
> Statut : Active
> Type : Sous-bibliothèque ACT
> Maturité : 2
> Bibliothèque : ACT

---

# Objectif

Référencer les Patterns réellement nécessaires aux Actions de Chroniques.

Un Pattern représente une mécanique réutilisable située entre un Principe et un Verbe conformément à [réf: ACT-002-B] et [réf: ACT-002-C].

```text
Principe
↓
Pattern
↓
Verbe
↓
Action
```

PATTERNS ne définit aucune règle métier de GDB et n'énumère aucun comportement qui n'est pas encore justifié par un besoin réel.

---

# Autorité

La création et l'organisation des Patterns respectent notamment :

- [réf: ACT-002-B] pour les niveaux d'abstraction ;
- [réf: ACT-002-C] pour les relations de spécialisation ;
- [réf: ACT-008-A] pour les familles de Verbes et le critère de création.

Un Pattern :

- spécialise un Principe ;
- reste indépendant des acteurs particuliers, objets particuliers et contextes particuliers ;
- peut être spécialisé par zéro, un ou plusieurs Verbes ;
- ne dépend jamais d'une Action exécutée.

---

# Règle d'attribution

Un identifiant `PAT-xxx` n'est attribué qu'à l'apparition d'un besoin concret.

Les exemples historiques présents dans `ACT/CATALOG.md` avant la création de cette sous-bibliothèque n'étaient pas des réservations d'identifiants.

La numérotation réelle commence donc avec le premier Pattern effectivement requis par le moteur validé.

---

# Patterns actuels

## PAT-001 — Repos

Statut : Proposition.

Maturité : 2.

Premier Pattern concret de Chroniques.

Il formalise la mécanique générique permettant à un Acteur de restaurer la satisfaction de son besoin de repos, sans imposer la manière particulière de se reposer.

Spécialisation actuelle :

```text
PAT-001 Repos
↓
VERB-001 Se reposer
```

---

# Frontière avec VERBS

PATTERNS définit la mécanique commune.

VERBS définit la capacité concrète.

```text
PATTERN
= structure réutilisable

VERBE
= spécialisation exprimable
```

Un Pattern ne doit jamais contenir les règles propres à un Verbe concret si celles-ci ne sont pas partagées par toute sa famille.

---

# État actuel

```text
PAT-001  Repos  Proposition / Maturité 2
```

---

# Critère de validation

Chaque Pattern catalogué représente-t-il une mécanique réellement distincte, réutilisable et nécessaire, sans dupliquer un Pattern existant ni absorber les règles propres à un Verbe ?

Si la réponse est non, le Pattern doit être corrigé ou supprimé avant validation.

---

# Historique

## Version 1.0

- création de la sous-bibliothèque PATTERNS ;
- attribution du premier identifiant réel `PAT-001` ;
- enregistrement de `PAT-001 — Repos`.

---

Fin du document
