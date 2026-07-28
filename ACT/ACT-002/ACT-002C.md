# ACT-002-C — Relations entre les niveaux

> Version : 1.1
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Maturité : 2
>
> Bibliothèque : ACT

---

# 1. Objectif

Définir les relations autorisées entre les niveaux d'abstraction du modèle universel des actions.

Ce document garantit que chaque niveau s'appuie sur le précédent sans créer de dépendances circulaires.

---

# 2. Principe

Les niveaux ne sont pas indépendants.

Ils forment une chaîne de spécialisation.

Chaque niveau apporte davantage d'information sans modifier le sens du niveau supérieur.

---

# 3. Relations autorisées

Les relations officielles sont :

- spécialisation ;
- instanciation ;
- composition ;
- référence.

Toute autre relation est interdite.

---

# 4. Spécialisation

La spécialisation consiste à enrichir progressivement un concept.

Exemple :

Principe : Déplacement

↓

Pattern : Déplacement terrestre

↓

Verbe : Marcher

↓

Action : « Alice marche jusqu'au marché. »

Le sens est conservé à chaque étape.

---

# 5. Instanciation

L'instanciation transforme un modèle abstrait en événement concret.

Le Verbe décrit une capacité.

L'Action représente son exécution dans un contexte donné.

---

# 6. Composition

Une Action peut être composée de plusieurs Actions.

Exemple :

Construire une maison

↓

Transporter des matériaux

↓

Assembler les fondations

↓

Monter les murs

↓

Installer la toiture

Chaque sous-action reste autonome tout en participant à l'objectif global.

---

# 6bis. Frontière entre Action et Interaction

Une Action possède un Acteur et une ou plusieurs Cibles [réf: ACT-001-B]. Une
Cible peut être passive (un objet, une ressource, un lieu) ou active (un
autre Acteur).

Une **Interaction** est le cas particulier où une Action cible un Acteur
capable de produire, en retour et dans le même événement causal, sa propre
Action en réponse. « Convaincre », « négocier » ou « attaquer » sont des
Interactions : leur Outcome [réf: ACT-002-G] dépend d'une résolution qui
prend en compte la réaction de la Cible, jamais seulement l'intention de
l'Acteur initial. « Cueillir » ou « construire » ne sont jamais des
Interactions : leur Cible ne produit aucune réponse.

Une Interaction n'est donc pas un niveau supplémentaire du modèle --- elle
reste une Action au sens de ce document, avec une seule particularité : sa
résolution [réf: ACT-002-G] intègre la réaction de la Cible comme une entrée
du calcul de l'Outcome, en plus du Contexte et des Conditions.

---

# 7. Référence

Une Action peut référencer :

- des entités (GDB) ;
- des ressources ;
- des lieux ;
- des organisations ;
- des règles.

Elle ne les définit jamais.

---

# 8. Relations interdites

Un Principe ne dépend jamais d'un Verbe.

Un Pattern ne dépend jamais d'une Action.

Une Action ne modifie jamais son Pattern.

Les dépendances remontantes sont interdites.

---

# 9. Traçabilité

Toute Action doit permettre de retrouver :

Action

↓

Verbe

↓

Pattern

↓

Principe

Cette chaîne doit être complète et non ambiguë.

---

# 10. Contrat

Aucune relation ne peut créer une dépendance circulaire entre deux niveaux.

---

# 11. Validation

Le document est conforme si :

✓ les relations sont orientées ;

✓ aucune boucle conceptuelle n'existe ;

✓ chaque niveau reste indépendant.

---

# 12. Historique

Version 1.1 : ajout de la frontière entre Action et Interaction (section 6bis).
Corrige ACT-002-C02. En-tête mis en conformité avec MASTER-004.

Version 1.0

Première définition officielle des relations entre les niveaux d'abstraction.
