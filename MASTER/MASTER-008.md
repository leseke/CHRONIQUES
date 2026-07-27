# MASTER-008 --- Méthodologie d'Audit et de Correction Documentaire

> Version : 1.1
> Statut : Officiel
> Type : Méthodologie
> Maturité : 1
> Bibliothèque : MASTER

---

# Objectif

Définir la méthode selon laquelle le dépôt Chroniques est audité et corrigé.

Ce document ne décrit pas le contenu des constats eux-mêmes (porté par AUDIT-GLOBALE.md [réf: AUDIT-GLOBALE]), mais la procédure à suivre pour les produire, les traiter et les clore.

---

# 1. Principe général

Une seule source de vérité.

Aucun patch.

Chaque document est régénéré dans son intégralité.

Toute correction doit préserver la cohérence globale du dépôt.

Une correction n'est considérée terminée qu'après fermeture explicite du constat correspondant dans l'audit.

---

# 2. Workflow d'audit

Pour chaque bibliothèque :

1. Lecture complète de la bibliothèque.
2. Analyse documentaire complète.
3. Production uniquement des constats exploitables.
4. Classement par priorité.
5. Ajout à AUDIT-GLOBALE.md.

Aucun correctif pendant la phase d'audit.

---

# 3. Workflow de correction

Pour chaque constat :

1. Sélection d'un unique constat.
2. Analyse de son impact sur l'ensemble du dépôt.
3. Identification de tous les documents concernés.
4. Validation de la liste des documents à modifier.
5. Régénération complète des documents, un par un.
6. Vérification de cohérence globale.
7. Fermeture du constat.
8. Mise à jour d'AUDIT-GLOBALE.md.

---

# 4. Régénération documentaire

Chaque document est toujours :

- entièrement réécrit ;
- jamais modifié par patch ;
- jamais complété par petits ajouts ;
- restructuré si nécessaire ;
- cohérent avec tous les autres documents.

---

# 5. Ordre de travail

Toujours :

Audit → Correction → Validation → Mise à jour de l'audit → Bibliothèque suivante.

Jamais :

- audit complet du projet puis correction globale ;
- correction de plusieurs constats en parallèle sans validation.

---

# 6. Analyse d'un constat

Avant toute correction :

- analyser le constat ;
- déterminer tous les impacts documentaires ;
- identifier les documents à modifier ;
- ne commencer la rédaction qu'après cette analyse.

---

# 7. Règle de régénération

Les documents sont régénérés :

- un document à la fois ;
- dans leur intégralité ;
- dans leur ordre logique ;
- jusqu'à fermeture complète du constat.

---

# 8. Gestion de l'audit général

AUDIT-GLOBALE.md est le document canonique.

Après chaque correction :

- le constat est supprimé s'il est résolu, ou explicitement marqué clos ;
- les statistiques sont recalculées ;
- la progression est mise à jour.

Il n'existe qu'une seule version de l'audit.

---

# 9. Critères de qualité

Une correction est valide uniquement si :

- elle ferme complètement le constat ;
- elle ne crée aucune contradiction ;
- elle respecte la hiérarchie documentaire ;
- elle n'introduit aucune redondance ;
- elle reste compatible avec toutes les bibliothèques.

---

# 10. Méthode de travail permanente

Pour toutes les futures demandes concernant Chroniques :

- appliquer automatiquement cette méthodologie ;
- conserver le même ordre de travail ;
- régénérer les documents complets ;
- traiter un constat à la fois ;
- valider chaque correction avant de passer à la suivante.

Toute exception à cet ordre (par exemple le traitement de plusieurs constats dans une même session, à la demande explicite du porteur du projet) doit être documentée comme telle dans AUDIT-GLOBALE.md, conformément à MASTER-006.

---

# Critère de validation

Avant de modifier cette méthodologie :

Cette évolution réduit-elle un risque réel déjà observé sur le dépôt, ou ajoute-t-elle une étape qui n'a jamais posé problème ?

Si la réponse est la seconde, elle est abandonnée.

---

# Historique

## Version 1.1

- absorption du document autrefois situé hors de toute bibliothèque déclarée, dans un dossier au nom corrompu (« M#U00e9thodologie officielle ») et un fichier au nommage non conforme (« Audit & Correction documentaire Chroniques.md ») ;
- attribution d'un identifiant MASTER-008 et d'un en-tête conforme à MASTER-004 ;
- reformulation en sections numérotées, sans changement de sens.

Corrige les constats MASTER-003-C02 et GLOBAL-C02. Voir [réf: ADR-004] pour la trace de cette décision.

## Version 1.0

- Contenu d'origine, préexistant à l'attribution d'un identifiant MASTER.

---

Fin du document

Statut : Validé --- Référence officielle.
