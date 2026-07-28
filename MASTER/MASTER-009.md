# MASTER-009 --- Contraintes du Projet

> Version : 1.0
> Statut : Officiel
> Type : Contraintes
> Maturité : 1
> Bibliothèque : MASTER

---

# Objectif

Définir les contraintes plateforme, techniques, commerciales et légales
auxquelles toute proposition de conception doit se conformer.

Ce document ne redéfinit ni la vision (MASTER-001), ni les principes de
conception (MASTER-002) : une excellente idée de gameplay qui viole une
contrainte de ce document n'est pas une bonne décision, mais son évaluation
sur le fond continue de relever de MASTER-002.

---

# Plateforme cible

Chroniques est conçu pour smartphone, en priorité :

- iOS ;
- Android.

Le mode **portrait** est prioritaire. Toute interface, mécanique ou
interaction doit être pensée pour une utilisation **tactile** en mode
portrait --- pas comme une adaptation a posteriori d'une interface pensée
pour un écran plus grand.

---

# Performance

Le jeu doit fonctionner correctement sur des smartphones récents, sans
exiger un appareil haut de gamme.

Chaque système doit avoir un coût raisonnable en :

- mémoire ;
- processeur ;
- stockage ;
- batterie.

Une fonctionnalité ne doit jamais compromettre les performances globales du
jeu. L'optimisation fait partie de la conception, pas d'une passe séparée
après coup.

---

# UX

Le joueur doit comprendre naturellement ce qu'il peut faire, sans avoir
besoin de consulter un manuel. La complexité doit être progressive.

Cela implique de limiter :

- les menus complexes ;
- les actions répétitives ou artificiellement longues ;
- les informations inutiles.

Chaque interaction doit avoir une utilité --- ce qui précise, pour la
bibliothèque UX, la manière dont le Principe 6 de MASTER-002 (progression
organique) doit se traduire à l'écran.

---

# Équilibrage

Aucun mode de vie ne doit être la seule stratégie optimale. Toutes les
trajectoires doivent pouvoir être intéressantes.

Le jeu récompense les décisions cohérentes plutôt qu'un style de jeu
imposé --- application directe du Principe 1 de MASTER-002 (le joueur est
libre) au niveau de l'équilibrage.

---

# Publication

Toute proposition doit rester compatible avec la publication sur l'App
Store et le Google Play Store, et respecter les politiques de publication
en vigueur sur ces plateformes.

Une fonctionnalité incompatible avec ces politiques n'est pas une bonne
solution, quelle que soit sa qualité par ailleurs.

---

# Légalité

Toute fonctionnalité doit éviter de poser un problème juridique,
notamment au regard :

- de la propriété intellectuelle ;
- des données personnelles ;
- des réglementations applicables sur les territoires visés.

---

# Monétisation

La monétisation, quelle que soit sa forme future, doit être :

- transparente ;
- éthique ;
- non intrusive.

Elle ne doit jamais dégrader volontairement l'expérience de jeu pour
inciter à la dépense. Une mécanique de jeu ne doit jamais être conçue
d'abord pour servir la monétisation, et seulement ensuite pour servir le
joueur.

---

# Ce que ce document ne couvre pas

- Les systèmes de jeu prioritaires (contenu vs systèmes, réutilisation,
  modularité, évolutivité) : voir MASTER-002.
- Le choix du moteur et du langage : voir ADR-002.
- La méthode de travail documentaire : voir MASTER-008.

---

# Critère de validation

Avant de valider une proposition de conception :

Cette proposition reste-t-elle jouable et confortable en une main, sur un
écran de smartphone en mode portrait, sans dégrader les performances ni
compromettre la publication sur les stores ?

Si la réponse est non, elle doit être revue avant d'être retenue.

---

# Historique

## Version 1.0

- Création du document, à partir des contraintes déjà en usage dans les
  sessions de travail avec les IA (dépôt `Prompt`, `02_CONSTRAINTS.md`),
  officialisées ici pour qu'elles fassent partie du dépôt de documentation
  plutôt que de rester dans un document externe non versionné avec le
  reste du projet. La contrainte « développeur solo » présente dans la
  source d'origine n'a pas été reprise : elle a été explicitement écartée
  par le porteur du projet. Voir [réf: ADR-005].

---

Fin du document

Statut : Validé --- Référence officielle.
