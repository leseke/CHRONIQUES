# GDB-002B --- La Mémoire du Monde

> Version : 1.3
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
- **Dernière génération évaluée** ;
- **état actif / oublié** ;
- **compteurs générationnels nécessaires au palier courant** ;
- **historique traçable des transitions de palier**.

Le moteur générique ne déduit jamais le Type depuis un texte libre ou un Event.

Les données de sujet peuvent être opaques pour ENGINE tant qu'elles restent persistables et déterministes.

Un élément oublié cesse d'appartenir à la Mémoire du Monde active. Une trace technique persistante peut être conservée afin de préserver l'auditabilité ; cette trace ne doit plus influencer les règles comme un souvenir actif.

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

Le palier initial d'un nouvel élément est **Anecdote** et son état initial est **actif**.

---

# PALIERS

Les quatre paliers sont :

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

Une transition de palier et un oubli sont appliqués au maximum une fois par élément et par génération évaluée.

---

# PREUVES GÉNÉRATIONNELLES

Pour un élément actif, sa règle concrète peut fournir les preuves déterministes suivantes pour la génération évaluée :

- **liaison ou transmission qualifiante** ;
- **référence qualifiante** ;
- **influence régionale qualifiante** ;
- **contradiction qualifiante d'ampleur au moins égale** ;
- **pratique qualifiante actuellement existante**.

Chaque preuve positive doit être accompagnée d'au moins une référence de source stable.

Le moteur générique ne déduit jamais ces preuves d'une similarité de texte, d'un nombre d'Events ou d'un score implicite.

Des combinaisons incompatibles doivent être rejetées par le contrat de règle plutôt que départagées arbitrairement par ENGINE. En particulier, pour une même Légende et une même génération :

```text
pratique qualifiante
+
contradiction qualifiante
→ combinaison invalide
```

---

# ANECDOTE

Portée conceptuelle : un individu ou un petit groupe.

Une Anecdote constitue la première trace narrative retenue.

Lors de la première évaluation d'une génération strictement postérieure à sa génération de création :

```text
liaison ou transmission qualifiante ?
├── oui → Souvenir
└── non → oublié
```

Le moteur générique ne décide jamais lui-même que deux événements sont reliés.

Lors du passage à Souvenir, les compteurs de référence et d'absence sont initialisés à zéro.

---

# SOUVENIR

Portée conceptuelle : une famille ou une communauté locale.

Un Souvenir possède deux compteurs techniques :

- `générations référencées consécutives` ;
- `générations sans référence consécutives`.

À chaque nouvelle génération évaluée :

1. si une **influence régionale qualifiante** existe, le Souvenir devient immédiatement **Légende** ;
2. sinon, si une **référence qualifiante** ou une **transmission qualifiante** existe :
   - le compteur sans référence revient à `0` ;
   - le compteur référencé augmente de `1` ;
   - à `2`, le Souvenir devient **Légende** ;
3. sinon :
   - le compteur référencé revient à `0` ;
   - le compteur sans référence augmente de `1` ;
   - à `2`, le Souvenir devient **oublié**.

Le passage à Légende remet à zéro les compteurs propres au palier Souvenir.

ENGINE compte les générations ; il ne qualifie jamais lui-même une référence, une transmission ou une influence régionale.

---

# LÉGENDE

Portée conceptuelle : une région ou plusieurs communautés.

À chaque nouvelle génération évaluée :

```text
pratique qualifiante existante ?
├── oui → Tradition
└── non
    ↓
contradiction qualifiante d'ampleur au moins égale ?
├── oui → Souvenir
└── non → reste Légende
```

Une Légende ne s'efface donc jamais spontanément par simple passage du temps.

Une contradiction ne supprime pas directement l'élément : elle provoque une régression d'un seul palier vers Souvenir.

Une règle ne peut pas déclarer simultanément pratique qualifiante et contradiction qualifiante pour la même évaluation.

---

# TRADITION

Portée conceptuelle : une culture ou civilisation.

À chaque nouvelle génération évaluée :

```text
pratique qualifiante toujours existante ?
├── oui → reste Tradition
└── non → Légende
```

Une Tradition ne disparaît jamais directement.

Si elle régresse vers Légende, les règles du palier Légende ne s'appliquent qu'à partir d'une génération ultérieure : une seule transition de palier est autorisée par évaluation.

---

# ÉVALUATION GÉNÉRATIONNELLE

GDB-002B ne définit pas la durée biologique d'une génération et ne l'infère pas à partir d'un nombre fixe de Ticks.

