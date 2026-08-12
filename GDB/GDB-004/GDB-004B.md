# GDB-004B --- Les Besoins des Habitants

> Version : 1.3
> Statut : Officiel
> Type : Population du Monde
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les besoins des habitants et leur rôle dans la production de décisions autonomes.

Un besoin ne modifie jamais directement le World : il peut produire un Intent, qui traverse ensuite ACT.

```text
Besoin
↓
évaluation
↓
Intent éventuel
↓
ACT
↓
Action
↓
Outcome
↓
World
```

---

# CATÉGORIES

Les besoins peuvent notamment concerner la nourriture, le logement, la sécurité, les relations, le travail, l'apprentissage, le repos, les loisirs et la transmission.

Toutes les catégories n'ont pas à être implémentées simultanément.

---

# SATISFACTION

Lorsqu'un besoin est représenté numériquement :

```text
0 = critique / non satisfait
100 = pleinement satisfait
```

La valeur reste bornée entre 0 et 100.

---

# SEUIL D'ACTIVATION

Un besoin devient candidat uniquement si :

```text
satisfaction < seuil
```

L'égalité au seuil signifie non activé.

Les seuils sont des paramètres d'équilibrage déterministes, pas des constantes universelles de GDB.

---

# BESOIN ACTIONNABLE

Un besoin sous son seuil n'est actionnable que si le contexte permet une réponse réellement exécutable.

```text
besoin urgent
+
aucune réponse exécutable
→ aucun faux Intent
```

Un besoin sans réponse ne disparaît pas et n'est pas considéré comme satisfait ; il ne bloque simplement pas les autres besoins actionnables.

---

# ARBITRAGE ENTRE BESOINS

Lorsque plusieurs besoins sont actionnables :

```text
satisfaction plus basse
→ urgence de base plus forte
```

Une égalité est départagée par un ordre stable explicitement configuré, jamais par un hasard non déterministe.

Ce mécanisme départage **uniquement les besoins**. Il ne constitue pas un score général entre les différentes familles de décisions autonomes.

L'ordre entre familles est défini par GDB-004A.

---

# CONTRAT AUTONOME — REPOS

```text
Fatigue < seuil configuré
→ Intent se_reposer
```

La capacité ACT correspondante est `VERB-001 — Se reposer`.

---

# CONTRAT AUTONOME — NOURRITURE

```text
Faim < seuil configuré
+
produit alimentaire accessible et consommable
→ Intent manger
```

Sans nourriture accessible :

```text
Faim < seuil
+
aucune nourriture accessible
→ aucun Intent manger
```

L'Intent `manger` ne transporte pas la Cible concrète. La sélection du produit appartient au Plan conformément à ACT et GDB-005E.

Une Action alimentaire réussie consomme réellement le produit et peut augmenter Faim selon la valeur configurée du produit.

---

# FRONTIÈRE AVEC LA PERSONNALITÉ

GDB-004D ne définit pas de coefficient direct modifiant l'urgence des besoins dans le modèle courant.

La personnalité agit en amont sur les Habitudes et les Ambitions selon les liens concrets spécifiés par GDB-004D/E/F.

Le moteur ne doit donc pas injecter automatiquement un Trait dans le calcul d'urgence d'un besoin.

---

# FRONTIÈRE AVEC LES HABITUDES

GDB-004E définit désormais les Habitudes comme une famille d'Intent distincte, située après les familles économiques dans l'ordre courant de GDB-004A.

Une Habitude ne modifie pas implicitement la satisfaction, le seuil ou l'urgence d'un besoin.

Toute future interaction directe Habitude → besoin devra être spécifiée explicitement.

---

# FRONTIÈRE AVEC LES AMBITIONS

GDB-004F définit désormais les Ambitions comme une famille d'Intent distincte, située après les Habitudes dans l'ordre courant de GDB-004A.

Une Ambition ne modifie pas implicitement la satisfaction, le seuil ou l'urgence d'un besoin.

Les besoins physiologiques actionnables restent prioritaires conformément à GDB-004A.

---

# FRONTIÈRE AVEC LES OPPORTUNITÉS

GDB-002E définit actuellement des Opportunités destinées au joueur.

Elles ne sont pas réutilisées silencieusement comme source normative de décision PNJ.

Toute opportunité PNJ doit être définie par l'autorité compétente, comme l'opportunité de transfert volontaire de GDB-005F.

---

# ÉVOLUTION

La satisfaction des besoins peut évoluer avec le temps, l'âge, la profession, la famille, les saisons et les conséquences du monde.

Cette évolution appartient aux Systems et Effects compétents. La couche de décision n'est jamais une seconde source de vérité.

---

# INVARIANTS

- Un besoin ne modifie jamais directement le World.
- Un besoin sans réponse exécutable ne produit aucun faux Intent.
- Le seuil est strict : égal au seuil signifie non activé.
- Une satisfaction plus faible ne produit pas une urgence de base plus faible.
- Les égalités entre besoins sont déterministes.
- `se_reposer` ne nécessite aucune ressource alimentaire.
- `manger` exige une nourriture accessible et réellement consommable.
- L'Intent `manger` ne transporte pas la Cible alimentaire.
- Personnalité, Habitudes et Ambitions ne modifient pas implicitement le calcul d'urgence des besoins.
- L'arbitrage entre familles appartient à GDB-004A.
- Les Opportunités joueur de GDB-002E ne sont pas réutilisées comme Opportunités PNJ sans autorité explicite.

---

# CRITÈRE DE VALIDATION

Le système transforme-t-il un besoin réellement insatisfait en objectif autonome cohérent et exécutable, sans inventer une Action, une Cible, une ressource ou un coefficient absent des autorités ?

Si la réponse est non, il doit être repensé.

---

# HISTORIQUE

## Version 1.3

- synchronisation avec GDB-004A v1.3 et GDB-004D/E/F ;
- Habitudes et Ambitions reconnues comme familles d'Intent distinctes plutôt que modificateurs implicites des besoins ;
- suppression des anciennes formulations indiquant que leur arbitrage restait non spécifié ;
- confirmation que l'arbitrage entre familles appartient à GDB-004A ;
- maintien de GDB-002E comme Opportunités joueur uniquement.

## Version 1.2

- ajout du contrat `Faim → manger` et de l'accessibilité alimentaire.

## Version 1.1

- passage en Maturité 2 ; seuil strict, besoin actionnable et arbitrage déterministe.

## Version 1.0

- création du document.

---

Fin du document
