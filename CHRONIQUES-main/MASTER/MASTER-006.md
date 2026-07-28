# MASTER-006 --- Gouvernance des Décisions

> Version : 1.0
> Statut : Officiel
> Type : Gouvernance
> Maturité : 1
> Bibliothèque : MASTER

---

# Objectif

Définir comment une décision est proposée, tranchée, inscrite ou abandonnée.

Ce document ne traite pas du contenu des décisions, mais de leur circulation.

---

# Le problème que ce document résout

Les décisions du projet naissent dans des conversations.

Une conversation ne conserve rien. Elle se referme, se perd, ou n'est plus retrouvable.

Une décision qui n'a pas été inscrite dans un document n'existe pas.

Elle sera reprise, contredite, ou réinventée différemment quelques semaines plus tard.

---

# Nature des décisions

| Type | Portée | Trace |
|------|--------|-------|
| Structurante | Vision, principes, architecture | Document MASTER modifié |
| De conception | Comportement d'un système | Document GDB créé ou modifié |
| Technique | Implémentation | Document TECH créé ou modifié |
| Courante | Détail sans conséquence | Aucune |

Une décision courante n'est pas documentée. Le coût d'écriture dépasserait le bénéfice.

Le doute se tranche en faveur de l'écriture : une décision inutilement inscrite ne coûte que quelques lignes, une décision perdue coûte une contradiction.

---

# Cycle d'une décision

## 1. Proposition

Une proposition énonce le problème avant la solution.

Une proposition sans problème identifié est une préférence, non une décision à prendre.

## 2. Examen

La proposition est confrontée aux documents existants.

Trois questions suffisent :

- Contredit-elle un document de rang supérieur ?
- Duplique-t-elle un sujet déjà traité ailleurs ?
- Répond-elle au critère de validation du document concerné ?

## 3. Arbitrage

Le chef de projet tranche.

Une décision peut être : adoptée, adoptée sous condition, ajournée, ou rejetée.

## 4. Inscription

Une décision adoptée est immédiatement inscrite dans le document compétent.

Tant qu'elle n'est pas inscrite, elle n'est pas prise.

---

# Modifier ou créer

Une décision qui précise un sujet existant modifie le document existant.

Une décision qui ouvre un sujet nouveau crée un document.

Un sujet est nouveau lorsqu'il possède son propre critère de validation. Dans le cas contraire, il appartient à un document existant.

Cette règle protège contre la multiplication des documents, qui est le principal risque d'une documentation abondante.

---

# Décisions rejetées

Une décision rejetée pour une raison de fond est conservée.

Elle est inscrite dans le document concerné sous la forme d'une ligne indiquant ce qui a été écarté et pourquoi.

Sans cette trace, la même proposition reviendra, et le même débat sera rejoué.

---

# Décisions ajournées

Une décision peut être ajournée lorsqu'elle dépend d'un enseignement que le projet n'a pas encore.

Elle est alors rattachée à la phase qui produira cet enseignement.

Aucune décision ne doit être ajournée sans condition de reprise.

---

# Rôle des contributeurs externes

Le projet fait appel à des contributeurs qui n'ont pas de mémoire du projet entre deux échanges.

Toute décision doit donc être compréhensible à partir du dépôt seul, sans connaissance des conversations qui l'ont précédée.

Un document qui suppose un contexte extérieur est incomplet.

Cette exigence s'applique aussi aux évolutions du dépôt lui-même : lorsqu'une bibliothèque ou un concept disparaît de la documentation en vigueur, sa disparition doit être tracée par un document, jamais laissée à la seule mémoire d'une conversation passée [réf: ADR-003].

---

# Critère de validation

Avant de considérer une décision comme prise :

Un contributeur qui n'a jamais participé à cette discussion pourrait-il retrouver cette décision et sa raison dans le dépôt ?

Si la réponse est non, la décision n'est pas prise.

---

Fin du document

Statut : Validé --- Référence officielle.
