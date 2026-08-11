# MASTER-006 --- Gouvernance des Décisions

> Version : 1.1
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
| Structurante | Vision, principes, architecture, gouvernance | Document MASTER modifié |
| De conception | Comportement d'un système | Document GDB ou ACT créé/modifié |
| D'architecture moteur | Contrat attendu du moteur | Document ENGINE créé/modifié |
| Technique | Implémentation réellement obtenue | Document TECH créé/modifié au point de consolidation applicable |
| Courante | Détail sans conséquence durable | Aucune |

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

Une décision adoptée est inscrite dans le document compétent dès qu'elle devient une autorité applicable au travail courant.

Tant qu'une règle structurante ou métier adoptée n'est pas inscrite, elle n'est pas prise.

Cette inscription immédiate ne signifie pas que tous les documents transverses du projet doivent être régénérés après chaque petit changement.

---

# Validation courante et consolidation documentaire

Chroniques distingue explicitement deux opérations.

```text
VALIDATION COURANTE
≠
CONSOLIDATION DOCUMENTAIRE
```

## Validation courante

Une validation courante confirme un incrément cohérent et directement vérifiable.

Elle met à jour immédiatement les sources de vérité directement concernées :

```text
règle ou contrat d'autorité concerné
+
code concerné
+
tests concernés
+
statut/catalogue local nécessaire à la traçabilité
```

Exemples :

- une GDB précisée pour autoriser une nouvelle mécanique ;
- un Pattern ou un Verbe ACT validé ;
- un document ENGINE passant de Proposition à Validée après réussite des tests ;
- le catalogue de la bibliothèque concernée synchronisé avec ce statut.

Une validation courante ne déclenche pas automatiquement la régénération de TECH, des README, de la roadmap ou des synthèses d'audit globales.

## Consolidation documentaire

Une consolidation documentaire remet en cohérence les documents transverses après un jalon significatif.

Elle est déclenchée par un événement, non par un nombre arbitraire de modifications.

Les déclencheurs normaux sont notamment :

- fermeture d'une bibliothèque ou d'un sous-ensemble documentaire cohérent ;
- jalon important de roadmap ;
- capacité fonctionnelle majeure obtenue de bout en bout ;
- fin d'un bloc architectural cohérent ;
- changement de phase ou de version ;
- audit ou correction critique nécessitant une remise en concordance immédiate.

À ce point, le contrôle porte selon le périmètre sur :

```text
sources d'autorité concernées
↓
ENGINE / GDB / ACT applicables
↓
implémentation + tests
↓
TECH
↓
AUDIT
↓
CATALOGUES
↓
roadmap
↓
README documentaires et moteur
```

Tous ces niveaux ne sont modifiés que s'ils sont réellement concernés par le jalon.

La consolidation ne doit jamais servir de prétexte à modifier des documents sans impact réel.

## Règle de seuil

Le seuil principal est donc qualitatif :

```text
le projet vient-il d'obtenir ou de fermer quelque chose que les documents transverses doivent désormais raconter ?
```

Si oui, consolidation.

Si non, validation courante et poursuite du développement.

Un garde-fou numérique peut être utilisé pour éviter une accumulation excessive de dette documentaire, mais il ne remplace jamais ce critère événementiel.

## Exception critique

Une contradiction d'autorité, un invariant faux, un statut trompeur ou une divergence susceptible d'orienter le développement dans une mauvaise direction est corrigé immédiatement, même hors point de consolidation.

La réduction du bruit documentaire ne doit jamais se faire au prix d'une source de vérité fausse.

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

Avant de déclencher une consolidation documentaire :

Le jalon modifie-t-il réellement ce que les documents transverses doivent raconter sur l'état du projet ?

Si la réponse applicable est non, l'opération n'est pas terminée ou la consolidation n'est pas justifiée.

---

# Historique

## Version 1.1

- distinction officielle entre validation courante et consolidation documentaire ;
- adoption d'un seuil de consolidation événementiel plutôt que d'une mise à jour transverse après chaque modification ;
- définition des déclencheurs : fermeture de bibliothèque/sous-ensemble, jalon de roadmap, capacité majeure, fin de bloc architectural, changement de phase/version ou audit critique ;
- maintien d'une exception immédiate pour toute contradiction d'autorité ou invariant trompeur ;
- clarification que TECH, README, roadmap et audit global ne sont pas régénérés automatiquement après chaque incrément validé.

## Version 1.0

- création du document.

---

Fin du document

Statut : Validé --- Référence officielle.
