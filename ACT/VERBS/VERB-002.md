# VERB-002 — Manger

> Version : 1.0
> Statut : Proposition
> Type : Verbe d'Action
> Maturité : 2
> Bibliothèque : ACT
> Dépendances : GDB-004B, GDB-005E, ACT-002-B, ACT-002-C, ACT-002-E, ACT-005-A, ACT-008-A, PAT-002

---

# 1. Objectif

Définir le Verbe concret `Manger`, deuxième capacité cataloguée dans VERBS.

VERB-002 spécialise PAT-002 afin de fournir une capacité exécutable répondant au besoin de nourriture défini par GDB-004B.

---

# 2. Chaîne de spécialisation

```text
Principe : Entretien
↓
PAT-002 : Alimentation
↓
VERB-002 : Manger
↓
Action exécutée
```

VERB-002 n'appartient à aucun autre Pattern.

---

# 3. Origine métier

GDB-004B définit le contrat autonome proposé :

```text
Faim < seuil configuré
+
produit alimentaire accessible
↓
Intent : manger
```

GDB-005E définit le produit alimentaire, son accessibilité métier et la consommation réelle de sa disponibilité.

VERB-002 représente la capacité ACT permettant de traiter cet Intent.

---

# 4. Identifiants

Nom conceptuel :

```text
Manger
```

Identifiant VERBS :

```text
VERB-002
```

Objectif d'Intent associé :

```text
manger
```

L'identifiant technique d'une future Action Definition devra rester compatible avec cette capacité sans devenir l'autorité sur son sens.

---

# 5. Cible principale

VERB-002 cible principalement un produit alimentaire réel.

Le produit doit :

- exister ;
- être alimentaire ;
- disposer encore d'une quantité consommable ;
- être accessible à l'Acteur au moment de la Validation.

L'Acteur est également destinataire de l'effet de restauration de Faim.

L'Intent `manger` ne contient pas la Cible concrète : le Planner doit sélectionner une Cible éligible conformément à ACT.

---

# 6. Action Contract

VERB-002 respecte la structure de PAT-002 et ACT-002-E.

## Inputs

- un Acteur ;
- un produit alimentaire sélectionné comme Cible principale.

## Preconditions

- Cible existante ;
- Cible alimentaire ;
- disponibilité consommable strictement positive ;
- Cible accessible à l'Acteur.

## Constraints

Aucune Constraint universelle supplémentaire dans cette version.

## Costs

Aucun Cost abstrait universel n'est défini.

Le produit réellement consommé n'est pas un coût fictif : sa disponibilité est diminuée par les Effects de l'Action.

## Effects

Après Outcome réussi :

```text
produit alimentaire disponible ↓
Faim de l'Acteur ↑
```

La restauration de Faim reste bornée par la plage `0..100` définie par GDB-004B.

## Events

L'implémentation future pourra publier des faits observables liés à la consommation et à la restauration de Faim.

Les identifiants techniques exacts seront fixés dans la spécification ENGINE applicable avant code.

---

# 7. Valeur alimentaire

VERB-002 ne fixe aucune valeur universelle de restauration.

La valeur consommée dépend du produit ou des données d'équilibrage prévues par GDB-005E.

VERB-002 exige uniquement que la valeur produise une contribution cohérente au besoin de nourriture.

---

# 8. Application des quatre tests ACT-008-A

## 1. Paramétrage

`VERB-001 — Se reposer` ne peut pas être paramétré en `Manger` : il ne possède ni Cible-produit ni consommation de disponibilité.

Résultat : non couvert.

## 2. Composition

Aucune composition de `VERB-001` ne peut produire l'alimentation.

Résultat : non couvert.

## 3. Pattern existant

PAT-001 — Repos possède une structure différente.

PAT-002 — Alimentation est créé pour la mécanique requise.

Résultat : VERB-002 appartient à PAT-002.

## 4. Nouveau Pattern

La création de PAT-002 est justifiée par la différence de structure contractuelle entre repos et alimentation.

---

# 9. Frontière avec la décision autonome

VERB-002 ne décide jamais quand un habitant doit manger.

```text
GDB-004B / future politique ENGINE
= décision

VERB-002
= capacité
```

La capacité peut être utilisée par un joueur, un PNJ ou tout autre Acteur éligible sans modifier son sens ACT.

---

# 10. Frontière avec l'accessibilité

VERB-002 exige une Cible accessible mais ne définit pas comment cette accessibilité est représentée techniquement.

L'architecture future peut employer inventaire, possession, contexte, résolution d'accès ou autre mécanisme compatible avec GDB-005E.

Le Verbe reste inchangé tant que la règle métier est respectée.

---

# 11. Non-objectifs

VERB-002 ne définit pas :

- acheter de la nourriture ;
- cuisiner ;
- récolter ;
- fabriquer ;
- transporter ;
- voler de la nourriture ;
- partager un repas ;
- boire ;
- digestion ;
- préférences ou allergies ;
- effets automatiques sur Santé ou Moral.

---

# 12. Invariants

- VERB-002 spécialise exactement PAT-002.
- VERB-002 ne peut pas être remplacé par un paramétrage de VERB-001.
- Une Action `Manger` cible un produit alimentaire réel et accessible.
- Une Cible sans disponibilité consommable ne peut pas produire une réussite.
- Une réussite diminue la disponibilité de la Cible.
- Une réussite augmente la satisfaction de Faim de l'Acteur.
- L'Intent ne contient jamais la Cible concrète.
- Le Verbe ne fixe aucun seuil autonome.
- Le Verbe ne fixe aucune valeur alimentaire universelle.

---

# 13. Contrat QA

La validation devra démontrer au minimum :

1. la traçabilité `Entretien → PAT-002 → VERB-002 → Action` ;
2. l'appartenance de VERB-002 à un seul Pattern ;
3. le refus d'une Cible absente, non alimentaire, épuisée ou inaccessible ;
4. la sélection d'une Cible alimentaire par le Plan et non par l'Intent ;
5. l'exécution réussie jusqu'à l'Outcome ;
6. la diminution réelle de disponibilité du produit ;
7. l'augmentation de Faim de l'Acteur ;
8. l'absence de mutation avant résolution réussie ;
9. le déterminisme à état et configuration identiques.

---

# 14. Critère de validation

VERB-002 permet-il de représenter sans ambiguïté l'Action « Manger » comme consommation réelle d'un produit alimentaire accessible, distincte de la décision de manger et des mécaniques d'achat, cuisine ou production ?

Si la réponse est non, le Verbe doit être corrigé avant validation.

---

# HISTORIQUE

## Version 1.0

- création de `VERB-002 — Manger` ;
- spécialisation de PAT-002 — Alimentation ;
- rattachement au second contrat autonome de GDB-004B ;
- intégration des règles de produit alimentaire et d'accessibilité de GDB-005E ;
- séparation entre Intent, sélection de Cible, capacité ACT et représentation ENGINE future.

---

Fin du document
