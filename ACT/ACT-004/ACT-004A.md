# ACT-004-A — Acteurs

> Version : 1.0
>
> Statut : Proposition
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT
>
> Dépendances :
> - ACT-001-B (Principe de responsabilité)
> - ACT-001-D (Structure canonique, section Origine)
> - ACT-001-H (Terminologie officielle, entrée Acteur)
> - ACT-002-E (Action Contract, section Inputs)
> - ACT-002-F (Modèle d'exécution, section 8bis)
>
> Utilisé par :
> - TECH
> - IA
> - QA

---

# 1. Objectif

Définir ce qui qualifie une entité comme Acteur capable d'initier une
Action : ses catégories, les conditions de son éligibilité, et les
limites de sa multiplicité.

Ce document n'introduit aucun nouvel axiome. Il élabore le Principe de
responsabilité déjà posé par ACT-001-B, section 2 : *« toute action
possède un acteur identifiable [...] une action ne peut jamais exister
sans origine. »* Ce que ce principe ne couvrait pas encore --- quand un
Acteur cesse d'être valide, et ce qui se passe quand une action requiert
plus d'un Acteur --- est précisé ici.

---

# 2. Principe

Un Acteur précède toujours l'Action qu'il initie, et peut lui survivre.

L'Acteur n'est jamais une propriété de l'Action : c'est l'inverse. Une
Action Instance référence son Acteur (ACT-002-E, section Inputs), elle ne
le contient pas.

---

# 3. Définition

Un Acteur est l'entité dont émane l'Intent à l'origine du pipeline
Intent → Plan → Action → Outcome (ACT-002-F, section 3bis).

Un Acteur n'est pas nécessairement le bénéficiaire de l'Action qu'il
initie --- voir section 8, Auto-ciblage.

---

# 4. Catégories officielles

Reprises d'ACT-001-B, section 2, sans modification :

- un être vivant ;
- une organisation ;
- une intelligence artificielle ;
- un système automatisé ;
- un événement du monde, lorsque celui-ci est explicitement modélisé comme
  acteur.

Ce document ne désigne aucune entité concrète du jeu (personnage, PNJ,
entreprise...) : cette responsabilité appartient à GDB, conformément à
ACT-001-G, section 4. ACT ne fait que garantir que toute entité GDB
prétendant au rôle d'Acteur appartient à l'une de ces catégories.

---

# 5. Éligibilité

Un Acteur potentiel doit satisfaire une éligibilité générale, distincte
et antérieure aux Preconditions propres à une Action donnée
(ACT-002-E, section 5).

L'éligibilité générale répond à une seule question : *cette entité
peut-elle, dans l'absolu, être l'origine d'une action --- indépendamment
de laquelle ?* Les Preconditions répondent à une question différente et
plus étroite : *cette entité peut-elle initier cette Action précise, ici
et maintenant ?*

Un Acteur est éligible si :

✓ il existe encore dans le World au moment de la Validation
(ACT-001-E, étape Validation) ;

✓ il n'est pas explicitement désigné comme incapable d'agir par son
propre état (ex. : un être vivant mort, une organisation dissoute, un
système automatisé désactivé) --- la liste exacte des états
disqualifiants pour chaque catégorie d'Acteur relève de GDB, pas d'ACT ;

✓ il ne fait l'objet d'aucune contrainte de plus haut niveau
l'empêchant explicitement d'agir (ex. : une contrainte juridique, sociale
ou physique documentée par GDB comme Constraint, ACT-002-E section 6).

L'absence d'une de ces trois conditions ne produit pas une Precondition
manquante (qui provoquerait normalement un échec de type « invalidité
interne », ACT-002-F section 8bis) : elle empêche l'Action Instance
d'être créée. Il n'y a alors rien à faire échouer --- l'Action n'a
jamais existé.

---

# 6. Perte d'éligibilité en cours d'exécution

Ce document définit *quand* un Acteur devient inéligible. Ce que le
moteur en fait *pendant* l'exécution d'une Action déjà en cours
appartient exclusivement à ACT-002-F, section 8bis (« Échec de
disparition ») : les Effects déjà produits avant la disparition restent
valides, ceux qui en dépendaient sont annulés.

ACT-004 ne redéfinit pas cette règle --- il ne fait que la référencer,
conformément au principe de responsabilité unique (README du dépôt,
section « Principe de responsabilité unique »).

---

# 7. Multiplicité

Le modèle canonique (ACT-001-D) et le modèle universel (ACT-002) ne
décrivent qu'un seul Acteur par Action Instance. Ce document confirme
ce choix explicitement : **une Action Instance possède exactement un
Acteur.**

Une situation nécessitant plusieurs entités agissant conjointement (un
effort collectif, une action coordonnée) n'est donc jamais modélisée
comme une Action à Acteurs multiples. Elle doit être exprimée comme une
composition de plusieurs Actions à Acteur unique, coordonnées entre
elles --- la responsabilité exacte de cette coordination appartient au
futur chapitre Composition (ACT-009, non encore créé). Tant qu'ACT-009
n'existe pas, aucune règle de coordination inter-Acteurs n'est
disponible ; ACT-004 se limite à garantir que cette absence n'incite pas
à contourner l'invariant d'unicité par une modélisation ad hoc.

---

# 8. Auto-ciblage

ACT-001-B, section 3 (Principe de ciblage), autorise déjà explicitement
qu'une cible soit un acteur. Il s'ensuit qu'un Acteur peut être sa propre
Cible (ex. : une action de soin sur soi-même). ACT-004 confirme cette
possibilité sans la restreindre davantage : les règles précises de
validité d'une Cible, y compris ce cas particulier, appartiennent au
futur ACT-005 (Cibles).

---

# 9. Contrat

Une Action Instance ne peut jamais être créée sans un Acteur identifiable
et éligible au sens de la section 5.

Un Acteur ne peut jamais être introduit après la création de l'Action
Instance : il fait partie de ses Inputs, fixés à la création
(ACT-002-D, Immutabilité).

---

# 10. Contrat TECH

Le moteur doit être capable de :

- vérifier l'existence de l'Acteur référencé avant toute Validation ;
- vérifier son éligibilité générale (section 5) indépendamment des
  Preconditions propres à l'Action ;
- refuser la création d'une Action Instance dont l'Acteur n'est pas
  éligible, sans produire d'échec de type ACT-002-F section 8bis (voir
  section 5, dernier paragraphe) ;
