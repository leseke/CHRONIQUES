# GDB-001

> Version : 1.1
> Statut : Officiel
> Type : Série
> Maturité : 1
> Bibliothèque : GDB

---

> Les fondations conceptuelles de Chroniques.

---

# Présentation

La série **GDB-001** rassemble les documents qui définissent l'identité fondamentale de Chroniques.

Elle expose la vision du projet, les concepts fondateurs, les principes de conception et le vocabulaire officiel utilisé dans toute la documentation.

Cette série constitue la base sur laquelle reposent toutes les autres séries de la Game Design Bible.

---

# Objectif

La série GDB-001 répond à la question :

> **Qu'est-ce que Chroniques et quels sont les principes qui le définissent ?**

Elle établit le cadre conceptuel commun à l'ensemble du projet.

---

# Relation avec CORE

Les documents de cette série (GDB-001A à GDB-001I) décrivent une **philosophie de conception** : pourquoi le monde, le joueur, le temps ou la lignée existent tels qu'ils sont voulus. Ils ne décrivent jamais leur structure technique.

CORE définit les **primitives structurelles** du moteur (Entity, Component, Value, State, Relation, Event, Time, Space, Lifecycle) [réf: CORE-000C]. Ces deux niveaux se recoupent en surface --- GDB-001E parle du Temps, CORE définit Time ; GDB-001F parle de la Lignée, CORE définit Lifecycle --- sans jamais se contredire, à condition que la frontière suivante soit respectée :

- CORE répond à « de quoi est fait le moteur ? » ;
- GDB-001 répond à « pourquoi le monde doit-il se comporter ainsi ? ».

Aucun document de cette série ne redéfinit une primitive CORE. Lorsqu'un concept de cette série s'appuie sur une primitive du Kernel, il le signale par une référence plutôt que de la redécrire, à l'image de GDB-001J [réf: CORE-000A].

---

# Cette série couvre

- la raison d'être de Chroniques ;
- la définition du monde ;
- le rôle du joueur ;
- la notion de liberté ;
- le fonctionnement du temps ;
- la lignée ;
- la civilisation ;
- les principes des systèmes ;
- les valeurs du studio ;
- l'arbitrage entre ces principes lorsqu'ils entrent en tension ;
- le glossaire officiel.

---

# Cette série ne couvre pas

Cette série ne décrit pas :

- les mécaniques détaillées ;
- les systèmes techniques ;
- les métiers ;
- les personnages ;
- les entreprises ;
- les implémentations du moteur.

---

# Documents

| Document | Sujet |
|-----------|-------|
| GDB-001A | La Raison d'être de Chroniques |
| GDB-001B | Le Monde |
| GDB-001C | Le Joueur |
| GDB-001D | La Liberté |
| GDB-001E | Le Temps |
| GDB-001F | La Lignée |
| GDB-001G | La Civilisation |
| GDB-001H | Les Systèmes |
| GDB-001I | Les Valeurs du Studio |
| GDB-001J | Glossaire Officiel |
| GDB-001I-2 | Arbitrage des Principes Fondateurs |

---

# Relations

Cette série est la référence documentaire de plus haut niveau de la Game Design Bible.

Toutes les autres séries doivent rester cohérentes avec les principes définis ici, et avec leur arbitrage défini en GDB-001K en cas de tension.

---

# Principes

Les documents de cette série doivent :

- définir des concepts durables ;
- rester indépendants de toute implémentation ;
- servir de référence aux autres GDB ;
- éviter toute duplication avec les séries spécialisées ;
- éviter toute duplication avec les primitives CORE.

---

# Évolution

Cette série évolue rarement.

Toute modification doit préserver la vision globale de Chroniques et être compatible avec l'ensemble de la documentation.

Toute tension nouvelle découverte entre deux principes de cette série doit être ajoutée à GDB-001K plutôt que résolue silencieusement ailleurs.

---

# Historique

## Version 1.1

- ajout de la section « Relation avec CORE », précisant la frontière entre philosophie de conception (GDB-001) et primitives structurelles (CORE) ;
- ajout de GDB-001I-2 (Arbitrage des Principes Fondateurs) à la table des documents ;
- en-tête mis en conformité avec MASTER-004.

Corrige les constats GDB-001-C01 et GDB-001-C02.

## Version 1.0

- Création du document.
