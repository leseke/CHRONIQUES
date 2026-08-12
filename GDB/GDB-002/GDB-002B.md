# GDB-002B --- La Mémoire du Monde

> Version : 1.2
> Statut : Officiel
> Type : Fondations du Gameplay
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir un modèle de Mémoire du Monde implémentable sans que le moteur générique décide seul ce qui est significatif, relié, transmis, régional ou traditionnel.

La Mémoire du Monde conserve un sous-ensemble narratif du passé afin que les générations suivantes héritent d'un monde qui possède réellement une histoire.

---

# PRINCIPE

```text
fait de simulation réel
↓
règle de mémoire concrète
↓
qualification éventuelle
↓
élément de Mémoire du Monde
↓
évolution générationnelle déterministe
```

Le monde peut se souvenir ; il ne mémorise pas automatiquement tout ce qui arrive.

La Mémoire du Monde est sélective, persistante et explicable.

---

# FRONTIÈRE AVEC LA MÉMOIRE DE SIMULATION

La mémoire de simulation est l'état technique nécessaire au fonctionnement du World : State, Components, Events et autres données persistées par le moteur.

La Mémoire du Monde est un sous-ensemble narratif curaté.

```text
mémoire de simulation
≠
Mémoire du Monde
```

Un Event de simulation peut être une source d'un souvenir, mais il ne devient jamais automatiquement un souvenir.

Une règle concrète doit explicitement reconnaître qu'un fait satisfait ses conditions de mémorisation.

ENGINE ne doit donc jamais scanner `World.Events` et appliquer un seuil universel implicite.

---

# TYPES DE FAITS POSSIBLES

Peuvent notamment fournir la matière d'une règle de mémoire :

- construction majeure ;
- destruction importante ;
- découverte remarquable ;
- événement historique ;
- famille influente ;
- œuvre durable ;
- transformation du paysage ;
- autre fait explicitement autorisé par une règle de mémoire concrète.

Cette liste est conceptuelle.

**Elle ne constitue pas un catalogue de Types directement implémentables.**

---

# ÉLÉMENT DE MÉMOIRE

Chaque élément de Mémoire du Monde possède au minimum :

- **Identifiant stable** : distingue cet élément de tout autre ;
- **Type de mémoire** : identifie la règle concrète qui sait l'évaluer ;
- **Palier courant** ;
- **Sujet / données de mémoire** : payload persistant interprété uniquement par sa règle ;
- **Sources identifiables** : références aux faits de simulation ayant justifié sa création ou ses évolutions ;
- **Génération de création** ;
- **Dernière génération évaluée**.

Le moteur générique ne déduit jamais le Type depuis un texte libre ou un Event.

Les données de sujet peuvent être opaques pour ENGINE tant qu'elles restent persistables et déterministes.

---

# CRÉATION

Un élément n'est créé que si une règle de mémoire concrète produit une candidate valide.

La règle est responsable de déterminer :

1. si le fait est suffisamment significatif dans son contexte ;
2. quel Type de mémoire s'applique ;
3. quel sujet ou payload doit être conservé ;
4. quelles sources de simulation justifient la création ;
5. quelle portée initiale est concernée ;
6. l'identifiant stable de l'élément.

Il n'existe donc **aucun seuil universel de significativité** dans GDB-002B.

```text
règle concrète absente
→ aucun nouvel élément de Mémoire du Monde
```

Une même identité stable ne peut pas être créée deux fois.

Le palier initial d'un nouvel élément est **Anecdote**.

---

# PALIERS

Les quatre paliers restent :

```text
Anecdote
↓
Souvenir
↓
Légende
↓
Tradition
```

Un élément ne progresse ou ne régresse que d'un palier à la fois lors d'une même évaluation générationnelle.

Aucun saut direct `Anecdote → Légende`, `Souvenir → Tradition` ou équivalent n'est autorisé.

---

# ANECDOTE

Portée conceptuelle : un individu ou un petit groupe.

