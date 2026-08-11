# PATTERNS — Catalogue des Patterns d'Actions

> Version : 1.6
> Statut : Active
> Type : Sous-bibliothèque ACT
> Maturité : 2
> Bibliothèque : ACT

---

# Objectif

Référencer les Patterns réellement nécessaires aux Actions de Chroniques.

```text
Principe
↓
Pattern
↓
Verbe
↓
Action
```

PATTERNS ne définit aucune règle métier GDB et n'ajoute aucun Pattern théorique sans besoin réel.

---

# Patterns actuels

## PAT-001 — Repos

```text
Officiel / Maturité 4
Validation : 161 / 161
Entretien → Repos → VERB-001 Se reposer
```

## PAT-002 — Alimentation

```text
Officiel / Maturité 4
Validation : 178 / 178
Entretien → Alimentation → VERB-002 Manger
```

## PAT-003 — Production

```text
Officiel / Maturité 4
Validation : 201 / 201
Transformation → Production → VERB-003 Produire une denrée
```

Contrat : entrées consommées → sortie produite + provenance.

## PAT-004 — Transfert

```text
Proposition / Maturité 2
Échange → Transfert → VERB-004 Donner une denrée
```

Origine métier : GDB-005E v1.3 et GDB-005F v1.2.

Contrat :

```text
stock source P -= q
stock destination P += q
```

avec :

- `q > 0` ;
- source et destination distinctes ;
- même identité de produit ;
- conservation de la quantité totale ;
- opportunité contextuelle autorisée ;
- aucun prix ni paiement implicite.

PAT-004 reste Proposition/M2 jusqu'à validation moteur.

---

# État actuel

```text
PAT-001  Repos         Officiel / M4
PAT-002  Alimentation  Officiel / M4
PAT-003  Production    Officiel / M4
PAT-004  Transfert     Proposition / M2
```

La sous-bibliothèque PATTERNS reste ouverte.

---

# Critère de validation

Chaque Pattern catalogué représente-t-il une mécanique réellement distincte, réutilisable et nécessaire, sans dupliquer un Pattern existant ni absorber les règles propres à un Verbe ?

---

# Historique

## Version 1.6

- PAT-004 synchronisé avec GDB-005E v1.3 / GDB-005F v1.2 ;
- invariant `stock source ≠ stock destination` enregistré ;
- PAT-004 reste Proposition / Maturité 2 avant validation locale.

## Version 1.5

- création de PAT-004 — Transfert.

## Version 1.4

- PAT-003 validé à 201 / 201.

## Versions 1.0 à 1.3

- création de PATTERNS et validation progressive de PAT-001 à PAT-002 ;
- ouverture de PAT-003.

---

Fin du document
