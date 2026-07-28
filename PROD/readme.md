# PROD

> Version : 1.0
> Statut : Fondation
> Type : Bibliothèque
> Maturité : 1
> Bibliothèque : PROD

---

## Rôle

Le dossier **PROD** regroupe toute la documentation liée à la gestion et au pilotage du développement de Chroniques.

Il permet de planifier, suivre et organiser l'ensemble de la production du jeu, depuis les premières phases de conception jusqu'à la publication des différentes versions.

---

## Objectifs

- Planifier le développement.
- Définir les priorités.
- Suivre l'avancement du projet.
- Organiser les livrables.
- Préparer les versions et les sorties.

---

## Contenu prévu

- Roadmap
- Planning
- Milestones
- Sprints
- Backlog
- Changelog
- Releases
- Journal de développement
- Gestion des risques

---

## État actuel

Un seul document réel existe à ce jour : `FeuilleDeRoute.md`. Il ne suit pas encore la convention de nommage ci-dessous (il n'est pas un `PROD-00X`) car il préexistait à la formalisation de cette convention ; son renommage éventuel devra faire l'objet d'une décision explicite plutôt que d'un renommage silencieux.

Le suivi du backlog de correction documentaire (constats, priorités, statistiques) ne relève pas de PROD malgré la mention « Backlog » ci-dessus : il est porté par `AUDIT-GLOBALE.md`, dans le dossier AUDIT. La frontière exacte entre les deux reste à documenter [réf: MASTER-003].

---

## Convention

Chaque nouveau document est identifié par un numéro unique.

Exemples (à créer) :

- PROD-001
- PROD-002
- PROD-003

---

## Dépendances

Le contenu du dossier PROD s'appuie sur les documents MASTER, GDB, TECH et QA afin d'assurer un suivi cohérent de l'ensemble du projet.

Les choix techniques structurants ne sont pas répétés ici : ils sont actés dans le registre ADR et seulement référencés [réf: ADR-002].

---

## Évolution

Le dossier PROD est mis à jour tout au long du développement afin de refléter l'état réel du projet, les décisions prises et l'avancement des différentes phases de production.

---

# Historique

## Version 1.0

- création avec en-tête conforme à MASTER-004 ;
- séparateurs corrigés (`---` au lieu de `—`) ;
- clarification du statut réel de FeuilleDeRoute.md et de la frontière avec AUDIT.

Corrige les constats STUB-C02, STUB-C03, et précise MASTER-003-C02.
