# GDB-005F --- Les Échanges

> Version : 1.1
> Statut : Officiel
> Type : Économie & Progression
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes fondamentaux des échanges dans Chroniques et préciser le premier transfert économique exécutable entre habitants sans imposer monnaie, prix ou marché.

Les échanges permettent aux habitants, aux joueurs et aux communautés de satisfaire leurs besoins grâce à la coopération, au commerce et au partage.

---

# PRINCIPE

Un échange est un transfert volontaire de valeur entre au moins deux parties.

La valeur d'un échange dépend du contexte, des besoins, de la confiance et de la rareté.

Aucun transfert ne doit être présenté comme volontaire si le contexte n'autorise pas réellement la partie qui cède la valeur à le faire.

---

# LES FORMES D'ÉCHANGE

Les échanges peuvent prendre plusieurs formes :

- troc ;
- monnaie ;
- services ;
- savoir-faire ;
- informations ;
- dons ;
- héritages.

Aucune forme n'est universellement supérieure.

Le premier lot exécutable de circulation économique utilise volontairement la forme la plus simple compatible avec les autorités actuelles : **le don explicite d'une quantité de produit entre deux habitants**.

Ce choix ne fait pas du don la forme dominante de l'économie finale. Il évite uniquement d'inventer une formule de prix ou de négociation encore absente des GDB.

---

# TRANSFERT VOLONTAIRE MINIMAL

Une opportunité de transfert volontaire peut être considérée exécutable lorsqu'elle identifie explicitement :

- un Acteur qui cède le produit ;
- un destinataire distinct ;
- un stock source accessible et autorisé pour l'Acteur ;
- un stock destination compatible et rattaché au contexte du destinataire ;
- une quantité strictement positive ;
- une même identité de produit entre source et destination conformément à GDB-005E.

```text
Acteur A
+
stock source du produit P
+
Destinataire B
+
stock destination du même produit P
+
quantité q > 0
↓
transfert volontaire exécutable
```

Le contexte qui fournit cette opportunité fait autorité sur le fait qu'elle est volontaire et autorisée. Le moteur ne doit jamais inventer seul la volonté de donner.

Cette version n'impose ni inventaire général, ni propriété universelle : elle exige seulement qu'une implémentation puisse résoudre de manière déterministe les stocks réellement concernés et leur accessibilité.

---

# CONSERVATION DU TRANSFERT

Conformément à GDB-005E, un transfert réussi conserve la quantité du produit :

```text
source P -= q
+
destination P += q
```

Invariants :

- `q > 0` ;
- la source possède au moins `q` avant résolution ;
- la source et la destination représentent le même produit ;
- aucune quantité ne devient négative ;
- aucune portion n'apparaît ou ne disparaît du seul fait du transfert.

Si l'une de ces conditions n'est plus vraie au moment de la validation/exécution, l'Action ne doit pas réussir comme si elle l'était encore.

---

# AUTONOMIE ET OPPORTUNITÉ D'ÉCHANGE

La capacité à échanger existe déjà conceptuellement pour les habitants [réf: GDB-004A].

Pour le premier lot autonome, une Action de transfert ne peut être proposée que si une **opportunité d'échange volontaire explicitement disponible** existe dans le contexte.

```text
aucune opportunité disponible
→ aucun Intent de transfert inventé

opportunité disponible
→ Intent de transfert possible
```

La sélection du destinataire, des stocks et de la quantité appartient au contexte/Planner compétent, pas à un Intent abstrait.

---

# LA VALEUR

La valeur d'un bien ou d'un service n'est jamais figée.

Elle évolue selon :

- l'offre ;
- la demande ;
- la qualité ;
- la réputation ;
- la distance ;
- les événements du monde.

GDB-005I reste l'autorité sur la Valeur économique contextuelle.

Le transfert volontaire minimal ne prétend pas calculer cette valeur. L'opportunité fournie par le contexte signifie seulement que la partie cédante accepte ce transfert dans la situation considérée.

---

# CONFIANCE

La confiance facilite les échanges.

Elle se construit progressivement grâce aux relations, à la réputation et aux expériences passées.

Aucun coefficient de confiance n'est introduit dans le premier transfert minimal tant qu'une règle GDB dédiée ne fixe pas son effet numérique.

---

# FRONTIÈRE AVEC TROC, MONNAIE ET MARCHÉ

Le premier transfert volontaire ne définit pas :

- une contrepartie obligatoire ;
- un taux de troc ;
- une monnaie ;
- un prix ;
- une négociation ;
- un marché ;
- un salaire ;
- une taxation.

Le troc bilatéral et les échanges monétaires restent des extensions futures qui devront posséder leurs propres règles exécutables.

GDB-005G conserve l'autorité sur les invariants du marché.

GDB-005H conserve l'autorité sur la monnaie.

GDB-019 décrit la dimension commerciale et institutionnelle sans autoriser le moteur à inventer un prix ou une formule absents des autorités GDB.

---

# IMPACT

Les échanges influencent :

- l'économie ;
- les métiers ;
- les relations sociales ;
- les opportunités ;
- le développement des communautés.

Le transfert d'une denrée peut notamment rendre un produit précédemment inaccessible disponible dans le contexte d'un autre habitant, permettant ensuite son utilisation normale par les Actions compétentes.

---

# INVARIANTS

- Un échange implique au moins deux parties identifiables.
- Le premier transfert minimal est volontaire et contextuellement autorisé.
- Aucune opportunité absente n'est inventée par le moteur.
- Source et destination portent la même identité de produit.
- La quantité transférée est strictement positive et conservée.
- Les Cibles concrètes et la quantité appartiennent au contexte/Plan, pas à l'Intent abstrait.
- Le transfert ne crée ni monnaie, ni prix, ni marché implicite.
- À état et opportunité identiques, le transfert sélectionné reste identique.

---

# RÈGLES DE CONCEPTION

Toute mécanique liée aux échanges devra :

1. reposer sur une logique crédible ;
2. favoriser plusieurs formes d'échange ;
3. rester sensible au contexte du monde ;
4. encourager les interactions entre systèmes ;
5. enrichir l'expérience du joueur ;
6. conserver les quantités lors d'un simple transfert ;
7. ne jamais confondre opportunité volontaire et décision arbitraire du moteur.

---

# CRITÈRE DE VALIDATION

Cette mécanique crée-t-elle une circulation réelle et crédible de valeur entre acteurs, avec des parties, des stocks et une autorisation explicites, plutôt qu'un simple déplacement gratuit ou un système de vente automatisé ?

Si la réponse est non, elle devra être repensée.

---

# HISTORIQUE

## Version 1.1

- en-tête mis en conformité avec MASTER-004 ;
- définition du premier transfert volontaire exécutable entre deux habitants ;
- conservation stricte des quantités et compatibilité d'identité de produit ;
- opportunité d'échange contextuelle obligatoire ;
- séparation explicite avec troc bilatéral, monnaie, prix et marché.

## Version 1.0

- création du document.

---

Fin du document
