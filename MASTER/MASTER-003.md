# MASTER-003 --- Architecture Officielle

> Version : 1.3
> Statut : Officiel
> Type : Architecture
> Maturité : 1
> Bibliothèque : MASTER

---

# Objectif

Décrire l'organisation générale du projet Chroniques.

Ce document explique pourquoi cette architecture existe et comment ses grands ensembles s'articulent.

Il ne décrit ni l'architecture logicielle, qui relève de TECH, ni le contenu du jeu, qui relève de la GDB.

---

# Principe d'organisation

Le projet est découpé en bibliothèques documentaires.

Chaque bibliothèque possède un périmètre propre.

Un sujet est traité une seule fois, dans la bibliothèque la plus pertinente. Les autres s'y réfèrent.

Cette règle est la condition de survie du projet : sans elle, chaque modification devrait être répercutée à plusieurs endroits, et la documentation finirait par se contredire.

---

# Les bibliothèques

| Dossier | Rôle |
|---------|------|
| MASTER | Vision, principes, architecture, conventions, roadmap |
| CORE | Concepts primitifs du moteur --- langage universel du projet |
| GDB | Game Design Bible --- spécifications fonctionnelles du jeu |
| ACT | Actions du joueur --- grammaire du gameplay |
| LORE | Univers, chronologie, géographie, cultures |
| TECH | Architecture logicielle, systèmes internes, outils |
| ART | Direction artistique, personnages, environnements |
| AUDIO | Musique, ambiances, sound design |
| UX | Interface, ergonomie, accessibilité, parcours joueur |
| QA | Tests, validation, équilibrage, playtests |
| PROD | Roadmap détaillée, jalons, ressources, planning |
| MKT | Communication, communauté, presse |

Cette liste est la seule liste officielle des bibliothèques du dépôt. Toute bibliothèque mentionnée dans un document antérieur (y compris dans le registre ADR) et absente de ce tableau est considérée retirée ; sa disparition doit être tracée par un ADR [réf: ADR-003].

---

# Le registre des décisions

Les décisions d'architecture sont conservées dans un registre dédié, à la racine du dépôt :

ADR/

Un ADR (Architecture Decision Record) enregistre une décision structurante : son contexte, la décision prise, ses conséquences et les alternatives écartées.

Ce registre est distinct des bibliothèques pour deux raisons :

- un ADR ne relève pas d'un domaine unique --- il peut concerner à la fois le moteur, la production et l'expérience ;

- un ADR est un enregistrement historique : il ne se modifie jamais. Lorsqu'une décision est remplacée, l'ancien ADR est conservé et un nouveau est écrit.

Les feuilles de route et la planification, qui indiquent quand les choses sont faites et évoluent dans le temps, relèvent de PROD. Les ADR, qui indiquent pourquoi une décision a été prise à un instant donné, relèvent du registre ADR.

Règle : le quand appartient à PROD, le pourquoi d'une décision d'architecture appartient à ADR.

Un ADR historique peut faire référence à une bibliothèque depuis retirée (par exemple STANDARDS ou PLN dans ADR-001). Ce n'est pas une erreur à corriger dans l'ADR --- il ne se modifie jamais --- mais un lecteur doit toujours pouvoir retrouver, dans un ADR ultérieur, ce qu'est devenue cette bibliothèque [réf: ADR-003].

---

# Le registre d'audit

Le dépôt contient un second registre, distinct des bibliothèques et du registre ADR, à la racine :

AUDIT/

Il porte le document canonique unique AUDIT-GLOBALE.md, qui recense les constats ouverts sur l'ensemble des bibliothèques, leur priorité et leur statut de correction.

Ce registre est distinct des bibliothèques pour la même raison que le registre ADR : un constat d'audit ne relève pas d'un domaine unique, il peut concerner n'importe quelle bibliothèque. Il diffère du registre ADR par sa nature : l'ADR enregistre des décisions déjà prises, l'audit recense des écarts encore ouverts.

La méthode selon laquelle ce registre est alimenté et corrigé est définie par MASTER-008 [réf: MASTER-008], et non par ce document.

---

# Hiérarchie d'autorité

