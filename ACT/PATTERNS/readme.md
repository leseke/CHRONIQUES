# PATTERNS — Catalogue des Patterns d'Actions

> Version : 1.4
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

---

# Patterns actuels

## PAT-001 — Repos

Statut : Officiel.

Maturité : 4.

Validation de référence : `161 / 161` tests réussis.

```text
Principe Entretien
↓
PAT-001 Repos
↓
VERB-001 Se reposer
```

---

## PAT-002 — Alimentation

Statut : Officiel.

Maturité : 4.

Validation de référence : `178 / 178` tests réussis.

```text
Principe Entretien
↓
PAT-002 Alimentation
↓
VERB-002 Manger
```

PAT-002 formalise la consommation réelle d'un produit alimentaire accessible afin de contribuer au besoin de nourriture.

---

## PAT-003 — Production

Statut : Officiel.

Maturité : 4.

Validation de référence : `201 / 201` tests réussis.

Origine métier : GDB-004A v1.1, GDB-005C v1.2, GDB-012B v1.1 et GDB-012E v1.1.

```text
Principe Transformation
↓
PAT-003 Production
↓
VERB-003 Produire une denrée
```

PAT-003 formalise une transformation productive réelle :

```text
entrées accessibles consommées
↓
sorties produites
+
provenance conservée
```

Il est distinct de PAT-001 et PAT-002 par sa structure de contrat entrée → sortie.

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
PAT-001  Repos         Officiel / Maturité 4
PAT-002  Alimentation  Officiel / Maturité 4
PAT-003  Production    Officiel / Maturité 4
```

La sous-bibliothèque PATTERNS reste ouverte.

---

# Critère de validation

Chaque Pattern catalogué représente-t-il une mécanique réellement distincte, réutilisable et nécessaire, sans dupliquer un Pattern existant ni absorber les règles propres à un Verbe ?

Si la réponse est non, le Pattern doit être corrigé ou supprimé avant validation.

---

# Historique

## Version 1.4

- `PAT-003 — Production` passe à **Officiel / Maturité 4** ;
- validation locale portée à **201 / 201 tests réussis** ;
- production réelle et provenance persistante confirmées ;
- PATTERNS reste ouverte.

## Version 1.3

- création et enregistrement de `PAT-003 — Production` en Proposition / Maturité 2 ;
- rattachement au Principe `Transformation` ;
- provenance et transformation entrée → sortie explicitées.

## Version 1.2

- `PAT-002 — Alimentation` passe à Officiel / Maturité 4 ;
- validation locale portée à 178 / 178.

## Version 1.1

- synchronisation de PAT-001 avec sa validation Officiel / Maturité 4 ;
- création de PAT-002.

## Version 1.0

- création de la sous-bibliothèque PATTERNS ;
- attribution du premier identifiant réel `PAT-001`.

---

Fin du document
