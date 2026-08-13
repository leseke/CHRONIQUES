# GDB-008D --- Les Générations

> Version : 1.1
> Statut : Officiel
> Type : Temps & Générations
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir une notion de génération suffisamment précise pour porter la continuité d'une Chronique sans transformer chaque décès du World en changement de génération global.

---

# PRINCIPE

Chaque génération hérite d'un monde façonné par celles qui l'ont précédée.

Elle reçoit un héritage, mais reste libre de suivre son propre chemin.

La génération utilisée pour la continuité d'une Chronique est **locale à une continuité de lignée identifiée**.

```text
continuité de lignée L
+
personnage courant A
↓
transmission valide A → B
↓
B devient le nouveau porteur de la continuité L
↓
index de génération de L + 1
```

Il n'existe pas de compteur biologique universel avançant à chaque mort du World.

---

# CONTINUITÉ DE LIGNÉE

Une continuité générationnelle possède au minimum :

- un identifiant stable de continuité ;
- un index de génération entier non négatif ;
- l'identifiant de l'individu actuellement porteur de cette continuité ;
- l'historique identifiable des transmissions ayant fait avancer cet index.

L'index initial est paramétrable par la création de la continuité ; la convention de travail minimale est `0`.

Deux continuités distinctes peuvent coexister dans le même World et évoluer indépendamment.

---

# FRONTIÈRE DE GÉNÉRATION

Une génération de continuité n'avance que lorsqu'une transmission **valide et effectivement adoptée par cette continuité** remplace son porteur courant par un successeur existant.

Pour la continuité suivie par `LifeSession`, la frontière correspond donc au même résultat déjà utilisé pour transférer le contrôle :

```text
heritage.transmission
source = porteur courant décédé
target = héritier existant
+
LifeSession adopte target comme nouveau personnage actif
```

Alors seulement :

```text
GenerationIndex += 1
CurrentMemberId = target
```

Ne font pas avancer l'index :

- la mort d'un autre habitant ;
- une transmission concernant une autre lignée ;
- un ancien Event de transmission ;
- une transmission dont la cible n'existe pas ;
- une absence de successeur ;
- une session déjà terminée ;
- un simple passage de Tick.

---

# HÉRITAGE

Une génération peut recevoir notamment :

- des connaissances ;
- des compétences ;
- un patrimoine ;
- une réputation ;
- des relations ;
- des traditions ;
- des souvenirs.

Rien n'est transmis automatiquement dans son intégralité.

`GDB-004J` reste l'autorité sur la désignation individuelle de l'héritier et les cas d'échec de transmission.

---

# UNE IDENTITÉ PROPRE

Chaque génération développe sa propre personnalité et son propre parcours.

Elle peut poursuivre l'œuvre de ses ancêtres, la transformer ou créer une nouvelle voie.

L'index de génération n'est donc jamais un score de puissance, d'âge ou de mérite. Il représente uniquement la position ordonnée d'un porteur dans une continuité donnée.

---

# DÉTERMINISME

À continuité, porteur courant et résultat de transmission identiques :

- la même frontière de génération est reconnue ;
- le même successeur devient porteur ;
- l'index augmente exactement d'une unité.

Aucun nombre de Ticks ne constitue implicitement une génération.

---

# FRONTIÈRE AVEC GDB-002B

`GDB-002B` utilise un marqueur générationnel fourni par une autorité de continuité.

Le marqueur défini ici peut servir à cette évaluation **lorsqu'une Mémoire du Monde est configurée pour suivre cette continuité de Chronique/lignée**.

Il ne signifie pas que toutes les familles du World changent biologiquement de génération au même instant.

---

# FRONTIÈRE AVEC GDB-008G

`GDB-008G` décrit ce qu'une génération peut transmettre à la suivante.

Le présent document définit uniquement la frontière ordonnée entre deux générations d'une même continuité.

---

# FRONTIÈRE AVEC GDB-008I

`GDB-008I` décrit l'observation de la Mémoire du Monde à travers ces transmissions de lignée.

Une Mémoire peut donc être évaluée au passage d'un index de continuité `N` vers `N+1` sans inventer de compteur temporel global.

---

# RÈGLES DE CONCEPTION

Toute mécanique liée aux générations doit :

1. préserver la liberté des descendants ;
2. valoriser l'héritage sans le rendre obligatoire ;
3. créer des conséquences durables ;
4. respecter l'évolution naturelle du monde ;
5. distinguer clairement continuité de lignée et mortalité globale du World ;
6. ne jamais convertir implicitement un nombre de Ticks en génération.

---

# INVARIANTS

- Une continuité possède une identité stable.
- Son index est entier et non négatif.
- L'index ne recule jamais.
- Une transmission adoptée fait avancer l'index d'exactement `+1`.
- Un même passage A → B ne peut être compté deux fois.
- La mort d'un tiers n'avance pas la continuité.
- Une absence de successeur n'avance pas la continuité.
- Plusieurs continuités peuvent coexister indépendamment.
- Il n'existe aucun compteur global « une mort = une génération ».

---

# CRITÈRE DE VALIDATION

La mécanique permet-elle de suivre plusieurs passages générationnels d'une même Chronique de manière déterministe, sans confondre la succession de cette lignée avec les décès simultanés du reste du World ?

Si la réponse est non, elle doit être repensée.

---

# HISTORIQUE

## Version 1.1

- passage en Maturité 2 ;
- définition d'une continuité de lignée identifiée ;
- définition déterministe de la frontière de génération par transmission valide effectivement adoptée ;
- interdiction de « une mort = une génération » et de `N Ticks = une génération` ;
- compatibilité explicite avec GDB-002B, GDB-004J, GDB-008G et GDB-008I.

## Version 1.0

- création du document.

---

Fin du document
