# ACT-001-C — Définition universelle de l'action

> Version : 1.0
>
> Statut : Fondation
>
> Bibliothèque : ACT
>
> Références :
> - MASTER
> - GDB
> - TECH
> - QA

---

# 1. Objectif

Définir le modèle universel d'une action.

Cette définition constitue la référence officielle utilisée par toutes les bibliothèques de Chroniques.

Aucune mécanique ne peut utiliser une définition différente.

---

# 2. Définition

Une action est une **tentative initiée par un acteur, exécutée dans un contexte donné, visant à produire un ou plusieurs effets sur le monde ou sur ses occupants.**

Une action ne garantit jamais un résultat.

Elle représente une intention soumise à des règles de simulation.

---

# 3. Caractéristiques

Toute action possède obligatoirement :

- un identifiant unique ;
- un acteur ;
- une ou plusieurs cibles ;
- un contexte ;
- un objectif ;
- des conditions ;
- une durée ;
- un coût éventuel ;
- un niveau de risque ;
- un état courant.

---

# 4. Cycle conceptuel

Toute action suit le modèle suivant :

Intention

↓

Validation

↓

Préparation

↓

Exécution

↓

Production d'effets

↓

Génération d'événements

↓

Modification de l'état du monde

↓

Archivage

---

# 5. Intention

Toute action naît d'une intention.

Une intention peut provenir :

- d'un joueur ;
- d'un PNJ ;
- d'une organisation ;
- d'un système automatique ;
- d'un événement.

L'intention est distincte de l'action elle-même.

---

# 6. Effets

Une action produit un ou plusieurs effets.

Les effets décrivent les changements directs générés par l'action.

Exemples :

- modification d'une valeur ;
- déplacement ;
- création ;
- destruction ;
- transfert ;
- influence ;
- acquisition ;
- perte.

Les effets ne modifient pas directement le monde.

Ils sont transmis au moteur de simulation.

---

# 7. Événements

Les effets produisent des événements.

Les événements servent notamment à :

- informer les autres systèmes ;
- déclencher des réactions ;
- alimenter les journaux ;
- notifier l'interface ;
- mettre à jour les statistiques.

Une même action peut produire plusieurs événements.

---

# 8. Monde

Le monde est modifié uniquement après la résolution des événements.

Cette séparation garantit :

- la cohérence ;
- la traçabilité ;
- la reproductibilité des simulations ;
- la possibilité de rejouer une simulation.

---

# 9. Composition

Une action peut être :

- élémentaire ;
- composée.

Une action composée est constituée de plusieurs actions élémentaires coordonnées.

Exemple :

Construire une maison

↓

Acheter

↓

Transporter

↓

Assembler

↓

Contrôler

↓

Valider

---

# 10. Neutralité

Une action n'est jamais liée :

- à un métier ;
- à une époque ;
- à une civilisation ;
- à une faction.

Ces éléments appartiennent au contexte.

L'action reste universelle.

---

# 11. Propriétés

Chaque action possède notamment :

- disponibilité ;
- priorité ;
- visibilité ;
- interruption ;
- répétition ;
- exclusivité ;
- dépendances ;
- historique.

Ces propriétés sont communes à toutes les actions.

---

# 12. Contraintes

Une action ne peut jamais :

- contourner les règles ACT ;
- modifier directement le monde ;
- ignorer ses conditions ;
- produire un état incohérent.

---

# 13. Impact technique

TECH devra représenter chaque action comme une entité autonome.

Les modules techniques manipuleront des actions, jamais directement les états du monde.

---

# 14. Impact IA

Les IA :

- planifient des actions ;
- évaluent leur coût ;
- estiment leurs chances de réussite ;
- exécutent ces actions ;
- analysent leurs conséquences.

L'IA ne manipule jamais directement le monde.

---

# 15. Impact QA

Les tests devront vérifier :

✓ la validité des actions ;

✓ leur cycle de vie ;

✓ leurs effets ;

✓ les événements produits ;

✓ la cohérence des modifications du monde.

---

# 16. Critères de validation

Ce document est respecté si :

✓ toutes les actions suivent ce modèle ;

✓ toutes les simulations utilisent ce cycle ;

✓ aucune mécanique ne contourne cette définition.

---

# 17. Historique

Version 1.0 — Définition officielle du modèle universel de l'action.
