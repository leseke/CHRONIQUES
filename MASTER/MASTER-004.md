# MASTER-004 --- Conventions de Documentation

> Version : 1.4
> Statut : Officiel
> Type : Convention
> Maturité : 1
> Bibliothèque : MASTER

---

# Objectif

Définir les règles minimales qui maintiennent la documentation cohérente pendant toute la durée du projet.

Ce document est une convention, pas un manuel. Il doit rester court pour être appliqué.

---

# Principe directeur

Une règle n'existe que si elle fait économiser plus d'efforts qu'elle n'en demande.

La gouvernance s'efface derrière le développement. Elle ne doit jamais devenir un projet parallèle.

---

# Autorité documentaire

Chaque sujet possède une source officielle unique.

Les autres documents la référencent, ils ne la recopient pas.

En cas de contradiction entre deux documents, la hiérarchie s'applique :

MASTER fait autorité sur GDB.
GDB fait autorité sur TECH.
TECH fait autorité sur le code.

---

# Nommage

Chaque document porte un identifiant unique composé du dossier, d'un numéro et d'une lettre de section.

Exemples :

- MASTER-004
- GDB-001A
- TECH-002

Les fichiers sont nommés d'après leur identifiant seul, sans le titre.

Exemple : `GDB-001A.md`

Le titre complet figure en première ligne du document.

---

# Casse des fichiers readme

Le readme d'une bibliothèque de premier niveau (MASTER, CORE, GDB, ACT, TECH, QA, UX, LORE, PROD, ART, AUDIO, MKT) s'écrit en minuscule : `readme.md`.

Le readme d'un sous-chapitre GDB (GDB-001, GDB-002, etc.) s'écrit avec une majuscule initiale : `Readme.md`.

Cette distinction lève l'ambiguïté entre les deux niveaux. Elle ne dispense pas de la prudence sur les systèmes de fichiers insensibles à la casse (Windows, macOS par défaut), où deux fichiers ne différant que par la casse entrent en collision silencieuse.

---

# Structure d'un document

Chaque document commence par :

```
IDENTIFIANT --- Titre

> Version : 1.1
> Statut : Officiel
> Type : Principe Fondateur
> Maturité : 1
> Bibliothèque : NOM
```

Le champ **Bibliothèque** indique le dossier racine auquel appartient le document (MASTER, CORE, GDB, ACT, etc.). Il lève toute ambiguïté lorsqu'un identifiant est lu hors de son dossier d'origine.

Cet en-tête est unique et obligatoire pour tout document **créé ou régénéré** à compter de la version 1.2 de la présente convention, MASTER inclus.

Les documents déjà existants à cette date et ne portant pas encore ces deux champs ne sont pas invalidés rétroactivement : ils constituent une dette de migration explicite, suivie dans AUDIT-GLOBALE.md jusqu'à leur régénération complète. Une bibliothèque n'est déclarée conforme à cet en-tête que lorsque 100 % de ses documents le portent --- ce taux doit être vérifiable, jamais supposé.

Puis les sections, séparées par des lignes horizontales.

Chaque document se termine par un critère de validation : une question opposable permettant de juger toute évolution future.

---

# Référence entre documents

Toute citation d'un autre document s'écrit sous la forme :

```
[réf: IDENTIFIANT]
```

Les exemples de cette convention utilisent le mot IDENTIFIANT afin de ne pas être comptés comme des références réelles.

L'index des dépendances est généré automatiquement à partir de ces marqueurs. Il n'est jamais tenu à la main.

---

# Niveaux de maturité

| Niveau | État | Moment |
|--------|------|--------|
| 1 | Fondations | Avant le développement |
| 2 | Spécification | Pendant le prototypage |
| 3 | Implémentation | Pendant la production |
| 4 | Validation | Après les tests |

Le niveau se déclare dans l'en-tête du document.

---

# Versionnement

Chaque document porte un numéro de version composé de deux nombres.

| Changement | Effet | Exemple |
|------------|-------|---------|
| Correction sans effet sur le sens | Aucun | 1.0 reste 1.0 |
| Précision, ajout, reformulation | Version mineure | 1.0 devient 1.1 |
| Modification d'une décision | Version majeure | 1.1 devient 2.0 |

Une version majeure signale que les documents dépendants doivent être vérifiés.

L'historique du dépôt conserve le détail des modifications. Le numéro de version ne sert qu'à signaler leur portée.

Le statut accompagne la version :

- **Officiel** : document en vigueur.
- **À réviser** : document invalidé par un enseignement, en attente de correction.
- **Obsolète** : document remplacé, conservé pour mémoire.

Un document obsolète n'est jamais supprimé. Il indique en tête le document qui le remplace.

---

# Règle de divergence

Toute divergence entre un document de niveau 3 ou 4 et son implémentation ouvre un constat.

Deux issues possibles, jamais choisies par défaut :

- La conception était fausse. Le document est rétrogradé d'un niveau, corrigé, puis revalidé.
- L'implémentation s'est écartée. Le code est corrigé, le document reste inchangé.

L'arbitrage revient au chef de projet. La rétrogradation est tracée par l'historique du dépôt.

---

# Boucle d'évolution

La documentation alimente le développement. Le développement alimente la documentation.

Tout enseignement issu d'un prototype ou d'un test doit produire soit une mise à jour, soit un nouveau document.

Aucun document n'est définitivement figé.

---

# Critère de validation

Avant d'ajouter une règle à ce document :

Cette règle fait-elle économiser plus d'efforts qu'elle n'en demande pour être appliquée ?

Si la réponse est non, elle est abandonnée.

---

# Historique

## Version 1.4

- ajout de la règle de casse des fichiers readme (minuscule pour les bibliothèques de premier niveau, majuscule pour les sous-chapitres GDB), pour clore GLOBAL-C01.

## Version 1.3

- assouplissement de la clause d'obligation de l'en-tête (constat MASTER-004-C03) : elle ne s'applique qu'aux documents créés ou régénérés à compter de la v1.2, et non plus rétroactivement à tout le dépôt ;
- introduction explicite d'une dette de migration pour les documents antérieurs, suivie dans AUDIT-GLOBALE.md plutôt que passée sous silence.

## Version 1.2

- ajout du champ obligatoire `Maturité` à l'en-tête, y compris pour la bibliothèque MASTER elle-même (constat MASTER-C01) ;
- formalisation du champ `Bibliothèque` dans l'en-tête, déjà utilisé de fait par CORE et ACT (constat MASTER-C02) ;
- passage de l'en-tête en forme citée (`>`), alignée sur l'usage déjà majoritaire du dépôt.

## Version 1.1

- Version antérieure, non détaillée rétroactivement.

---

Fin du document

Statut : Validé --- Référence officielle.
