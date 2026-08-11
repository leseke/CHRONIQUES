# VERB-003 — Produire une denrée

> Version : 1.0
> Statut : Proposition
> Type : Verbe d'Action
> Maturité : 2
> Bibliothèque : ACT
> Dépendances : GDB-004A, GDB-005C, GDB-012B, GDB-012E, ACT-002-B, ACT-002-C, ACT-002-E, ACT-005-A, ACT-008-A, PAT-003

---

# 1. Objectif

Définir le premier Verbe productif concret de Chroniques : `Produire une denrée`.

VERB-003 spécialise PAT-003 afin de transformer une entrée matérielle accessible en quantité de produit alimentaire selon une opération productive explicitement disponible.

---

# 2. Chaîne de spécialisation

```text
Principe : Transformation
↓
PAT-003 : Production
↓
VERB-003 : Produire une denrée
↓
Action exécutée
```

VERB-003 n'appartient à aucun autre Pattern.

---

# 3. Origine métier

GDB-004A autorise une activité productive autonome lorsque aucun Intent d'entretien immédiatement exécutable n'est produit et qu'une activité réelle reste disponible.

GDB-012B définit l'activité productive.

GDB-005C définit l'opération de production et ses invariants de consommation, sortie et provenance.

GDB-012E définit la production exécutable et sa frontière avec le commerce.

---

# 4. Identifiants

Nom conceptuel :

```text
Produire une denrée
```

Identifiant VERBS :

```text
VERB-003
```

Objectif d'Intent associé au premier lot moteur :

```text
produire_denree
```

L'Intent exprime l'objectif mais ne porte ni recette, ni quantité, ni Cible concrète.

---

# 5. Contrat resserré du premier Verbe

VERB-003 resserre PAT-003 à une forme volontairement minimale :

```text
1 entrée matérielle
+
1 sortie alimentaire
```

L'opération sélectionnée fournit :

- l'identité de l'opération ;
- la Cible d'entrée ;
- la quantité d'entrée à consommer ;
- la Cible de sortie alimentaire ;
- le nombre de portions à produire.

Les quantités sont strictement positives.

---

# 6. Cibles

## Cible principale

Le produit alimentaire dont la disponibilité doit augmenter.

## Cible secondaire

L'entrée matérielle réellement consommée.

L'Acteur reste l'origine de l'Action et n'a pas besoin d'être une Cible si aucun Effect direct ne modifie son état personnel.

La Cible concrète est sélectionnée par le Planner à partir de l'activité productive disponible, jamais encodée dans l'Intent.

---

# 7. Preconditions

Avant Validation :

- l'Acteur existe et est éligible ;
- une opération productive correspondant à l'Acteur est actuellement disponible ;
- l'entrée matérielle existe ;
- sa quantité disponible est supérieure ou égale à la quantité requise ;
- l'entrée est accessible dans le contexte de l'activité ;
- la sortie alimentaire existe comme destination de stock ou représentation compatible ;
- la sortie est bien un produit alimentaire exploitable par GDB-005E.

Si une de ces conditions cesse d'être vraie, l'Action ne peut pas réussir comme si elle l'était encore.

---

# 8. Effects

Après Outcome réussi :

```text
entrée matérielle disponible
→ diminue de la quantité configurée

sortie alimentaire disponible
→ augmente du nombre de portions configuré
```

La sortie reçoit ou complète une provenance permettant de retrouver :

- l'opération ;
- l'entrée consommée ;
- l'instant de production.

Aucun Effect n'est appliqué après un Outcome en échec dans le premier lot minimal.

---

# 9. Events

L'implémentation peut publier au minimum :

```text
production.entree.consommee
production.denree.creee
```

Ces événements sont des faits observables et ne remplacent jamais l'état persistant des stocks ou de la provenance.

---

# 10. Décision autonome

VERB-003 ne décide jamais de travailler.

```text
GDB-004A / source autonome
= choix de l'objectif

VERB-003
= capacité de production
```

Le premier ordre autonome est :

```text
entretien exécutable
avant
activité productive
```

VERB-003 ne définit pas cet ordre ; il le respecte.

---

# 11. Frontière avec métier et économie commerciale

VERB-003 ne crée pas :

- métier ;
- employeur ;
- salaire ;
- monnaie ;
- prix ;
- marché ;
- vente ;
- bénéfice.

Il apporte uniquement la première transformation économique réelle du World : des entrées consommées produisent une sortie utile et traçable.

---

# 12. Application des quatre tests ACT-008-A

## 1. Paramétrage

Ni `Se reposer` ni `Manger` ne possède une structure entrées → sortie productive.

Résultat : non couvert.

## 2. Composition

La composition des deux Verbes existants ne produit aucune nouvelle quantité de produit.

Résultat : non couvert.

## 3. Pattern existant

PAT-001 et PAT-002 ont des contrats incompatibles.

Résultat : aucun Pattern existant.

## 4. Nouveau Pattern

PAT-003 — Production est justifié et VERB-003 en est le premier Verbe.

---

# 13. Invariants

- VERB-003 spécialise exactement PAT-003.
- L'Intent `produire_denree` ne contient aucune Cible concrète.
- Le Planner choisit l'opération et les Cibles.
- Une entrée insuffisante ou inaccessible interdit la réussite.
- Une réussite consomme exactement la quantité d'entrée configurée.
- Une réussite ajoute exactement les portions de sortie configurées.
- Une sortie produite possède une provenance exploitable.
- Aucun prix, salaire ou métier implicite n'est créé.

---

# 14. Contrat QA

La validation devra démontrer au minimum :

1. la traçabilité `Transformation → PAT-003 → VERB-003 → Action` ;
2. l'appartenance unique de VERB-003 à PAT-003 ;
3. l'absence d'Intent productif sans opération exécutable ;
4. la sélection de l'opération par le contexte/Planner et non par l'Intent ;
5. le refus d'une entrée absente, insuffisante ou inaccessible ;
6. le refus d'une sortie alimentaire invalide ;
7. la consommation exacte de l'entrée ;
8. l'augmentation exacte des portions de sortie ;
9. la provenance persistante de la sortie ;
10. l'absence de mutation après échec ;
11. le déterminisme à état et configuration identiques ;
12. l'intégration avec l'arbitrage autonome entretien → travail.

---

# 15. Critère de validation

VERB-003 permet-il à un Acteur de transformer une entrée matérielle réelle en une denrée alimentaire réelle et traçable selon une opération explicite, sans inventer de marché, de salaire ou de carrière ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# HISTORIQUE

## Version 1.0

- création de `VERB-003 — Produire une denrée` ;
- spécialisation de PAT-003 — Production ;
- objectif d'Intent `produire_denree` ;
- contrat minimal une entrée / une sortie alimentaire ;
- provenance et consommation réelle rendues obligatoires ;
- séparation avec carrière et économie commerciale.

---

Fin du document
