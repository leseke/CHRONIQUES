# GDB-004A — Les Habitants du Monde

> Version : 1.3
> Statut : Officiel
> Type : Population du Monde
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes qui gouvernent les habitants de Chroniques et l'ordre minimal des familles de décisions autonomes actuellement spécifiées.

Les habitants poursuivent leur existence même lorsque le joueur n'interagit pas avec eux. Une capacité conceptuelle n'autorise jamais le moteur à inventer silencieusement sa règle d'exécution.

---

# IDENTITÉ ET VIE AUTONOME

Un habitant possède notamment une identité, des besoins, des relations, des compétences, une personnalité, des Habitudes, des Ambitions et des contraintes.

Il peut notamment répondre à ses besoins, travailler, échanger, apprendre, agir selon ses Habitudes, poursuivre des Ambitions, se déplacer et vieillir.

Toutes ces dimensions n'ont pas à être implémentées simultanément.

---

# FAMILLES DÉJÀ SPÉCIFIÉES

## Entretien

Les besoins physiologiques actionnables suivent GDB-004B. Un besoin sans réponse exécutable ne produit aucun faux Intent.

## Échange volontaire

Une Action d'échange autonome exige une opportunité de transfert volontaire explicitement disponible et encore exécutable conformément à GDB-005F. L'absence d'opportunité ne devient jamais une volonté implicite de donner.

## Production

Une activité productive autonome exige une opération productive explicitement disponible et réellement exécutable conformément à GDB-005C et GDB-012B. Le moteur ne choisit pas silencieusement un métier ou une carrière.

## Habitudes

Une Habitude devient candidate conformément à GDB-004E : elle existe réellement, son déclencheur déterministe est satisfait, sa Force est strictement positive et son objectif d'Intent est traitable par le contexte.

## Ambitions

Une Ambition devient candidate conformément à GDB-004F : elle existe réellement, n'est ni accomplie ni abandonnée, possède une règle concrète déterministe d'évaluation de son objectif/progrès et son objectif d'Intent est traitable par le contexte.

---

# ARBITRAGE AUTONOME COURANT

Pour v0.4, l'ordre des familles est fixe :

```text
besoins physiologiques actionnables
↓
transfert volontaire exécutable
↓
activité productive exécutable
↓
Habitudes actives
↓
Ambitions candidates
↓
aucun Intent
```

La première famille qui produit un Intent exécutable gagne pour ce passage de décision. Les familles suivantes ne produisent pas de second Intent concurrent pendant le même passage.

Cet ordre de familles est distinct des règles internes :

- GDB-004B départage les besoins actionnables ;
- GDB-004E départage les Habitudes par Force puis ancienneté ;
- GDB-004F départage les Ambitions par Intensité, puis Progrès, puis ancienneté.

**Force et Intensité sont des priorités internes à leur famille.** Elles ne forment pas un score universel permettant de comparer directement un besoin, un transfert, une production, une Habitude et une Ambition.

Le champ `Priorite` d'un Intent reste conforme à ACT, mais cette version ne définit aucun calcul transversal entre familles.

---

# ABSENCE DE FAIRNESS IMPLICITE

Si une famille située plus haut reste continuellement exécutable, elle peut différer les familles situées plus bas.

Le moteur ne doit pas inventer de round-robin, quota, vieillissement de priorité, bonus de frustration ou score psychologique global.

Toute future règle de fairness ou d'arbitrage transversal devra être spécifiée explicitement dans GDB avant code.

---

# PERSONNALITÉ

La personnalité n'est pas une famille d'Intent et n'entre pas directement dans la chaîne précédente.

Conformément à GDB-004D, elle agit en amont uniquement lorsque le lien concret est spécifié :

- modulation du seuil de formation d'une Habitude ;
- modulation de l'Intensité d'une Ambition.

Elle ne court-circuite jamais l'ordre des familles.

---

# RELATIONS ET DIVERSITÉ

Les relations évoluent selon les interactions et leurs conséquences. Un transfert volontaire n'applique pas automatiquement un effet relationnel tant qu'une règle distincte ne le spécifie pas.

Deux habitants placés dans un contexte proche peuvent diverger par leur personnalité, leur histoire, leurs Habitudes, leurs Ambitions, leurs relations et leurs compétences.

---

# INVARIANTS

- Un habitant peut agir sans intervention du joueur.
- Toute famille autonome produit au maximum un Intent avant ACT.
- Une réponse indisponible ne génère aucun faux Intent.
- L'ordre courant est `entretien → échange volontaire → travail → Habitudes → Ambitions → aucun Intent`.
- Force et Intensité restent internes à leur famille.
- Aucun score ou mécanisme de fairness inter-familles n'est implicite.
- La personnalité n'est pas une source directe d'Intent.
- Le moteur n'invente ni volonté, ni métier, ni prix, ni Habitude, ni Ambition absente.
- À état et configuration identiques, la décision reste déterministe.

---

# CRITÈRE DE VALIDATION

L'habitant peut-il produire une décision autonome unique, déterministe et réellement exécutable à partir des familles spécifiées, sans que le moteur invente un score, une volonté, une ressource ou un objectif absent des autorités ?

Si la réponse est non, le modèle doit être repensé.

---

# HISTORIQUE

## Version 1.3

- synchronisation avec GDB-004D/E/F ;
- extension de l'ordre à `entretien → échange volontaire → travail → Habitudes → Ambitions → aucun Intent` ;
- Force et Intensité limitées à l'arbitrage interne de leur famille ;
- absence de fairness inter-familles implicite ;
- personnalité confirmée comme influence amont, jamais comme source directe d'Intent.

## Version 1.2

- ajout du transfert volontaire avant la production ;
- interdiction d'inventer volonté de donner, prix ou négociation.

## Version 1.1

- formalisation de l'activité productive courante et du premier arbitrage minimal.

## Version 1.0

- création du document.

---

Fin du document

Statut : Validé — Référence officielle.
