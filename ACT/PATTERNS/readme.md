# PATTERNS — Catalogue des Patterns d'Actions

> Version : 1.5
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

---

# Patterns actuels

## PAT-001 — Repos

Statut : Officiel.  
Maturité : 4.  
Validation de référence : `161 / 161`.

```text
Entretien → PAT-001 Repos → VERB-001 Se reposer
```

---

## PAT-002 — Alimentation

Statut : Officiel.  
Maturité : 4.  
Validation de référence : `178 / 178`.

```text
Entretien → PAT-002 Alimentation → VERB-002 Manger
```

---

## PAT-003 — Production

Statut : Officiel.  
Maturité : 4.  
Validation de référence : `201 / 201`.

```text
Transformation
↓
PAT-003 Production
↓
VERB-003 Produire une denrée
```

Contrat : entrées consommées → sortie produite + provenance.

---

## PAT-004 — Transfert

Statut : Proposition.  
Maturité : 2.

Origine métier : GDB-005E v1.2 et GDB-005F v1.1.

```text
Échange
↓
PAT-004 Transfert
↓
VERB-004 Donner une denrée
```

PAT-004 formalise un déplacement conservatif de valeur :

```text
stock source P -= q
stock destination P += q
```

Il est distinct d'Alimentation, qui consomme un produit, et de Production, qui transforme des entrées en sorties.

PAT-004 ne définit ni prix, ni paiement, ni contrepartie.

---

# État actuel

```text
PAT-001  Repos         Officiel / Maturité 4
PAT-002  Alimentation  Officiel / Maturité 4
PAT-003  Production    Officiel / Maturité 4
PAT-004  Transfert     Proposition / Maturité 2
```

La sous-bibliothèque PATTERNS reste ouverte.

---

# Critère de validation

Chaque Pattern catalogué représente-t-il une mécanique réellement distincte, réutilisable et nécessaire, sans dupliquer un Pattern existant ni absorber les règles propres à un Verbe ?

Si la réponse est non, le Pattern doit être corrigé ou supprimé avant validation.

---

# Historique

## Version 1.5

- création et enregistrement de `PAT-004 — Transfert` en Proposition / Maturité 2 ;
- rattachement au Principe `Échange` ;
- conservation stricte des quantités entre deux stocks compatibles ;
- séparation explicite avec prix, monnaie et marché.

## Version 1.4

- `PAT-003 — Production` passe à Officiel / Maturité 4 ;
- validation locale portée à 201 / 201.

## Versions 1.0 à 1.3

- création de PATTERNS ;
- création et validation progressive de PAT-001 à PAT-003.

---

Fin du document
