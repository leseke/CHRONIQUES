# GDB-004A — Les Habitants du Monde

> Version : 1.1
> Statut : Officiel
> Type : Population du Monde
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes qui gouvernent les habitants de Chroniques et préciser le premier contrat minimal permettant à un habitant de mener une activité productive sans intervention du joueur.

Les habitants donnent vie au monde. Ils ne sont pas de simples distributeurs de quêtes ou de services.

---

# PRINCIPE

Chaque habitant est un individu appartenant à une société.

Il possède un contexte, des besoins, des relations et une place dans le monde.

---

# IDENTITÉ

Chaque habitant est notamment défini par :

- son identité ;
- son mode de vie ;
- ses compétences ;
- ses relations ;
- ses ambitions ;
- ses contraintes.

Toutes ces dimensions n'ont pas à être implémentées simultanément.

---

# VIE AUTONOME

Les habitants poursuivent leur existence même lorsque le joueur n'interagit pas avec eux.

Ils peuvent notamment :

- travailler ;
- se déplacer ;
- échanger ;
- apprendre ;
- vieillir.

Une capacité conceptuelle n'autorise cependant pas le moteur à inventer silencieusement sa règle d'exécution. Chaque comportement autonome doit posséder une réponse GDB/ACT suffisamment définie avant code.

---

# ACTIVITÉ PRODUCTIVE COURANTE

Le premier lot productif de v0.4 ne choisit pas encore automatiquement une carrière ou un métier.

Il peut fonctionner à partir d'une **activité productive courante explicitement disponible** dans le contexte de l'habitant.

Cette disponibilité signifie qu'une opération productive réelle peut être tentée maintenant conformément à GDB-012B et GDB-005C.

```text
habitant
+
activité productive disponible
+
opération exécutable
→ candidat à une activité de travail
```

L'activité productive courante peut provenir ultérieurement d'un métier, d'une organisation, d'un lieu, d'un projet ou d'un autre système compétent.

Cette version n'impose aucune représentation technique de cette provenance.

---

# ARBITRAGE MINIMAL ENTRE ENTRETIEN ET TRAVAIL

Le premier lot autonome productif conserve une priorité minimale et déterministe :

1. répondre d'abord aux besoins physiologiques actuellement actionnables déjà couverts par GDB-004B ;
2. si aucun de ces besoins ne produit d'Intent exécutable, permettre une activité productive disponible ;
3. si aucune activité productive n'est exécutable, ne rien inventer.

```text
Intent d'entretien exécutable ?
├── oui → entretien
└── non
    ↓
activité productive exécutable ?
├── oui → travail
└── non → aucun Intent
```

Cette règle est volontairement minimale.

Elle ne définit pas encore :

- une motivation professionnelle ;
- un salaire ;
- un horaire de travail ;
- une ambition de carrière ;
- une obligation sociale de travailler ;
- une pondération psychologique entre travail et loisirs.

Elle fournit uniquement un ordre stable pour rendre possible le premier monde productif autonome sans inventer ces systèmes.

---

# RELATIONS

Les relations évoluent selon les interactions et les conséquences.

Elles ne sont jamais figées.

---

# DIVERSITÉ

Deux habitants exerçant le même métier ne doivent pas être interchangeables à terme.

Leur personnalité, leur histoire et leurs choix créent cette différence.

Le premier lot productif minimal n'est pas tenu d'implémenter immédiatement toutes ces sources de diversité.

---

# INVARIANTS

- Un habitant peut agir sans intervention du joueur.
- Une activité productive autonome doit correspondre à une opération réellement exécutable.
- Une activité indisponible ne génère aucun faux Intent.
- Le premier arbitrage minimal traite les besoins physiologiques actionnables avant le travail.
- Le moteur ne choisit pas silencieusement un métier ou une carrière dans ce lot.
- À état et configuration identiques, l'ordre d'arbitrage reste identique.

---

# RÈGLES DE CONCEPTION

Tout habitant devra :

1. avoir une raison crédible d'exister ;
2. appartenir à un environnement cohérent ;
3. pouvoir évoluer ;
4. renforcer l'immersion ;
5. participer aux histoires émergentes ;
6. ne jamais produire une activité autonome que le contexte ne rend pas réellement exécutable.

---

# CRITÈRE DE VALIDATION

Cet habitant paraît-il vivre pour lui-même, répondre à ses besoins et participer réellement au monde avant de servir le joueur ?

Si la réponse est non, il devra être repensé.

---

# HISTORIQUE

## Version 1.1

- en-tête mis en conformité avec MASTER-004 ;
- formalisation de l'activité productive courante comme capacité contextuelle explicite ;
- interdiction d'inventer automatiquement métier ou carrière ;
- définition du premier arbitrage minimal `entretien actionnable → travail → aucun Intent` ;
- ajout des invariants nécessaires au premier lot productif autonome de v0.4.

## Version 1.0

- création du document.

---

Fin du document

Statut : Validé — Référence officielle.