Une Anecdote constitue la première trace narrative retenue.

À l'évaluation de la génération suivante :

- elle devient **Souvenir** si sa règle concrète fournit une preuve déterministe de liaison à au moins un autre fait mémorisé **ou** de transmission qualifiante ;
- sinon elle disparaît.

Le moteur générique ne décide jamais lui-même que deux événements « se ressemblent » ou sont « reliés ».

La relation doit être produite explicitement par la règle compétente à partir d'identifiants réels.

---

# SOUVENIR

Portée conceptuelle : une famille ou une communauté locale.

Un Souvenir peut devenir **Légende** si sa règle concrète établit l'un des faits suivants :

- il reste effectivement référencé pendant deux générations évaluées ;
- il influence un fait qualifié d'ampleur régionale par une autorité concrète.

Un Souvenir s'efface après deux générations évaluées consécutives sans nouvelle référence ni transmission qualifiante.

ENGINE compte les évaluations générationnelles ; il ne qualifie pas lui-même une référence, une transmission ou une influence régionale.

---

# LÉGENDE

Portée conceptuelle : une région ou plusieurs communautés.

Une Légende ne s'efface pas spontanément par simple passage du temps.

Elle peut :

- rester Légende ;
- devenir Tradition si une règle concrète établit qu'elle a donné naissance à une pratique qualifiante répétée ;
- être révisée ou déclassée uniquement si une règle concrète identifie un fait contradictoire d'ampleur au moins égale.

La notion d'ampleur comparable appartient à la règle concrète concernée ; ENGINE ne calcule aucun score universel d'importance.

---

# TRADITION

Portée conceptuelle : une culture ou civilisation.

Une Tradition correspond à une Légende ayant produit une pratique durable explicitement identifiable : rite, fête, coutume, institution ou autre pratique autorisée.

Elle demeure Tradition tant que la règle concrète confirme l'existence de cette pratique.

Si la pratique cesse d'exister, l'élément peut régresser d'un seul palier vers Légende lors d'une évaluation générationnelle.

La suppression immédiate d'une Tradition sans passage par Légende n'est pas autorisée.

---

# ÉVALUATION GÉNÉRATIONNELLE

GDB-002B ne définit pas la durée biologique d'une génération et ne l'infère pas à partir d'un nombre fixe de Ticks.

Une **Génération de mémoire** est identifiée par un marqueur ordonné et stable fourni par l'autorité de continuité générationnelle compétente.

Contraintes :

- le marqueur ne peut pas reculer ;
- un même élément n'est évalué qu'une fois pour un même marqueur ;
- les règles d'évolution s'appliquent uniquement lorsque le marqueur passe à une génération ultérieure ;
- le moteur ne transforme jamais arbitrairement `N Ticks = 1 génération`.

Tant qu'aucune autorité/runtime ne fournit un marqueur de génération suivant, les éléments de Mémoire restent persistés sans évolution de palier liée au passage générationnel.

Cette règle permet un premier stockage de Mémoire avant l'intégration complète de toutes les transitions générationnelles.

---

# ÉVALUATION PAR RÈGLE CONCRÈTE

Chaque Type de mémoire implémentable doit fournir une règle déterministe capable au minimum :

1. de proposer les nouvelles candidates ;
2. d'interpréter son payload ;
3. d'identifier les faits de liaison ou transmission applicables ;
4. d'identifier les références qualifiantes ;
5. d'identifier une éventuelle influence régionale ;
6. d'identifier une contradiction qualifiante ;
7. d'identifier l'existence ou la disparition d'une pratique pour les Traditions.

Une règle peut retourner qu'aucun de ces faits n'est applicable.

ENGINE applique alors uniquement les conséquences de palier définies par le présent document.

---

# SOURCES ET TRAÇABILITÉ

Toute création, promotion, régression, révision ou suppression doit être explicable à partir :

