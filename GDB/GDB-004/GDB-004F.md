# GDB-004F --- Les Ambitions

> Version : 1.2
> Statut : Officiel
> Type : Population du Monde
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir un modèle d'Ambitions implémentable sans que le moteur générique invente la création d'un objectif, son évaluation ou sa progression.

---

# PRINCIPE

Une Ambition est une direction de vie durable : un état futur désiré qui peut orienter des décisions sur plusieurs Ticks.

Elle n'est ni un besoin urgent ni une Habitude contextuelle.

Une Ambition produit au maximum un Intent et ne matérialise jamais directement l'état futur recherché.

---

# MODÈLE

Chaque Ambition possède :

- **Type d'Ambition** : identifie la règle concrète qui définit sa création, son évaluateur d'objectif et son calcul de Progrès ;
- **Objectif** : données concrètes décrivant l'état futur désiré ;
- **Intensité** : valeur continue bornée de 0 à 100 ;
- **Progrès** : valeur continue bornée de 0 à 100 ;
- **Objectif d'Intent** : objectif soumis à ACT lorsqu'elle est sélectionnée ;
- **Tick de création**.

Le moteur générique ne déduit jamais le Type d'Ambition à partir d'un texte libre.

---

# RÈGLE CONCRÈTE D'AMBITION

Chaque Type d'Ambition autorisé doit fournir une règle déterministe contenant au minimum :

1. les conditions de création de ce type d'Ambition ;
2. la structure de ses données d'Objectif ;
3. un évaluateur capable de déterminer si l'objectif est atteint ;
4. une fonction déterministe produisant le Progrès `0..100` à partir du World et de l'Objectif ;
5. l'Objectif d'Intent que cette Ambition peut produire ;
6. les conditions qui rendent cet Intent actuellement traitable.

Exemples conceptuels possibles : logement, niveau de Compétence, relation ou stock de produit. **Ces exemples ne constituent pas à eux seuls des Types implémentables.** Leur règle concrète doit exister avant ENGINE.

```text
Type concret absent
→ Ambition non créable par le moteur générique
```

---

# PROGRÈS

`Progrès = 0` représente le début de la progression et `Progrès = 100` l'objectif atteint.

Le System compétent évalue le Progrès en lisant le World via la règle du Type d'Ambition.

Il est interdit au moteur générique d'inventer une formule universelle de distance entre l'état actuel et un objectif quelconque.

À World, Objectif, Type et configuration identiques, le même Progrès doit être produit.

---

# CRÉATION

Une Ambition n'est jamais créée simplement parce qu'un objectif paraît plausible.

Sa création exige les conditions déterministes définies par son Type concret.

Les données suivantes peuvent être lues par un Type lorsqu'une autorité applicable le prévoit :

- personnalité ;
- besoins ;
- expériences et événements du World ;
- culture ;
- relations ;
- autres données explicitement autorisées.

**GDB-002E reste l'autorité sur les Opportunités offertes au joueur et n'est pas réutilisé silencieusement comme source de création d'Ambitions PNJ.**

Une future notion d'Opportunité PNJ devra disposer de sa propre autorité.

---

# CANDIDATURE

Une Ambition est candidate si :

```text
Ambition existante
+
Intensité > 0
+
Progrès < 100
+
objectif non abandonné
+
Objectif d'Intent actuellement traitable
→ candidate
```

Une Ambition non exécutable ne produit aucun faux Intent et ne bloque pas les autres Ambitions candidates.

---

# ARBITRAGE INTERNE

Lorsque plusieurs Ambitions sont candidates :

1. Intensité la plus élevée ;
2. en cas d'égalité, Progrès le plus élevé ;
3. en cas de nouvelle égalité, Tick de création le plus bas.

Cet ordre est une règle propre aux Ambitions. Il n'est pas dérivé de l'urgence des besoins et ne constitue pas un score transversal.

L'Intensité compare uniquement des Ambitions candidates entre elles.

---

