# ACT-009-A — Composition d'Actions

> Version : 1.1
>
> Statut : Proposition
>
> Type : Contrat d'architecture
>
> Maturité : 2
>
> Bibliothèque : ACT
>
> Dépendances :
> - ACT-002-C, section 6 (Composition)
> - ACT-002-E (Action Contract)
> - ACT-002-G (Outcome)
> - ACT-002-I (Plan)
> - ACT-007-A (Taxonomie des Conséquences, section 6 --- Composition
>   selon la forme de l'Outcome)
>
> Utilisé par :
> - TECH
> - IA
> - QA

---

# 1. Objectif

Définir les règles de composition d'une Action complexe à partir
d'Actions simples --- propagation d'échec, agrégation de l'Outcome,
héritage du Contexte --- et trancher explicitement la frontière entre
une Action composite et un Plan (ACT-002-I), pour lever une ambiguïté
que ni ACT-002-C ni ACT-002-I ne résolvent aujourd'hui.

ACT-002-C, section 6, pose déjà l'axiome : « Une Action peut être
composée de plusieurs Actions », avec un exemple (construire une
maison) mais sans aucune règle sur ce qui se passe quand une sous-Action
échoue, ni sur la manière dont l'Outcome de l'ensemble se détermine ---
c'est l'objet de ce document.

---

# 2. Principe

Une Action composite reste une Action au sens plein du terme (ACT-002-C,
section 6 : « chaque sous-action reste autonome tout en participant à
l'objectif global »). Elle possède un seul Action Contract (ACT-002-E),
un seul Outcome (ACT-002-G), et est initiée par un seul Intent. Ses
sous-Actions ne sont jamais elles-mêmes reliées chacune à un Intent
propre --- si elles l'étaient, il ne s'agirait plus d'une Action
composite mais d'un Plan (section 3).

---

# 3. Frontière avec le Plan

ACT-002-I (Plan) et le présent document décrivent tous les deux
plusieurs Actions liées entre elles --- ce qui les distingue n'est pas
la structure, mais l'origine de la liaison.

**Un Plan** relie des Actions Instances indépendantes en réponse à un
seul Intent (ACT-002-F, section 3bis). Chaque Action du Plan possède son
propre Outcome ; le Plan peut être suspendu, adapté, abandonné ou
reconstruit si une Action échoue (ACT-002-I, sections 7 et 8) --- jamais
remplacé par un Plan entièrement nouveau sans lien avec le précédent, la
décision restant toujours au même Planner. Les Actions d'un Plan
peuvent viser des Cibles différentes, dans des Contextes différents.

**Une Action composite** est une seule Action Instance, définie par un
seul Action Contract, dont l'exécution interne se décompose en
sous-Actions structurellement fixes --- elles ne sont jamais
réévaluées ni remplacées en cours d'exécution, contrairement aux Actions
d'un Plan. Ses sous-Actions héritent toujours du même Acteur et du même
Contexte que l'Action composite (section 5).

Règle de décision : si la décomposition peut varier selon les
circonstances (essayer une sous-Action, échouer, en essayer une autre à
la place), c'est un Plan. Si la décomposition est toujours la même,
quelle que soit la situation, c'est une Action composite.

---

# 4. Propagation d'échec

L'échec d'une sous-Action ne produit pas automatiquement l'échec de
l'Action composite --- la forme de l'Outcome de l'ensemble dépend de
quelle sous-Action a échoué.

**Sous-Action non essentielle.** Si l'Action Contract composite désigne
la sous-Action comme non essentielle, son échec n'empêche pas la
poursuite des autres sous-Actions ; l'Outcome global peut rester une
Réussite ou devenir une Réussite partielle (ACT-002-G), jamais un Échec
pour cette seule raison.

**Sous-Action essentielle.** Si l'Action Contract composite désigne la
sous-Action comme essentielle, son échec entraîne l'Échec de l'Action
composite dans son ensemble --- les sous-Actions suivantes non encore
exécutées ne le sont jamais.

Quelle sous-Action est essentielle ou non relève de l'Action Contract
propre à chaque Action composite (ACT-002-E) --- ce document ne fixe
qu'la règle de propagation, jamais la désignation au cas par cas.

---

# 5. Héritage du Contexte

Toute sous-Action hérite de l'Acteur de l'Action composite (ACT-004-A)
--- une sous-Action ne peut jamais avoir un Acteur différent. Elle peut
en revanche avoir ses propres Cibles, distinctes de celles de l'Action
composite (ex. : « Transporter des matériaux » cible une Ressource,
« Monter les murs » cible le bâtiment en construction).

Toute Condition (ACT-006-A) qui s'applique à l'Action composite
s'applique aussi à chacune de ses sous-Actions, par héritage --- au même
titre que l'héritage déjà défini entre une Entity et les Actions qui la
concernent (ACT-006-A, section 6).

---

# 6. Agrégation de l'Outcome

L'Action composite produit un seul Outcome (ACT-002-G), jamais un par
sous-Action. Cet Outcome se détermine ainsi :

- Réussite si toutes les sous-Actions essentielles ont réussi ;
- Réussite partielle si au moins une sous-Action non essentielle a
  échoué, mais qu'aucune sous-Action essentielle n'a échoué ;
- Échec si au moins une sous-Action essentielle a échoué (section 4) ;
- Interruption si l'Action composite elle-même a été interrompue
  (ACT-001-E, section 5), indépendamment du sort de ses sous-Actions.

Les Conséquences (ACT-007-A) de chaque sous-Action restent rattachées à
l'Action composite dans son ensemble --- une sous-Action n'a jamais son
propre Outcome consommé séparément par le reste du pipeline
(ACT-002-F).

---

# 7. Contrat

Une Action composite ne peut jamais produire plus d'un Outcome.

Une sous-Action ne peut jamais avoir un Acteur différent de l'Action
composite qui la contient.

La décomposition d'une Action composite en sous-Actions est toujours
fixe --- si elle doit varier selon les circonstances, il ne s'agit pas
d'une Action composite mais d'un Plan (section 3).

---

# 8. Contrat TECH

Le moteur doit être capable de :

- exécuter les sous-Actions d'une Action composite dans l'ordre défini
  par son Action Contract, sans jamais les réévaluer ni les remplacer ;
- appliquer la règle de propagation d'échec (section 4) selon que
  chaque sous-Action est essentielle ou non ;
- agréger un seul Outcome pour l'ensemble (section 6) ;
- transmettre l'Acteur de l'Action composite à chacune de ses
  sous-Actions, sans jamais permettre une substitution.

---

# 9. Contrat QA

Les tests devront vérifier :

✓ qu'une Action composite ne produit jamais plus d'un Outcome ;

✓ que l'échec d'une sous-Action non essentielle ne produit jamais un
Échec de l'ensemble ;

✓ que l'échec d'une sous-Action essentielle produit toujours un Échec
de l'ensemble, et empêche les sous-Actions suivantes de s'exécuter ;

✓ qu'une sous-Action ne peut jamais avoir un Acteur différent de
l'Action composite.

---

# 10. Critères de validation

Ce document est conforme si :

✓ il n'introduit aucun axiome déjà posé par ACT-002-C, section 6 ;

✓ il tranche explicitement la frontière avec ACT-002-I (Plan), sans la
laisser ambiguë comme avant sa création ;

✓ il ne redéfinit jamais les formes de l'Outcome déjà posées par
ACT-002-G, seulement la manière de les agréger pour une Action
composite.

---

# 11. Historique

## Version 1.1

- audit formel (méthodologie MASTER-008) : correction d'une imprécision
  de citation, section 3 (Frontière avec le Plan) --- le texte disait
  qu'un Plan pouvait être « remplacé par un autre Plan » en cas
  d'échec d'une Action, alors qu'ACT-002-I (sections 7 et 8) parle de
  suspension, adaptation, abandon ou reconstruction du même Plan par le
  même Planner, jamais d'un remplacement par un Plan entièrement
  nouveau. Reformulé pour respecter exactement le vocabulaire
  d'ACT-002-I.

## Version 1.0

- Création du document. Élabore ACT-002-C, section 6, avec des règles de
  propagation d'échec, d'héritage du Contexte et d'agrégation de
  l'Outcome, absentes de cette section. Tranche explicitement la
  frontière avec ACT-002-I (Plan), jusqu'ici non résolue. Statut
  Proposition : n'a pas encore traversé les étapes Validée/Spécifiée du
  cycle de vie documentaire d'une mécanique (ACT-001-G, section 14).
