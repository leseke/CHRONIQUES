Méthodologie officielle — Audit & Correction documentaire Chroniques
1. Principe général
Une seule source de vérité.
Aucun patch.
Chaque document est régénéré dans son intégralité.
Toute correction doit préserver la cohérence globale du dépôt.
Une correction n'est considérée terminée qu'après fermeture explicite du constat correspondant dans l'audit.
2. Workflow d'audit

Pour chaque bibliothèque :

Lecture complète de la bibliothèque.
Analyse documentaire complète.
Production uniquement des constats exploitables.
Classement par priorité.
Ajout au AUDIT-GLOBALE.md.
Aucun correctif pendant la phase d'audit.
3. Workflow de correction

Pour chaque constat :

Sélection d'un unique constat.
Analyse de son impact sur l'ensemble du dépôt.
Identification de tous les documents concernés.
Validation de la liste des documents à modifier.
Régénération complète des documents, un par un.
Vérification de cohérence globale.
Fermeture du constat.
Mise à jour du AUDIT-GLOBALE.md.
4. Régénération documentaire

Chaque document est toujours :

entièrement réécrit ;
jamais modifié par patch ;
jamais complété par petits ajouts ;
restructuré si nécessaire ;
cohérent avec tous les autres documents.
5. Ordre de travail

Toujours :

Audit.
Correction.
Validation.
Mise à jour de l'audit.
Bibliothèque suivante.

Jamais :

audit complet du projet puis correction globale ;
correction de plusieurs constats en parallèle sans validation.
6. Analyse d'un constat

Avant toute correction :

analyser le constat ;
déterminer tous les impacts documentaires ;
identifier les documents à modifier ;
ne commencer la rédaction qu'après cette analyse.
7. Règle de régénération

Les documents sont régénérés :

un document à la fois ;
dans leur intégralité ;
dans leur ordre logique ;
jusqu'à fermeture complète du constat.
8. Gestion de l'audit général

AUDIT-GLOBALE.md est le document canonique.

Après chaque correction :

le constat est supprimé s'il est résolu ;
les statistiques sont recalculées ;
la progression est mise à jour.

Il n'existe qu'une seule version de l'audit.

9. Critères de qualité

Une correction est valide uniquement si :

elle ferme complètement le constat ;
elle ne crée aucune contradiction ;
elle respecte la hiérarchie documentaire ;
elle n'introduit aucune redondance ;
elle reste compatible avec toutes les bibliothèques.
10. Méthode de travail permanente

Pour toutes les futures demandes concernant Chroniques :

appliquer automatiquement cette méthodologie ;
conserver le même ordre de travail ;
régénérer les documents complets ;
traiter un constat à la fois ;
valider chaque correction avant de passer à la suivante.
