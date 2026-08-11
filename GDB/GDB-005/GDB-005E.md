# GDB-005E --- Les Produits

> Version : 1.2
> Statut : Officiel
> Type : Économie & Progression
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes fondamentaux des produits dans Chroniques.

Les produits représentent l'aboutissement des chaînes de production et répondent aux besoins des habitants, des joueurs et du monde.

---

# PRINCIPE

Tout produit doit avoir une origine identifiable, une utilité crédible et une place dans l'économie.

Un produit n'existe jamais uniquement comme récompense de gameplay.

Un produit utilisé par une Action doit exister comme élément réellement disponible dans le monde ou dans le contexte de l'Acteur. Une Action ne peut jamais matérialiser gratuitement le produit dont elle a besoin.

---

# IDENTITÉ DE PRODUIT

Lorsqu'une mécanique doit transférer, regrouper ou comparer plusieurs stocks de produits, leur nature ne peut pas être déduite d'une simple quantité ou d'un même type technique de Component.

Le contexte doit donc pouvoir fournir une **identité de produit stable**.

```text
même identité de produit
→ stocks compatibles pour un transfert ou regroupement

identités différentes
→ stocks non fusionnables implicitement
```

Cette identité décrit la nature du produit, pas l'Entity particulière qui porte un stock.

Deux Entities différentes peuvent donc représenter deux stocks du même produit.

Inversement, deux produits possédant par hasard la même valeur alimentaire ne deviennent jamais le même produit pour cette seule raison.

GDB-005E n'impose pas le format technique de l'identifiant. Il doit seulement être explicite, stable dans le contexte concerné et comparable de manière déterministe.

---

# CYCLE DE VIE

Chaque produit suit un cycle :

- conception ;
- fabrication ;
- distribution ;
- utilisation ;
- entretien éventuel ;
- recyclage ou disparition.

Lorsqu'un produit est consommable, son utilisation réduit sa disponibilité : consommation d'une unité, d'une portion, d'une quantité ou disparition complète selon la nature du produit.

Invariant :

```text
consommation réussie
→ disponibilité du produit consommé diminue
```

Une même unité consommée ne peut donc pas être réutilisée indéfiniment.

---

# UTILITÉ

Un produit peut répondre à plusieurs besoins :

- alimentation ;
- artisanat ;
- construction ;
- transport ;
- confort ;
- culture ;
- transmission.

Les usages multiples sont privilégiés lorsque cela reste crédible.

---

# PRODUIT ALIMENTAIRE

Un produit alimentaire est un produit dont au moins un usage consiste à contribuer à satisfaire le besoin de nourriture d'un habitant [réf: GDB-004B].

Sa consommation réussie peut augmenter la satisfaction de ce besoin.

Dans la représentation actuellement utilisée par la simulation :

```text
besoin de nourriture
→ Faim

0
→ critique

100
→ pleinement satisfait
```

GDB-005E ne fixe aucune quantité universelle de restauration.

La valeur alimentaire dépend du produit ou des données d'équilibrage applicables.

```text
produit A
≠ nécessairement
produit B
```

Une valeur plus importante peut restaurer davantage le besoin de nourriture, mais les valeurs numériques exactes restent du tuning tant qu'une règle plus précise ne les fixe pas.

---

# ACCESSIBILITÉ D'UN PRODUIT

Un produit ne peut être utilisé par un Acteur que s'il est accessible dans le Contexte de l'Action conformément au contrat de Cible d'ACT [réf: ACT-005-A].

L'accessibilité est une propriété métier contextuelle. Elle peut notamment résulter :

- d'une possession ou garde personnelle future ;
- d'un accès partagé ;
- d'une mise à disposition explicite ;
- d'une présence dans un contexte où l'Acteur est autorisé à l'utiliser.

Cette liste ne définit pas un système d'inventaire et n'impose aucune représentation technique.

Invariant :

```text
produit existant mais non accessible à l'Acteur
≠
produit utilisable par son Action
```

L'architecture moteur devra représenter ou résoudre cette accessibilité avant d'autoriser l'utilisation du produit.

---

# TRANSFERT ENTRE STOCKS

Un transfert de produit ne crée ni ne détruit implicitement la quantité transférée.