- déléguer à ACT-002-F la gestion d'une disparition d'Acteur survenant
  après la création de l'Action Instance.

---

# 11. Contrat QA

Les tests devront vérifier :

✓ qu'une Action Instance ne peut pas être créée sans Acteur ;

✓ qu'une Action Instance ne peut pas être créée avec un Acteur inéligible ;

✓ qu'un Acteur devenu inéligible après création suit bien le chemin
ACT-002-F section 8bis, jamais un chemin distinct ;

✓ qu'aucune Action Instance ne référence plus d'un Acteur.

---

# 12. Critères de validation

Ce document est conforme si :

✓ il n'introduit aucun axiome déjà posé par ACT-001-B ou ACT-001-H ;

✓ il ne redéfinit aucune règle déjà couverte par ACT-002-E ou ACT-002-F ;

✓ il laisse à GDB la responsabilité de désigner les entités concrètes et
leurs états disqualifiants ;

✓ il laisse à ACT-009 (à créer) la responsabilité de toute coordination
entre plusieurs Acteurs.

---

# 13. Historique

## Version 1.0

- Création du document. Élabore ACT-001-B section 2 et ACT-001-H (entrée
  Acteur) avec des règles d'éligibilité, de perte d'éligibilité et de
  multiplicité absentes des deux documents source. Statut Proposition :
  n'a pas encore traversé les étapes Validée/Spécifiée du cycle de vie
  documentaire d'une mécanique (ACT-001-G, section 14).
