# ACT-001-B — Principes fondamentaux

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

Ce document définit les principes universels régissant toutes les actions de Chroniques.

Ces principes constituent les règles fondamentales du système d'action et s'appliquent sans exception à toutes les mécaniques de gameplay.

Toute nouvelle mécanique doit être compatible avec ces principes.

---

# 2. Principe de responsabilité

Toute action possède un acteur identifiable.

Une action ne peut jamais exister sans origine.

L'acteur peut être :

- un être vivant ;
- une organisation ;
- une intelligence artificielle ;
- un système automatisé ;
- un événement du monde, lorsque celui-ci est explicitement modélisé comme acteur.

---

# 3. Principe de ciblage

Toute action possède au moins une cible.

Une cible peut être :

- un acteur ;
- un objet ;
- une ressource ;
- un lieu ;
- une organisation ;
- une information ;
- le monde lui-même.

Certaines actions peuvent posséder plusieurs cibles.

---

# 4. Principe de contexte

Aucune action n'est indépendante de son contexte.

Le contexte influence notamment :

- la disponibilité de l'action ;
- sa probabilité de réussite ;
- son coût ;
- sa durée ;
- ses conséquences.

---

# 5. Principe de conditions

Une action n'est exécutable que si l'ensemble de ses conditions est satisfait.

Les conditions peuvent être :

- matérielles ;
- sociales ;
- économiques ;
- juridiques ;
- environnementales ;
- temporelles ;
- physiologiques ;
- psychologiques.

---

# 6. Principe de conséquence

Toute action modifie l'état du monde.

Même un échec peut produire des conséquences.

Aucune action n'est totalement neutre.

---

# 7. Principe de causalité

Chaque conséquence possède une origine identifiable.

Le moteur doit être capable d'expliquer pourquoi un état du monde a changé.

Ce principe garantit la traçabilité des événements.

---

# 8. Principe de temporalité

Toute action possède une dimension temporelle.

Une action peut être :

- instantanée ;
- progressive ;
- différée ;
- continue ;
- périodique.

---

# 9. Principe de composition

Les actions peuvent être combinées pour produire des comportements plus complexes.

Une action complexe est toujours composée d'actions plus simples.

Les mécaniques doivent privilégier la composition plutôt que la duplication.

---

# 10. Principe de réutilisation

Une même mécanique doit pouvoir être utilisée dans plusieurs contextes.

Le système favorise les composants génériques plutôt que les solutions spécialisées.

---

# 11. Principe de cohérence

Deux situations identiques doivent produire des résultats cohérents, sous réserve des éléments variables du contexte.

Le moteur ne doit jamais produire de comportement arbitraire.

---

# 12. Principe d'évolutivité

Toute nouvelle mécanique doit pouvoir être ajoutée sans remettre en cause les principes définis dans ce document.

Les extensions enrichissent le système ; elles ne le contredisent pas.

---

# 13. Principe de traçabilité

Toute action doit pouvoir être reliée à :

- son acteur ;
- sa cible ;
- ses conditions ;
- son déroulement ;
- ses conséquences ;
- les systèmes techniques qui l'implémentent ;
- les tests qui la valident.

---

# 14. Impact technique

Ces principes constituent les contraintes de conception de tous les modules TECH liés au gameplay.

Aucun module ne peut les contourner sans décision d'architecture documentée.

---

# 15. Impact QA

Les tests devront vérifier notamment :

- le respect des conditions ;
- la cohérence des conséquences ;
- la traçabilité des événements ;
- la stabilité des comportements ;
- la conformité aux principes définis dans ce document.

---

# 16. Critères de validation

Ce document est considéré comme respecté si :

✓ Toute action possède un acteur.

✓ Toute action possède une cible.

✓ Toute action possède des conditions.

✓ Toute action produit des conséquences.

✓ Toute conséquence est explicable.

✓ Toute mécanique respecte ces principes.

---

# 17. Historique

Version 1.0 — Création des principes fondateurs du système d'action de Chroniques.
