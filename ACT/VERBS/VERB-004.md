# VERB-004 — Donner une denrée

> Version : 1.0
> Statut : Proposition
> Type : Verbe d'Action
> Maturité : 2
> Bibliothèque : ACT
> Dépendances : GDB-004A v1.2, GDB-005E v1.2, GDB-005F v1.1, ACT-002-B, ACT-002-C, ACT-002-E, ACT-005-A, ACT-008-A, PAT-004

---

# 1. Objectif

Définir le premier Verbe concret de circulation économique entre habitants : `Donner une denrée`.

VERB-004 spécialise PAT-004 afin de déplacer volontairement un nombre de portions d'un produit alimentaire depuis un stock source vers un stock destination compatible rattaché au contexte du destinataire.

---

# 2. Chaîne de spécialisation

```text
Principe : Échange
↓
PAT-004 : Transfert
↓
VERB-004 : Donner une denrée
↓
Action exécutée
```

VERB-004 n'appartient à aucun autre Pattern.

---

# 3. Origine métier

GDB-004A v1.2 autorise un transfert autonome seulement lorsqu'une opportunité volontaire réellement disponible existe.

GDB-005F v1.1 définit le transfert volontaire minimal entre deux parties.

GDB-005E v1.2 impose l'identité de produit et la conservation des quantités entre stocks compatibles.

---

# 4. Identifiants

Nom conceptuel :

```text
Donner une denrée
```

Identifiant VERBS :

```text
VERB-004
```

Objectif d'Intent associé au premier lot moteur :

```text
donner_denree
```

L'Intent exprime uniquement l'objectif. Il ne contient ni destinataire, ni stocks, ni quantité.

---

# 5. Contrat resserré

VERB-004 resserre PAT-004 à :

```text
1 Acteur donneur
+
1 destinataire distinct
+
1 stock FoodProduct source
+
1 stock FoodProduct destination compatible
+
q portions entières > 0
```

L'opportunité sélectionnée fournit :

- le destinataire ;
- la Cible source ;
- la Cible destination ;
- la quantité de portions à transférer.

---

# 6. Cibles

## Cible principale

Le stock alimentaire destination dont la disponibilité doit augmenter.

## Cibles secondaires

- le stock alimentaire source dont la disponibilité doit diminuer ;
- le destinataire, pour préserver la traçabilité de la partie qui reçoit la valeur.

L'Acteur donneur reste l'origine de l'Action.

Les Cibles concrètes sont sélectionnées par le Planner à partir de l'opportunité de transfert, jamais encodées dans l'Intent.

---

# 7. Preconditions

Avant Validation :

- l'Acteur donneur existe et est éligible ;
- le destinataire existe et est distinct de l'Acteur ;
- l'opportunité de transfert est encore disponible et volontaire ;
- le stock source existe ;
- le stock destination existe ;
- les deux stocks sont des produits alimentaires ;
- ils portent la même identité de produit explicite ;
- la quantité à transférer est strictement positive ;
- le stock source contient au moins cette quantité ;
- le contexte confirme l'autorisation/accessibilité requise.

Si une de ces conditions cesse d'être vraie, l'Action ne peut pas réussir comme si elle l'était encore.

---

# 8. Effects

Après Outcome réussi :

```text
source.PortionsDisponibles -= q

destination.PortionsDisponibles += q
```

La somme des portions source + destination reste identique.

Aucun besoin n'est directement restauré par le don : le destinataire devra utiliser normalement le produit via VERB-002 — Manger lorsqu'il devient accessible.

---

# 9. Events

L'implémentation peut publier au minimum :

```text
produit.alimentaire.transfere
```

L'Event est observable et ne remplace jamais l'état réel des deux stocks.

---

# 10. Décision autonome

VERB-004 ne décide jamais de la volonté de donner.

```text
GDB / opportunité contextuelle
= transfert volontaire disponible

VERB-004
= capacité de déplacer les portions
```

Le premier ordre autonome applicable est :

```text
entretien
↓
transfert volontaire
↓
production
```

VERB-004 respecte cet ordre sans le redéfinir.

---

# 11. Frontière avec commerce

VERB-004 ne crée pas :

- paiement ;
- contrepartie ;
- prix ;
- monnaie ;
- taux de troc ;
- vente ;
- bénéfice ;
- taxe ;
- marché.

Il démontre seulement la circulation réelle d'un produit entre deux habitants.

---

# 12. Application des quatre tests ACT-008-A

## 1. Paramétrage

Aucun Verbe existant ne déplace un produit intact entre deux stocks.

Résultat : non couvert.

## 2. Composition

`Produire une denrée` puis `Manger` ne transfère pas un stock entre habitants ; cette composition transformerait ou consommerait le produit.

Résultat : non couvert.

## 3. Pattern existant

PAT-001, PAT-002 et PAT-003 ont des contrats incompatibles avec la conservation d'un transfert.

Résultat : aucun Pattern existant.

## 4. Nouveau Pattern

PAT-004 — Transfert est justifié et VERB-004 en est le premier Verbe.

---

# 13. Invariants

- VERB-004 spécialise exactement PAT-004.
- L'Intent `donner_denree` ne contient aucune Cible ni quantité concrète.
- Le Planner sélectionne l'opportunité et matérialise les Cibles.
- Le donneur et le destinataire sont distincts.
- Source et destination portent la même identité de produit.
- Une réussite soustrait et ajoute exactement la même quantité.
- Aucun stock ne devient négatif.
- Aucune contrepartie n'est créée.
- Aucun effet relationnel ou besoin n'est appliqué implicitement.

---

# 14. Contrat QA

La validation devra démontrer au minimum :

1. la traçabilité `Échange → PAT-004 → VERB-004 → Action` ;
2. l'appartenance unique de VERB-004 à PAT-004 ;
3. l'absence d'Intent sans opportunité volontaire ;
4. la sélection du destinataire, des stocks et de la quantité par le contexte/Planner ;
5. le refus d'un destinataire absent ou identique au donneur ;
6. le refus d'une source insuffisante ;
7. le refus de produits d'identités différentes ;
8. la conservation exacte des portions ;
9. l'absence de mutation après échec ;
10. le déterminisme ;
11. l'intégration avec l'ordre `entretien → échange → production` ;
12. un scénario autonome où une denrée produite circule vers un autre habitant puis est consommée normalement par celui-ci.

---

# 15. Critère de validation

VERB-004 permet-il à un habitant de mettre volontairement une denrée réellement existante à disposition d'un autre habitant par transfert conservatif entre stocks compatibles, sans inventer de paiement, prix ou marché ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# HISTORIQUE

## Version 1.0

- création de `VERB-004 — Donner une denrée` ;
- spécialisation de PAT-004 — Transfert ;
- objectif d'Intent `donner_denree` ;
- transfert conservatif entre deux stocks alimentaires compatibles ;
- destinataire explicite ;
- séparation avec commerce monétaire, troc et effets relationnels.

---

Fin du document
