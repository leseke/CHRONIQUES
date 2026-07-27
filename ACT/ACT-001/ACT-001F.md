# ACT-001-F — États d'une action

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat
>
> Bibliothèque : ACT
>
> Dépendances :
> - MASTER
> - GDB
> - ACT-001-E
>
> Utilisé par :
> - TECH
> - IA
> - QA
> - UX

---

# 1. Objectif

Définir les états officiels qu'une action peut occuper au cours de son cycle de vie.

Ces états constituent la machine à états de référence utilisée par le moteur de simulation.

---

# 2. Principe

Une action possède toujours un et un seul état courant.

Les changements d'état sont appelés **transitions**.

Chaque transition est validée par le moteur.

---

# 3. États officiels

## CREATED

L'action vient d'être créée.

Aucune validation n'a encore été réalisée.

---

## VALIDATED

Toutes les conditions sont satisfaites.

L'action est autorisée.

---

## PLANNED

L'action est planifiée.

Le moteur connaît son ordre d'exécution.

---

## PREPARED

Les ressources sont réservées.

L'action est prête.

---

## RUNNING

L'action est actuellement exécutée.

Les effets ne sont pas encore appliqués.

---

## SUSPENDED

L'exécution est temporairement arrêtée.

La progression est conservée.

L'action pourra reprendre.

---

## INTERRUPTED

L'action a été stoppée par une cause externe.

La reprise dépend des règles du système.

---

## FAILED

L'action ne peut pas atteindre son objectif.

Les effets éventuels sont limités à ceux prévus par les règles.

---

## SUCCEEDED

L'objectif est atteint.

Les effets sont validés.

---

## RESOLVED

Tous les effets sont calculés.

Le résultat est définitif.

---

## COMMITTED

Les modifications sont appliquées au monde.

Le nouvel état est officiel.

---

## ARCHIVED

L'action est terminée.

Elle est conservée uniquement pour consultation et audit.

---

# 4. États terminaux

Les états suivants sont définitifs :

- FAILED
- ARCHIVED

Une action terminée ne peut jamais revenir dans un état précédent.

---

# 5. États temporaires

Les états suivants peuvent évoluer :

- CREATED
- VALIDATED
- PLANNED
- PREPARED
- RUNNING
- SUSPENDED
- INTERRUPTED
- SUCCEEDED
- RESOLVED
- COMMITTED

---

# 6. Transitions autorisées

CREATED

↓

VALIDATED

↓

PLANNED

↓

PREPARED

↓

RUNNING

↓

SUCCEEDED ou FAILED

↓

RESOLVED

↓

COMMITTED

↓

ARCHIVED

Transitions secondaires :

RUNNING

↓

SUSPENDED

↓

RUNNING

RUNNING

↓

INTERRUPTED

↓

RUNNING

ou

↓

FAILED

---

# 7. Transitions interdites

Exemples :

ARCHIVED → RUNNING

FAILED → RUNNING

COMMITTED → PREPARED

RESOLVED → CREATED

Toute transition non documentée est interdite.

---

# 8. Garanties

Chaque état garantit :

- une signification unique ;
- une traçabilité complète ;
- une validation explicite ;
- une cohérence avec le cycle de vie.

---

# 9. Contrat TECH

Le moteur doit :

- connaître l'état courant ;
- contrôler les transitions ;
- refuser les transitions invalides ;
- enregistrer chaque changement d'état ;
- permettre l'audit complet.

---

# 10. Contrat IA

Les IA peuvent :

- consulter les états ;
- attendre une transition ;
- interrompre une action selon les règles ;
- replanifier une action suspendue.

Les IA ne peuvent jamais modifier directement l'état d'une action.

---

# 11. Contrat QA

Les tests doivent vérifier :

✓ tous les états ;

✓ toutes les transitions autorisées ;

✓ le refus des transitions interdites ;

✓ la conservation de l'historique ;

✓ la cohérence de la machine à états.

---

# 12. Critères de validation

Le document est respecté si :

✓ chaque action possède un état ;

✓ chaque transition est contrôlée ;

✓ aucun état n'est ambigu ;

✓ la machine à états est identique dans tous les systèmes.

---

# 13. Historique

Version 1.0

Création de la machine à états officielle des actions.
