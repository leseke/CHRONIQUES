# GDB-004E --- Les Habitudes

> Version : 1.2
> Statut : Officiel
> Type : Population du Monde
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir un modèle d'Habitudes implémentable sans interprétation floue du contexte ni score transversal entre familles d'Intent.

---

# PRINCIPE

Une Habitude est un comportement acquis par répétition. Elle peut produire un Intent lorsque son contexte d'activation est satisfait, sans produire directement une Action Instance.

Une Habitude n'est jamais un script imposé et ne court-circuite pas l'ordre des familles défini par GDB-004A.

---

# MODÈLE

Chaque Habitude possède au minimum :

- **Déclencheur** : règle déterministe lisant le World et le Tick courant ;
- **Objectif d'Intent** : objectif soumis à ACT si l'Habitude est sélectionnée ;
- **Force** : valeur continue bornée de 0 à 100 ;
- **Tick de dernière activation** ;
- **Tick de création** ;
- **Signature de formation** : identité déterministe du contexte dans lequel les répétitions sont comptées pour former cette Habitude.

Le Déclencheur ne peut pas être une condition vague comme « quand cela semble approprié ». Il doit être évalué comme vrai ou faux à état et Tick identiques.

Il ne peut pas être « toujours » dans le modèle minimal : un comportement permanent appartient à une autre règle de décision.

---

# SIGNATURE DE FORMATION

La formation ne repose jamais sur une notion implicite de « contexte similaire ».

Chaque type concret d'Habitude fournit une règle déterministe permettant de produire une **Signature de formation** à partir du contexte pertinent.

```text
même objectif d'Intent
+
même Signature de formation
→ répétitions comptées ensemble
```

```text
signature différente
→ séquence de formation distincte
```

La signature peut dépendre, selon le type d'Habitude, d'un lieu, d'une plage temporelle, d'une relation, d'une activité, d'une saison ou d'autres données explicitement choisies par la règle concrète.

Le moteur générique ne calcule jamais une distance de similarité entre contextes.

---

# FORMATION

Une Habitude se forme lorsqu'un même objectif d'Intent est observé avec la même Signature de formation un nombre de fois suffisant dans une fenêtre temporelle configurée.

Les valeurs exactes restent paramétrables :

- nombre de répétitions ;
- taille de fenêtre ;
- Force initiale.

La Force initiale reste inférieure au maximum.

Conformément à GDB-004D, un Trait peut modifier le seuil de répétitions uniquement lorsqu'un mapping concret Trait/Habitude le spécifie.

La personnalité ne modifie pas automatiquement le Déclencheur d'une Habitude déjà formée.

---

# CANDIDATURE

Une Habitude est candidate si :

```text
Habitude existante
+
Force > 0
+
Déclencheur = vrai
+
objectif d'Intent actuellement traitable
→ candidate
```

Une Habitude dont l'objectif ne peut pas être planifié/exécuté dans le contexte courant ne produit aucun faux Intent et ne bloque pas les autres Habitudes candidates.

---

# ARBITRAGE INTERNE

Lorsque plusieurs Habitudes sont candidates :

1. Force la plus élevée ;
2. en cas d'égalité, Tick de création le plus bas.

La Force exprime **uniquement la priorité relative entre Habitudes candidates**.

Elle ne compare jamais directement une Habitude à :

- un besoin ;
- un transfert ;
- une production ;
- une Ambition.

L'ordre entre familles appartient exclusivement à GDB-004A.

---

# PLACE DANS L'ARBITRAGE GÉNÉRAL

La place courante est :

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

Une Habitude forte ne dépasse donc pas une famille située plus haut dans cette version.

Aucune fairness transversale n'est implicite.

---

# ÉVOLUTION

## Renforcement

Après exécution réussie de l'Intent produit dans le contexte attendu, la Force peut augmenter. Le gain diminue à mesure que la Force approche 100.

## Érosion

Après une durée d'inactivité supérieure à un seuil configuré, la Force diminue progressivement. Une activation ultérieure interrompt l'érosion.

Une Force atteignant 0 entraîne la disparition de l'Habitude.

## Perturbation

Un événement significatif identifiable peut modifier le Déclencheur, réduire la Force ou supprimer l'Habitude si une règle concrète le prévoit.

Aucune perturbation n'est déclenchée par une dérive silencieuse.

---

# ACTIVATION ET TICK DE DERNIÈRE ACTIVATION

Le Tick de dernière activation est mis à jour lorsqu'une Habitude sélectionnée produit effectivement son Intent.

Le renforcement, lui, exige la réussite de l'exécution associée. Activation et réussite restent donc deux faits distincts.

---

# FRONTIÈRE AVEC GDB-004D

La personnalité peut modifier la formation d'une Habitude via un mapping concret de seuil de répétition.

GDB-004D ne décide ni du Déclencheur courant, ni de la Force courante, ni de l'ordre de familles.

---

# FRONTIÈRE AVEC GDB-004F

Une Habitude est un comportement contextuel acquis ; une Ambition est une direction de vie durable.

Une Habitude peut se former à partir d'Actions répétées motivées par une Ambition, mais les deux données restent indépendantes.

---

# PARAMÈTRES D'IMPLÉMENTATION

Restent paramétrables :

- seuil de répétitions ;
- fenêtre de formation ;
- Force initiale ;
- gain de renforcement ;
- forme de décroissance du gain ;
- seuil d'inactivité ;
- taux d'érosion ;
- règles concrètes de perturbation ;
- mappings Trait/Habitude.

La définition de chaque Déclencheur et de chaque Signature de formation appartient au type concret d'Habitude.

---

# INVARIANTS

- Une Habitude possède un Déclencheur déterministe et une Signature de formation déterministe.
- Aucune similarité contextuelle implicite n'est calculée par le moteur générique.
- Une Habitude produit au maximum un Intent, jamais une Action Instance.
- Force est bornée entre 0 et 100.
- Force départage uniquement les Habitudes.
- L'ordre entre familles appartient à GDB-004A.
- Une Habitude non exécutable ne produit aucun faux Intent.
- La personnalité ne modifie pas implicitement l'activation d'une Habitude existante.
- Renforcement et érosion suivent des règles déterministes paramétrées.
- Toute perturbation significative possède une cause identifiable.

---

# CRITÈRE DE VALIDATION

Le système peut-il former, sélectionner et faire évoluer une Habitude à partir de règles contextuelles entièrement déterministes, sans inventer une similarité de contexte ni comparer sa Force aux autres familles d'Intent ?

Si la réponse est non, il doit être repensé.

---

# HISTORIQUE

## Version 1.2

- synchronisation avec GDB-004A v1.3 et GDB-004D v1.3 ;
- ajout de la Signature de formation déterministe ;
- suppression de la notion floue de « contexte similaire » ;
- Force limitée à l'arbitrage interne entre Habitudes ;
- exigence d'un objectif d'Intent actuellement traitable ;
- personnalité limitée à la modulation explicite du seuil de formation.

## Version 1.1

- passage en Maturité 2 ; modèle Force/Ticks, formation, évolution et premier arbitrage.

## Version 1.0

- création du document.

---

Fin du document
