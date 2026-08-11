# GDB-004B --- Audit de l'autonomie décisionnelle minimale

> Version : 1.0
> Statut : Clos
> Type : Audit de concordance
> Maturité : 4
> Bibliothèque : AUDIT
> Autorité corrigée : GDB-004B v1.1

---

# 1. Objet

Vérifier si la documentation GDB permet de produire, sans invention technique, une première décision autonome déterministe pour un habitant pendant la Phase 3 de MASTER-005.

Question examinée :

```text
Entity + World + Tick
↓
décision déterministe
↓
Intent?
```

---

# 2. Documents audités

- GDB-004B --- Les Besoins des Habitants ;
- GDB-004D --- Les Personnalités ;
- GDB-004E --- Les Habitudes ;
- GDB-004F --- Les Ambitions ;
- GDB-002E --- Les Opportunités ;
- contrôle transversal de GDB-011C --- Les Décisions.

---

# 3. Constat initial

Avant correction, les documents ne permettaient pas d'implémenter une politique autonome sans interprétation.

GDB-004B affirmait que les besoins constituent un moteur principal des décisions et que les habitants établissent des priorités selon leur situation, mais ne définissait :

- ni représentation commune de satisfaction ;
- ni seuil d'activation ;
- ni règle d'urgence ;
- ni traitement des égalités ;
- ni comportement lorsqu'un besoin ne possède aucune Action exécutable ;
- ni frontière implémentable avec Personnalité, Habitudes et Ambitions.

GDB-004D, GDB-004E et GDB-004F affirmaient des influences réelles sur les choix, mais sans fournir de pondération utilisable par le moteur.

GDB-002E concernait explicitement les Opportunités proposées au joueur ; il ne pouvait donc pas être réutilisé silencieusement comme source d'Opportunités PNJ.

GDB-011C concernait les décisions conscientes du joueur et ne constituait pas une politique interne des habitants.

Conclusion initiale :

```text
ENGINE-011 interdit
```

car toute implémentation aurait inventé des règles métier absentes de la GDB.

---

# 4. Correction appliquée

GDB-004B est régénéré en version 1.1 / Maturité 2.

La correction ajoute :

- satisfaction normalisée `0..100` ;
- seuil d'activation strict ;
- notion de besoin actionnable ;
- interdiction de produire un faux Intent lorsqu'aucune réponse exécutable n'existe ;
- urgence de base monotone selon la satisfaction ;
- départage déterministe des égalités ;
- frontières explicites avec Personnalité, Habitudes, Ambitions et Opportunités ;
- premier contrat autonome implémentable :

```text
Fatigue sous seuil configurable
↓
Intent se_reposer
```

Le seuil numérique exact reste un paramètre d'équilibrage et n'est pas figé par la GDB.

---

# 5. Pourquoi les autres documents ne sont pas modifiés

GDB-004D, GDB-004E et GDB-004F n'ont pas besoin d'être artificiellement enrichis pour ce premier lot.

Leur influence future est reconnue par GDB-004B, mais aucune formule ne leur est attribuée par anticipation.

GDB-002E reste inchangé car son périmètre joueur est cohérent avec son propre objectif. Une éventuelle notion d'Opportunité PNJ devra être proposée explicitement plus tard.

GDB-011C reste inchangé car il décrit correctement les décisions du joueur.

---

# 6. État après correction

Après GDB-004B v1.1, le premier lot suivant devient spécifiable :

```text
Entity
+
NeedsComponent
+
seuil configuré
↓
Intent? se_reposer
```

Cette possibilité est volontairement plus étroite qu'une IA générale.

Elle suffit pour produire une première implémentation réelle de `IAutonomousIntentSource` sans inventer :

- des traits de personnalité ;
- des habitudes ;
- des ambitions ;
- des Opportunités PNJ ;
- un catalogue complet de Verbes ;
- une pondération multi-objectifs.

---

# 7. Décision

Le constat est clos.

```text
GDB insuffisante
↓
GDB-004B v1.1
↓
Maturité 2
↓
ENGINE-011 autorisé
```

---

# 8. Condition de réouverture

Cet audit devra être complété ou un nouveau constat ouvert lorsque le moteur cherchera à arbitrer réellement plusieurs sources concurrentes d'Intent, notamment :

- plusieurs besoins simultanément actionnables ;
- personnalité ;
- habitudes ;
- ambitions ;
- opportunités perçues par des PNJ.

Ces futurs besoins ne remettent pas en cause la validité du premier contrat `Fatigue → se_reposer`.

---

Fin du document