# PLACE DANS L'ARBITRAGE GÉNÉRAL

Conformément à GDB-004A :

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

Une Ambition d'Intensité élevée ne dépasse pas une famille placée plus haut dans la version courante.

Aucune fairness inter-familles n'est implicite.

---

# PERSONNALITÉ

Conformément à GDB-004D, un Trait peut modifier l'Intensité d'une Ambition uniquement lorsqu'un mapping concret Trait/Ambition le prévoit.

La personnalité ne crée pas automatiquement une Ambition et ne choisit pas directement son Intent.

---

# FRONTIÈRE AVEC LES BESOINS

Un besoin décrit un état courant et son urgence interne est définie par GDB-004B.

Une Ambition décrit un état futur désiré. Elle ne modifie pas implicitement la satisfaction ou l'urgence d'un besoin.

---

# FRONTIÈRE AVEC LES HABITUDES

Une Habitude est un comportement contextuel acquis ; une Ambition est une direction durable.

Des Actions répétées pour poursuivre une Ambition peuvent participer à la formation d'une Habitude conformément à GDB-004E, sans fusionner les deux données.

---

# ÉVOLUTION

## Renforcement

Un événement ou résultat identifiable peut augmenter l'Intensité lorsqu'une règle applicable le prévoit.

## Affaiblissement

Un événement identifiable peut diminuer l'Intensité. À Intensité 0, l'Ambition disparaît.

## Accomplissement

À Progrès 100, l'Ambition est accomplie et cesse d'être candidate.

La création d'une Ambition suivante n'est jamais automatique sans règle concrète.

## Abandon

Une Ambition peut être abandonnée lorsqu'une règle concrète identifie que ses conditions d'abandon sont remplies.

L'abandon est un fait identifiable ; aucune disparition silencieuse n'est autorisée.

---

# PARAMÈTRES D'IMPLÉMENTATION

Restent paramétrables :

- Intensité initiale ;
- gains/pertes d'Intensité ;
- conditions d'abandon ;
- mappings Trait/Ambition ;
- paramètres propres aux évaluateurs de chaque Type d'Ambition.

Les Types concrets et leurs règles doivent être documentés avant leur implémentation.

---

# INVARIANTS

- Une Ambition possède un Type concret, un Objectif, une Intensité, un Progrès, un Objectif d'Intent et un Tick de création.
- Aucun Type d'Ambition n'est inventé par le moteur générique.
- Chaque Type fournit un évaluateur d'objectif/progrès déterministe.
- Intensité et Progrès restent bornés entre 0 et 100.
- Intensité départage uniquement les Ambitions.
- L'ordre entre familles appartient à GDB-004A.
- Une Ambition non exécutable ne produit aucun faux Intent.
- GDB-002E n'est pas réutilisé comme source PNJ.
- Une personnalité ne crée pas automatiquement d'Ambition.
- Accomplissement et abandon sont des états identifiables.

---

# CRITÈRE DE VALIDATION

Le système peut-il créer, évaluer, faire progresser et sélectionner une Ambition à partir d'un Type concret déterministe, sans que le moteur générique invente une formule de progression, une Opportunité PNJ ou un score transversal ?

Si la réponse est non, il doit être repensé.

---

# HISTORIQUE

## Version 1.2

- synchronisation avec GDB-004A v1.3, GDB-004B v1.3, GDB-004D v1.3 et GDB-004E v1.2 ;
- ajout du Type d'Ambition et de l'évaluateur objectif/progrès déterministe ;
- interdiction d'une formule générique implicite de Progrès ;
- Intensité limitée à l'arbitrage interne entre Ambitions ;
- suppression de la dépendance normative à GDB-002E pour les PNJ ;
- exigence d'un Objectif d'Intent actuellement traitable.

## Version 1.1

- passage en Maturité 2 ; modèle Objectif/Intensité/Progrès/Intent/Tick et arbitrage interne.

## Version 1.0

- création du document.

---

Fin du document