Une **Génération de mémoire** est identifiée par un marqueur entier ordonné, stable et non négatif fourni par l'autorité/runtime de continuité générationnelle compétente.

Contraintes :

- le marqueur ne peut pas reculer ;
- un même élément n'est évalué qu'une fois pour un même marqueur ;
- les règles d'évolution s'appliquent uniquement lorsque le marqueur est strictement supérieur à la dernière génération évaluée ;
- si plusieurs générations ont été sautées entre deux exécutions, elles doivent être évaluées **une par une dans l'ordre**, sans condenser plusieurs générations en une seule transition ;
- le moteur ne transforme jamais arbitrairement `N Ticks = 1 génération`.

Tant qu'aucune autorité/runtime ne fournit un marqueur de génération suivant, les éléments de Mémoire restent persistés sans évolution de palier liée au passage générationnel.

---

# ÉVALUATION PAR RÈGLE CONCRÈTE

Chaque Type de mémoire implémentable doit fournir une règle déterministe capable au minimum :

1. de proposer les nouvelles candidates ;
2. d'interpréter son payload ;
3. de produire les preuves générationnelles applicables ;
4. d'associer des sources stables à chaque preuve positive.

Une règle peut retourner qu'aucune preuve positive n'est applicable.

ENGINE applique alors uniquement les conséquences de palier définies par le présent document.

La règle ne choisit pas directement le prochain palier : le prochain palier est déterminé par GDB-002B à partir du palier courant, des compteurs et des preuves qualifiées.

---

# SOURCES ET TRAÇABILITÉ

Toute création, promotion, régression ou oubli doit être explicable à partir :

```text
élément concerné
+
règle concrète
+
génération évaluée
+
preuves positives et leurs sources
+
compteurs avant / après lorsque nécessaires
+
transition obtenue
```

Pour l'oubli provoqué par absence de preuve, l'historique doit au minimum tracer la génération évaluée et les compteurs ayant atteint leur seuil.

---

# DÉTERMINISME

À World, élément de mémoire, règle, configuration et marqueur de génération identiques :

- la même candidate est ou non produite ;
- les mêmes preuves sont identifiées ;
- les mêmes compteurs sont obtenus ;
- la même transition de palier ou d'oubli est obtenue.

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
- Tout nouvel élément commence comme Anecdote active.
- Aucun palier n'est sauté.
- Une seule transition de palier est appliquée par élément et par génération.
- La significativité est définie par une règle concrète, jamais par ENGINE générique.
- La liaison entre faits est explicite et déterministe.
- Une génération n'est jamais déduite d'un nombre arbitraire de Ticks.
- Les générations sautées sont rejouées une par une.
- Un élément n'est évalué qu'une fois par génération.
- Une Anecdote non reliée/transmise à la génération suivante devient oubliée.
- Un Souvenir exige deux générations référencées consécutives pour devenir Légende hors influence régionale directe.
- Un Souvenir devient oublié après deux générations consécutives sans référence/transmission.
- Une Légende contradite régresse vers Souvenir ; elle ne disparaît pas directement.
- Une Tradition sans pratique régresse vers Légende ; elle ne disparaît pas directement.
- Un élément oublié n'agit plus comme mémoire active mais peut conserver une trace technique persistante.

---

# CRITÈRE DE VALIDATION

Le système peut-il créer et faire évoluer une Mémoire du Monde à partir de règles concrètes déterministes, sans que le moteur générique invente la significativité, la liaison entre événements, l'importance régionale, une pratique culturelle ou la durée d'une génération ?

Si la réponse est non, il doit être repensé.

---

# HISTORIQUE

## Version 1.3

- transitions générationnelles rendues totalement déterministes ;
- compteurs consécutifs du palier Souvenir explicités ;
- ordre exact des transitions Anecdote/Souvenir/Légende/Tradition fixé ;
- contradiction de Légende définie comme régression vers Souvenir ;
- Tradition sans pratique définie comme régression vers Légende ;
- oubli représenté comme sortie de la mémoire active avec conservation technique possible ;
- générations sautées évaluées une par une ;
- preuves positives associées à des sources stables ;
- combinaisons de preuves incompatibles interdites.

## Version 1.2

- significativité, liaison entre faits et génération rendues explicites et déléguées aux règles concrètes ;
- identité stable, Type, payload, sources et marqueurs générationnels ajoutés ;
- frontières avec GDB-002C/D explicitées.

## Version 1.1

- distinction mémoire du monde / mémoire de simulation ;
- ajout des quatre paliers et de leurs conditions conceptuelles de persistance.

## Version 1.0

- création du document.

---

Fin du document
