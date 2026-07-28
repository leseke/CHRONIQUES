# ACT-001-E — Cycle de vie d'une action

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
>
> Utilisé par :
> - TECH
> - IA
> - QA
> - UX

---

# 1. Objectif

Définir le cycle de vie officiel de toute action dans Chroniques.

Toute action suit ce cycle, quel que soit son type, son contexte ou son auteur.

Ce cycle garantit un comportement homogène, prévisible et traçable.

---

# 2. Principe

Une action ne passe jamais directement de sa création à son résultat.

Elle traverse une succession d'états contrôlés.

Chaque transition est validée par le moteur.

---

# 3. Machine à états

```
Création
    │
    ▼
Validation
    │
    ▼
Planification
    │
    ▼
Préparation
    │
    ▼
Exécution
    │
    ▼
Résolution
    │
    ▼
Production des effets
    │
    ▼
Publication des événements
    │
    ▼
Mise à jour du monde
    │
    ▼
Archivage
```

Aucune transition ne peut être ignorée sans justification documentée.

---

# 4. Description des états

## Création

L'action est instanciée.

Aucun effet n'est encore produit.

---

## Validation

Le moteur vérifie :

- les conditions ;
- les autorisations ;
- les ressources ;
- les dépendances.

En cas d'échec, l'action est refusée.

---

## Planification

Le moteur détermine :

- l'ordre d'exécution ;
- les conflits éventuels ;
- les priorités ;
- les attentes.

---

## Préparation

Les ressources sont réservées.

Les acteurs concernés sont notifiés.

Les préconditions finales sont contrôlées.

---

## Exécution

L'action est exécutée.

Elle peut :

- réussir ;
- échouer ;
- être interrompue ;
- être suspendue.

---

## Résolution

Le moteur calcule le résultat réel.

Il détermine :

- le niveau de réussite ;
- les pertes ;
- les gains ;
- les conséquences immédiates.

---

## Production des effets

Les effets sont générés.

Ils restent indépendants de l'état du monde.

---

## Publication des événements

Les effets produisent des événements.

Ces événements sont transmis aux systèmes abonnés.

Exemples :

- IA
- Journal
- Interface
- Quêtes
- Succès
- Statistiques
- Audio
- Animation

---

## Mise à jour du monde

Le moteur applique les effets validés.

Le nouvel état devient officiel.

---

## Archivage

Toutes les informations sont enregistrées.

L'action devient consultable dans l'historique.

---

# 5. Interruptions

Une action peut être interrompue :

- volontairement ;
- automatiquement ;
- par une autre action ;
- par le contexte.

Une interruption est elle-même journalisée.

---

# 6. Suspension

Certaines actions peuvent être suspendues.

Une suspension conserve :

- la progression ;
- les ressources réservées ;
- le contexte.

Une action suspendue peut reprendre ultérieurement.

---

# 7. Annulation

Une action peut être annulée uniquement avant la production des effets.

Après cette étape, seules des actions compensatoires peuvent corriger les conséquences.

---

# 8. Garanties

Le cycle garantit :

✓ cohérence

✓ traçabilité

✓ reproductibilité

✓ auditabilité

✓ débogage

✓ simulation déterministe (si le contexte est identique)

---

# 9. Contrat TECH

Le moteur doit être capable de :

- créer ;
- valider ;
- planifier ;
- préparer ;
- exécuter ;
- suspendre ;
- reprendre ;
- interrompre ;
- résoudre ;
- publier les événements ;
- appliquer les effets ;
- archiver.

Aucune implémentation ne peut supprimer une étape obligatoire.

---

# 10. Contrat IA

Les IA peuvent :

- préparer plusieurs actions ;
- abandonner une action ;
- replanifier une action ;
- réagir aux interruptions ;
- apprendre des résultats.

---

# 11. Contrat QA

Les tests devront vérifier :

✓ toutes les transitions d'état ;

✓ les interruptions ;

✓ les suspensions ;

✓ les annulations ;

✓ la publication des événements ;

✓ la mise à jour correcte du monde.

---

# 12. Critères de validation

Le cycle est conforme si :

✓ toutes les actions suivent cette machine à états ;

✓ chaque transition est contrôlée ;

✓ les effets précèdent toujours les événements ;

✓ les événements précèdent toujours la modification du monde.

---

# 13. Historique

Version 1.0

Création du cycle de vie officiel des actions de Chroniques.