```text
élément concerné
+
règle concrète
+
génération évaluée
+
sources / preuves identifiables
```

Une transition sans cause identifiable est interdite, sauf la disparition prévue d'une Anecdote ou d'un Souvenir après absence qualifiée de références pendant les fenêtres définies.

Même dans ces cas, l'absence est constatée lors d'une évaluation générationnelle explicite.

---

# DÉTERMINISME

À World, élément de mémoire, règle, configuration et marqueur de génération identiques :

- la même candidate est ou non produite ;
- les mêmes preuves sont identifiées ;
- la même transition de palier est obtenue.

Aucun bruit aléatoire implicite n'est requis.

---

# FRONTIÈRE AVEC GDB-002C

GDB-002C décrit la philosophie des conséquences du monde.

Il ne constitue pas un algorithme de significativité pour la Mémoire du Monde.

Une conséquence ne devient un souvenir que lorsqu'une règle de mémoire concrète la qualifie explicitement.

---

# FRONTIÈRE AVEC GDB-002D

GDB-002D décrit la philosophie des événements dynamiques.

Un événement dynamique peut devenir source de Mémoire, mais GDB-002D ne fournit pas à lui seul une règle automatique de mémorisation.

---

# FRONTIÈRE AVEC LA LIGNÉE

La Mémoire du Monde survit aux individus et peut traverser plusieurs générations.

Elle n'est pas attachée au personnage contrôlé ni détruite lors d'un changement d'héritier.

La continuité d'un personnage vers son héritier peut fournir un marqueur générationnel lorsque l'autorité technique correspondante le prévoit, mais GDB-002B ne suppose pas que toute mort ou tout héritage universel équivaut automatiquement à une nouvelle génération de mémoire.

---

# RÈGLES DE CONCEPTION

Toute mécanique liée à la Mémoire du Monde doit :

1. préserver les performances ;
2. conserver uniquement les éléments explicitement qualifiés ;
3. renforcer la continuité ;
4. favoriser les histoires émergentes ;
5. rester compréhensible ;
6. conserver une cause traçable ;
7. ne jamais inventer un score universel de significativité.

---

# INVARIANTS

- La Mémoire du Monde est distincte de la mémoire de simulation.
- Un Event ne devient jamais automatiquement un souvenir.
- Tout élément possède une identité stable, un Type, un palier, des données, des sources et des marqueurs générationnels.
- Tout nouvel élément commence comme Anecdote.
- Aucun palier n'est sauté.
- La significativité est définie par une règle concrète, jamais par ENGINE générique.
- La liaison entre faits est explicite et déterministe.
- Une génération n'est jamais déduite d'un nombre arbitraire de Ticks.
- Un élément n'est évalué qu'une fois par génération.
- Les transitions de palier sont déterministes et traçables.
- Une Tradition régresse vers Légende avant toute disparition éventuelle.

---

# CRITÈRE DE VALIDATION

Le système peut-il créer et faire évoluer une Mémoire du Monde à partir de règles concrètes déterministes, sans que le moteur générique invente la significativité, la liaison entre événements, l'importance régionale, une pratique culturelle ou la durée d'une génération ?

Si la réponse est non, il doit être repensé.

---

# HISTORIQUE

## Version 1.2

- correction de l'ambiguïté du « seuil de significativité » : qualification déléguée aux Types/règles concrètes ;
- identité stable, Type, payload, sources et marqueurs générationnels explicités ;
- liaison entre événements rendue explicite et déterministe ;
- définition d'une évaluation générationnelle sans conversion implicite Tick → génération ;
- règles de promotion/régression précisées sans saut de palier ;
- frontière avec GDB-002C/D explicitée ;
- conservation des quatre paliers Anecdote → Souvenir → Légende → Tradition.

## Version 1.1

- distinction mémoire du monde / mémoire de simulation ;
- ajout des quatre paliers et de leurs conditions conceptuelles de persistance.

## Version 1.0

- création du document.

---

Fin du document
