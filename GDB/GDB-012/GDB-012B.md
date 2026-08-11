# GDB-012B — Les Activités

> Version : 1.1
> Statut : Officiel
> Type : Métiers & Activités
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes fondamentaux des activités dans Chroniques et préciser le contrat minimal d'une activité productive exécutable par un habitant.

Les activités représentent l'ensemble des occupations qu'un personnage peut exercer au quotidien.

---

# PRINCIPE

Une activité est une action durable réalisée dans un but précis.

Elle peut être productive, sociale, créative, culturelle, scientifique ou personnelle.

Chaque activité possède une valeur propre.

---

# LES GRANDES CATÉGORIES

Les activités comprennent notamment :

- produire ;
- explorer ;
- apprendre ;
- enseigner ;
- commercer ;
- construire ;
- créer ;
- se divertir.

Aucune catégorie n'est obligatoire ni supérieure aux autres.

---

# ACTIVITÉ PRODUCTIVE

Une activité productive est une activité dont l'exécution contribue à une opération de production conforme à GDB-005C.

Dans le premier lot autonome minimal, une activité productive est **disponible** pour un Acteur seulement si le contexte peut fournir une opération de production actuellement exécutable.

```text
Acteur
+
opération productive disponible
+
entrées accessibles et suffisantes
→ activité productive exécutable
```

L'activité ne crée jamais ses propres entrées ni sa propre recette.

---

# ACTIVITÉ ET MÉTIER

Une activité productive n'est pas nécessairement un métier complet.

```text
Métier
= manière durable de vivre et d'exercer

Activité
= occupation concrète réalisable dans un contexte donné
```

Le premier lot moteur peut recevoir une activité productive explicitement disponible sans encore simuler le choix de carrière, le contrat de travail, l'employeur ou le salaire.

Cette simplification ne transforme pas l'activité en métier implicite.

---

# DÉCISION AUTONOME MINIMALE

GDB-004A définit l'ordre minimal entre entretien physiologique et travail.

Lorsque l'habitant ne produit aucun Intent d'entretien immédiatement exécutable et qu'une activité productive réelle est disponible :

```text
activité productive disponible
→ Intent productif possible
```

L'objectif exact et le Verbe ACT correspondants doivent être documentés avant implémentation.

Si l'activité cesse d'être exécutable, aucun faux Intent productif ne doit être créé.

---

# ÉVOLUTION

Les activités évoluent avec :

- les compétences ;
- les outils ;
- les connaissances ;
- les besoins des communautés ;
- les innovations.

Ces influences ne deviennent pas automatiquement des modificateurs numériques tant que leurs règles ne sont pas précisées.

---

# IMPACT

Les activités influencent :

- les métiers ;
- les relations ;
- l'économie ;
- les projets ;
- les histoires émergentes.

---

# INVARIANTS

- Une activité productive autonome correspond à une opération réellement disponible.
- Une activité n'invente ni recette, ni ressource, ni produit.
- Une activité productive peut être exécutée sans qu'un système complet de carrière soit déjà implémenté.
- L'activité productive cesse d'être actionnable lorsque ses conditions réelles ne sont plus satisfaites.
- Le choix d'une activité doit rester reproductible pour un même état et une même configuration lorsque le système autonome est déterministe.

---

# RÈGLES DE CONCEPTION

Toute activité devra :

1. avoir une utilité crédible ;
2. pouvoir évoluer avec le temps ;
3. interagir avec plusieurs systèmes ;
4. respecter la liberté du joueur ;
5. enrichir le monde vivant ;
6. reposer sur des conditions réellement satisfaites lorsqu'elle devient autonome.

---

# CRITÈRE DE VALIDATION

Cette activité fournit-elle une manière crédible d'agir dans le monde, avec des conditions et conséquences réelles, plutôt qu'une simple tâche répétée ou un résultat créé artificiellement ?

Si la réponse est non, elle devra être repensée.

---

# HISTORIQUE

## Version 1.1

- en-tête mis en conformité avec MASTER-004 ;
- définition de l'activité productive exécutable ;
- distinction explicite entre activité et métier ;
- raccordement à l'opération de production de GDB-005C ;
- autorisation d'un premier lot productif autonome sans carrière, employeur ni salaire implicites.

## Version 1.0

- création du document.

---

Fin du document

Statut : Validé — Référence officielle.
