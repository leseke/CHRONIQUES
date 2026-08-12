# VERBS — Catalogue des Verbes d'Actions

> Version : 1.7
> Statut : Active
> Type : Sous-bibliothèque ACT
> Maturité : 2
> Bibliothèque : ACT

---

# Objectif

Référencer les Verbes concrets réellement nécessaires aux mécaniques de Chroniques.

Aucun Verbe n'est créé pour compléter une liste théorique : chaque Verbe répond à un besoin GDB réel et spécialise exactement un Pattern.

---

# Verbes actuels

## VERB-001 — Se reposer

```text
Officiel / M4
Validation : 161 / 161
Intent : se_reposer
```

## VERB-002 — Manger

```text
Officiel / M4
Validation : 178 / 178
Intent : manger
```

## VERB-003 — Produire une denrée

```text
Officiel / M4
Validation : 201 / 201
Intent : produire_denree
Transformation → PAT-003 Production → VERB-003
```

## VERB-004 — Donner une denrée

```text
Officiel / M4
Validation : 224 / 224
Intent : donner_denree
Échange → PAT-004 Transfert → VERB-004
```

Origine métier : GDB-004A v1.2, GDB-005E v1.3 et GDB-005F v1.2.

Contrat minimal :

```text
Donneur A
+
Destinataire B distinct
+
stock source P
+
stock destination P distinct
+
q > 0
↓
source -= q
destination += q
```

Source et destination sont deux stocks distincts du même produit.

Le transfert ne restaure aucun besoin directement. Le destinataire peut ensuite utiliser VERB-002 — Manger si le produit devient accessible.

VERB-004 ne crée ni prix, monnaie, vente, troc réciproque, négociation ou effet relationnel implicite.

---

# État actuel

```text
VERB-001  Se reposer            Officiel / M4
VERB-002  Manger                Officiel / M4
VERB-003  Produire une denrée   Officiel / M4
VERB-004  Donner une denrée     Officiel / M4
```

La sous-bibliothèque VERBS reste ouverte.

---

# Critère de validation

Chaque Verbe catalogué répond-il à un besoin GDB réel, spécialise-t-il exactement un Pattern et possède-t-il un contrat suffisamment précis pour produire une Action sans ambiguïté ?

---

# Historique

## Version 1.7

- VERB-004 passe à **Officiel / Maturité 4** ;
- validation locale enregistrée à **224 / 224 tests réussis** ;
- scénario production → transfert → alimentation entre habitants confirmé ;
- VERBS reste ouverte.

## Version 1.6

- VERB-004 synchronisé avec GDB-005E v1.3, GDB-005F v1.2 et PAT-004 v1.1 ;
- invariant `stock source ≠ stock destination` enregistré.

## Version 1.5

- création de VERB-004 — Donner une denrée.

## Version 1.4

- VERB-003 validé à 201 / 201.

## Versions 1.0 à 1.3

- création de VERBS et validation progressive de VERB-001 à VERB-002 ;
- ouverture de VERB-003.

---

Fin du document