Les bibliothèques ne sont pas au même niveau.

MASTER fait autorité sur toutes les autres.

CORE fait autorité sur les concepts employés par GDB, ACT et TECH.

GDB fait autorité sur TECH.

TECH fait autorité sur le code.

En cas de contradiction, le document situé le plus haut dans cette hiérarchie l'emporte. Le document inférieur doit être corrigé.

---

# Articulation

Une fonctionnalité traverse le projet dans cet ordre :

1. MASTER en pose la légitimité.
2. CORE en fournit les concepts primitifs.
3. La GDB en définit le comportement attendu, ACT en définit les actions.
4. TECH en décrit l'implémentation.
5. Le code la réalise.
6. QA la valide.

Le retour est tout aussi important : tout enseignement issu du code ou d'un test remonte vers TECH, puis vers la GDB si nécessaire.

La documentation n'est jamais une prescription à sens unique. Elle est une connaissance qui se corrige.

---

# Intention et réalisation

Certains sujets apparaissent à la fois dans la GDB et dans une bibliothèque de production. Ce n'est pas une redondance, à condition de respecter la séparation suivante.

La GDB décrit **l'intention** : à quoi sert cet élément, quel besoin de jeu il satisfait, quelles informations il doit porter.

La bibliothèque de production décrit **la réalisation** : maquettes, composants, palettes, pipelines, formats.

Exemple. La GDB définit pourquoi une interface d'inventaire existe et ce qu'elle doit rendre visible. UX définit ses écrans, ses composants et son comportement tactile.

La même séparation s'applique à AUDIO et à ART.

---

# Structure de la Game Design Bible

La GDB est organisée en chapitres numérotés.

Chaque chapitre est découpé en dix sections de référence, identifiées par une lettre de A à J.

Une section contient un document. Elle peut en contenir plusieurs si le sujet l'exige : la structure fixe les emplacements, elle ne limite pas la profondeur.

Exemples :

- GDB-001A
- GDB-001B
- GDB-002A

La numérotation est volontairement ouverte. De nouveaux chapitres peuvent être ajoutés sans remettre en cause la structure existante.

Lorsqu'une section contient plusieurs documents, le second et les suivants portent un suffixe numérique après la lettre de section : `GDB-001I-2`, `GDB-001I-3`, etc. Ce format s'ajoute au document initial de la section (`GDB-001I`) sans le remplacer, et sans introduire de onzième lettre. Une section ne dépasse jamais la lettre J.

---

# Correspondance entre spécification et code

Chaque document TECH décrivant un système possède une implémentation correspondante dans le code.

Cette correspondance porte le même identifiant, ce qui la rend vérifiable automatiquement.

Un système implémenté sans document, ou un document sans implémentation, constitue un écart à corriger.

---

# Évolutivité

L'architecture ne se modifie plus sans raison. Elle se remplit progressivement.

Une bibliothèque peut être ajoutée si un domaine entier apparaît et n'entre dans aucune des existantes.

Un chapitre peut être ajouté à tout moment.

Une réorganisation d'ensemble doit rester exceptionnelle et être justifiée par écrit, au moyen d'un ADR.

---

# Critère de validation

Avant toute modification de l'architecture :

Ce changement supprime-t-il une ambiguïté réelle, ou déplace-t-il simplement le problème ailleurs ?

Si la réponse est la seconde, il doit être abandonné.

---

# Historique

## Version 1.3

- formalisation du format de nommage pour une section contenant plusieurs documents (`GDB-001I-2`, etc.), jusqu'ici prévu en principe mais jamais concrétisé, découvert lors de la correction de GDB-001-C02.

## Version 1.2

- déclaration officielle du registre AUDIT (AUDIT-GLOBALE.md), jusqu'ici non mentionné par ce document ;
- référence à MASTER-008 pour la méthode d'alimentation de ce registre ;

Corrige (en partie) MASTER-003-C02. Voir [réf: ADR-004].

## Version 1.1

- ajout de la note sur les bibliothèques retirées (STANDARDS, PLN) et référence à ADR-003.

---

Fin du document

Statut : Validé --- Référence officielle.
