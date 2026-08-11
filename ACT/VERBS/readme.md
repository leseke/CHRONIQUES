# VERBS — Catalogue des Verbes d'Actions

> Version : 1.5
> Statut : Active
> Type : Sous-bibliothèque ACT
> Maturité : 2
> Bibliothèque : ACT

---

# Objectif

Référencer les Verbes concrets réellement nécessaires aux mécaniques de Chroniques.

Un Verbe représente une capacité exprimable située entre un Pattern et une Action exécutée conformément à [réf: ACT-002-B] et [réf: ACT-002-C].

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

Officiel / Maturité 4 — validation `161 / 161`.  
Intent : `se_reposer`.

---

## VERB-002 — Manger

Officiel / Maturité 4 — validation `178 / 178`.  
Intent : `manger`.

---

## VERB-003 — Produire une denrée

Officiel / Maturité 4 — validation `201 / 201`.  
Intent : `produire_denree`.

```text
Transformation → PAT-003 Production → VERB-003 Produire une denrée
```

Une réussite consomme une entrée matérielle, produit une sortie alimentaire et conserve une provenance.

---

## VERB-004 — Donner une denrée

Statut : Proposition.  
Maturité : 2.

Origine métier : GDB-004A v1.2, GDB-005E v1.2 et GDB-005F v1.1.

```text
Échange
↓
PAT-004 Transfert
↓
VERB-004 Donner une denrée
```

Intent associé :

```text
donner_denree
```

Le premier contrat resserré déplace un nombre entier positif de portions entre deux stocks alimentaires distincts et compatibles du même produit.

Une réussite :

```text
source -= q
destination += q
```

Le destinataire est explicite. Aucun besoin n'est restauré directement et aucune contrepartie n'est créée.

VERB-004 ne définit ni prix, ni monnaie, ni vente, ni troc réciproque, ni effet relationnel implicite.

---

# État actuel

```text
VERB-001  Se reposer            Officiel / Maturité 4
VERB-002  Manger                Officiel / Maturité 4
VERB-003  Produire une denrée   Officiel / Maturité 4
VERB-004  Donner une denrée     Proposition / Maturité 2
```

La sous-bibliothèque VERBS reste ouverte.

---

# Critère de validation

Chaque Verbe catalogué répond-il à un besoin GDB réel, spécialise-t-il exactement un Pattern et possède-t-il une définition suffisamment précise pour produire des Actions sans ambiguïté ni duplication ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# Historique

## Version 1.5

- création et enregistrement de `VERB-004 — Donner une denrée` en Proposition / Maturité 2 ;
- rattachement unique à PAT-004 — Transfert ;
- objectif d'Intent `donner_denree` ;
- circulation conservatrice d'un produit entre deux habitants ;
- séparation explicite avec commerce monétaire et troc.

## Version 1.4

- VERB-003 passe à Officiel / Maturité 4 ;
- validation locale portée à 201 / 201.

## Versions 1.0 à 1.3

- création de VERBS ;
- création et validation progressive de VERB-001 à VERB-003.

---

Fin du document