Pour une quantité `q > 0` :

```text
stock source du produit P -= q
stock destination du même produit P += q
```

Un transfert réussi exige donc :

- une source existante et suffisamment disponible ;
- une destination compatible ;
- la même identité de produit de part et d'autre ;
- une accessibilité/autorisation conforme au contexte de l'échange ;
- aucune quantité négative après résolution.

Le transfert peut modifier l'accessibilité du produit pour les parties sans créer un système général d'inventaire dans cette version.

---

# CONSOMMATION ALIMENTAIRE

Une consommation alimentaire valide relie trois faits :

```text
Acteur
+
produit alimentaire accessible
+
Action résolue avec succès
↓
disponibilité du produit ↓
+
satisfaction de Faim ↑
```

La consommation ne modifie jamais directement le besoin avant la résolution de l'Action.

Si le produit n'est plus disponible ou n'est plus accessible au moment où l'Action doit être validée, l'Action ne doit pas être exécutée comme si le produit existait encore.

---

# QUALITÉ

Tous les produits ne se valent pas.

Leur qualité dépend notamment :

- des ressources utilisées ;
- des compétences du fabricant ;
- des outils employés ;
- des conditions de production.

La qualité pourra ultérieurement influencer l'alimentation si une règle GDB dédiée précise cette relation. Aucun coefficient implicite n'est introduit dans cette version.

---

# IMPACT

Les produits alimentent les échanges, les métiers, les projets et les histoires émergentes.

Ils participent à l'identité économique du monde.

Les produits alimentaires créent en particulier un lien réel entre les besoins des habitants [réf: GDB-004B], les ressources [réf: GDB-005B], la production, la distribution et la consommation.

---

# INVARIANTS

- Un produit possède une origine et une utilité crédibles.
- Une Action ne crée jamais gratuitement le produit qu'elle prétend utiliser.
- Un produit consommable perd de la disponibilité après consommation réussie.
- Un produit non accessible à l'Acteur ne peut pas être utilisé par son Action.
- Un produit alimentaire peut contribuer à restaurer le besoin de nourriture.
- La restauration alimentaire n'a pas de valeur universelle imposée par cette version.
- L'accessibilité métier n'impose pas encore un système technique d'inventaire.
- Deux stocks ne sont fusionnables ou transférables l'un vers l'autre que si leur identité de produit est compatible.
- Un transfert conserve la quantité : ce qui quitte la source apparaît dans la destination, sauf règle distincte explicitement documentée.

---

# RÈGLES DE CONCEPTION

Tout produit devra :

1. avoir une utilité crédible ;
2. provenir d'une chaîne de production logique ;
3. posséder plusieurs usages lorsque cela est pertinent ;
4. interagir avec d'autres systèmes ;
5. enrichir l'économie du monde ;
6. ne jamais être consommé sans réduction correspondante de sa disponibilité ;
7. respecter l'accessibilité de l'Acteur lorsqu'il sert de Cible à une Action ;
8. posséder une identité explicite lorsqu'une mécanique doit comparer ou transférer plusieurs stocks.

---

# CRITÈRE DE VALIDATION

Ce produit apporte-t-il une véritable valeur au monde, avec une origine, une identité, une disponibilité et des usages cohérents, plutôt que d'être un objet abstrait créé, fusionné ou consommé gratuitement pour les besoins du gameplay ?

Si la réponse est non, il devra être repensé.

---

# HISTORIQUE

## Version 1.2

- ajout de l'identité de produit stable pour les mécaniques de transfert/regroupement ;
- interdiction de déduire l'identité d'un produit de sa seule valeur alimentaire ou de son type technique ;
- formalisation de la conservation lors d'un transfert entre stocks compatibles ;
- maintien de la frontière avec un futur système général d'inventaire.

## Version 1.1

- en-tête mis en conformité avec MASTER-004 ;
- formalisation des produits consommables et de la réduction de disponibilité ;
- définition minimale du produit alimentaire ;
- liaison explicite alimentation → satisfaction de Faim [réf: GDB-004B] ;
- définition de l'accessibilité métier d'un produit sans imposer un système d'inventaire ;
- séparation entre règle GDB et valeurs numériques de tuning.

## Version 1.0

- création du document.

---

Fin du document
