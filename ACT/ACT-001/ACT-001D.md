# ACT-001-D — Modèle canonique d'une action

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

Définir la structure officielle utilisée pour représenter toute action dans Chroniques.

Cette structure constitue le contrat de référence entre le gameplay et le moteur.

Toute action implémentée dans TECH devra respecter ce modèle.

---

# 2. Principe

Une action est un objet autonome.

Elle possède toutes les informations nécessaires à son exécution.

Elle ne dépend jamais d'un métier, d'une civilisation ou d'un système particulier.

---

# 3. Structure canonique

Toute action est composée des éléments suivants :

## Identité

- Identifiant unique
- Nom
- Verbe
- Pattern
- Version

---

## Origine

- Acteur initiateur
- Intention
- Déclencheur
- Priorité

---

## Contexte

- Date
- Heure
- Lieu
- Conditions environnementales
- Conditions sociales
- Conditions juridiques
- Conditions économiques

---

## Cibles

Une ou plusieurs cibles.

Chaque cible possède :

- type
- rôle
- état
- accessibilité

---

## Ressources

L'action peut nécessiter :

- temps
- énergie
- argent
- objets
- compétences
- connaissances
- autorisations

---

## Contraintes

Conditions obligatoires.

Conditions optionnelles.

Interdictions.

Dépendances.

Verrous.

---

## Déroulement

Le déroulement est découpé en étapes.

Chaque étape possède :

- objectif
- durée
- coût
- risques
- effets possibles

---

## Effets

Chaque effet possède :

- catégorie
- intensité
- portée
- durée
- probabilité

Les effets sont indépendants du monde.

---

## Événements

Chaque effet peut produire plusieurs événements.

Les événements sont destinés aux autres systèmes.

---

## Résolution

Résultat :

- réussite
- réussite partielle
- échec
- interruption
- annulation

---

## Conséquences

Conséquences immédiates.

Conséquences différées.

Conséquences permanentes.

Conséquences temporaires.

---

## Historique

Journal complet.

Traçabilité.

Références.

---

# 4. Garanties

Une action garantit :

✓ sa traçabilité

✓ sa reproductibilité

✓ sa sérialisation

✓ son audit

✓ son historique

---

# 5. Contraintes

Une action ne doit jamais :

- modifier directement le monde ;
- ignorer ses conditions ;
- contourner son cycle de vie ;
- produire un état invalide.

---

# 6. Contrat TECH

Le moteur doit être capable de :

- créer une action ;
- valider une action ;
- exécuter une action ;
- suspendre une action ;
- reprendre une action ;
- interrompre une action ;
- annuler une action ;
- archiver une action.

Ces capacités sont obligatoires.

---

# 7. Contrat IA

Les IA doivent pouvoir :

- générer des intentions ;
- sélectionner une action ;
- estimer son coût ;
- prévoir son risque ;
- lancer son exécution ;
- analyser son résultat.

---

# 8. Contrat QA

Les tests devront vérifier :

✓ la validité du modèle ;

✓ les transitions d'état ;

✓ la cohérence des effets ;

✓ la production d'événements ;

✓ les conséquences ;

✓ la journalisation.

---

# 9. Traçabilité

Chaque action doit pouvoir être reliée à :

MASTER

↓

GDB

↓

ACT

↓

TECH

↓

QA

---

# 10. Critères de validation

Le modèle est valide si :

✓ toutes les actions utilisent cette structure ;

✓ aucun système ne définit son propre modèle ;

✓ toutes les implémentations TECH utilisent ce contrat.

---

# 11. Historique

Version 1.0

Création du contrat canonique des actions.
