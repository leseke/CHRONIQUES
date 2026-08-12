GDB-004E --- Les Habitudes

Version : 1.1
Statut : Officiel
Type : Population du Monde
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir les principes qui gouvernent les habitudes des habitants de
Chroniques, avec une précision suffisante pour être implémentées sans
interprétation (MASTER-007, Maturité 2).

Les habitudes rendent les comportements cohérents, prévisibles sans être
répétitifs, et donnent l'impression d'un monde vivant.
⸻
PRINCIPE

Chaque habitant développe des habitudes au fil du temps.

Elles résultent de son mode de vie, de sa personnalité, de son métier et
de son environnement.
⸻
DÉFINITION

Une Habitude est une règle de comportement acquise : lorsque le
contexte correspond à son déclencheur, l'habitant produit un Intent
spécifique sans passer par l'évaluation complète de ses besoins ou
ambitions. Elle réduit le coût cognitif de la décision pour les
situations familières.

Une Habitude n'est jamais un script imposé. Elle constitue une
suggestion prioritaire que les besoins urgents ou une perturbation
suffisante peuvent interrompre.
⸻
MODÈLE

Chaque Habitude d'un habitant possède cinq attributs :

- **Déclencheur.** La condition contextuelle minimale qui rend l'Habitude
  candidate : un moment de la journée, une saison, un lieu, une
  relation présente, un seuil de besoin atteint. Le déclencheur est
  toujours une donnée vérifiable dans le World à l'instant du Tick.
  Il ne peut jamais être « toujours » (ce serait un Intent permanent,
  pas une Habitude).

- **Intent produit.** L'objectif que l'Habitude soumet au pipeline ACT
  si elle est activée. Il suit le même contrat qu'un Intent ordinaire :
  un acteur, un objectif, une priorité. L'Habitude ne produit jamais
  directement une Action Instance --- elle alimente ACT comme toute
  autre source d'Intent [réf: GDB-004B, ACT-002].

- **Force.** Valeur continue bornée entre 0 et 100. Elle exprime la
  solidité de l'Habitude : à Force élevée, l'Habitude est candidate
  dès que son déclencheur est satisfait ; à Force basse, elle ne se
  manifeste que si aucune autre source d'Intent ne produit de résultat
  exécutable. La Force ne représente jamais une durée ni une
  fréquence --- seulement la priorité relative de l'Habitude face aux
  autres sources d'Intent.

- **Tick de dernière activation.** Le Tick auquel l'Habitude a
  produit un Intent pour la dernière fois, qu'il ait été exécuté avec
  succès ou non. Sert exclusivement au calcul de l'érosion (voir
  ÉVOLUTION).

- **Tick de création.** Le Tick auquel l'Habitude a été formée.
  Sert au tie-break déterministe (voir ARBITRAGE).
⸻
FORMATION

Une Habitude se forme lorsqu'un même Intent est produit dans un contexte
similaire un nombre de fois suffisant, sur une fenêtre temporelle
suffisante. Les deux seuils (nombre de répétitions, fenêtre en Ticks)
ne sont pas fixés par ce document --- ce sont des paramètres
d'équilibrage, comme les seuils de besoins dans GDB-004B.

Une Habitude formée démarre à une Force initiale modérée --- elle
n'est jamais immédiatement aussi solide qu'une habitude de longue date.
La valeur exacte de la Force initiale est un paramètre d'équilibrage.
⸻
ÉVOLUTION

La Force d'une Habitude évolue selon deux mécanismes distincts, à
distinguer strictement :

1. **Renforcement.** Chaque fois que le déclencheur est satisfait et
   que l'Intent produit est exécuté avec succès, la Force augmente d'un
   montant fixe. Le gain décroît à mesure que la Force approche 100 ---
   une Habitude très ancrée se consolide plus lentement qu'une jeune
   Habitude en formation (même logique que GDB-004H, MODÈLE DE
   PROGRESSION des Compétences).

2. **Érosion.** En l'absence d'activation dépassant un seuil d'inactivité
   (exprimé en Ticks), la Force diminue progressivement. L'érosion cesse
   dès qu'une nouvelle activation a lieu. Une Habitude dont la Force
   atteint 0 disparaît.

La Force reste toujours bornée entre 0 et 100 (Clamp).

PERTURBATION --- Un événement d'ampleur suffisante [réf: GDB-002B, seuils
de significativité ; GDB-004D, Inflexion] peut modifier le déclencheur
d'une Habitude, réduire fortement sa Force ou la supprimer directement.
Ce mécanisme garantit que les habitudes évoluent avec l'histoire de
l'individu plutôt que de devenir des comportements figés. La perturbation
est toujours causée par un fait identifiable, jamais par une dérive
silencieuse (invariant partagé avec GDB-004D).
⸻
ARBITRAGE AVEC LES AUTRES SOURCES D'INTENT

Une Habitude est une source d'Intent parmi d'autres. Son activation suit
l'ordre général de priorité défini par GDB-004B et GDB-004A :

```
besoins physiologiques urgents (GDB-004B)
↓
transfert volontaire exécutable (GDB-004A)
↓
activité productive exécutable (GDB-004A)
↓
Habitudes actives
↓
Ambitions (GDB-004F)
↓
aucun Intent
```

Les Habitudes se situent donc après les besoins urgents et les
opportunités économiques immédiates --- conformément à GDB-004A, qui
établit que l'entretien précède toujours le travail ou l'échange.

Lorsque plusieurs Habitudes sont simultanément candidates (déclencheur
satisfait et Force non nulle), la priorité suit :

1. Force la plus élevée.
2. En cas d'égalité de Force : Habitude créée au Tick le plus bas
   (la plus ancienne).

Ce tie-break est déterministe. Il ne constitue pas une hiérarchie
narrative entre Habitudes.
⸻
FRONTIÈRE AVEC GDB-004D (PERSONNALITÉS)

La personnalité influence la formation des Habitudes (elle peut
accélérer ou ralentir le seuil de répétition nécessaire, ou rendre
certains déclencheurs plus sensibles) mais elle ne définit pas elle-même
les Habitudes. GDB-004D reste l'autorité sur les traits ; GDB-004E
reste l'autorité sur les Habitudes comme comportements acquis par
la répétition.
⸻
FRONTIÈRE AVEC GDB-004F (AMBITIONS)

Une Ambition est une direction de vie durable ; une Habitude est un
comportement contextuel acquis. Une Habitude peut avoir été formée en
réponse à une Ambition (répéter une activité productive parce qu'on
aspire à en devenir expert), mais elle ne représente pas l'Ambition
elle-même. GDB-004F reste l'autorité sur les directions de vie ;
GDB-004E sur les comportements routiniers.
⸻
IMPACT

Les habitudes influencent :

- les rencontres ;
- l'économie locale ;
- les routines des villes ;
- les opportunités offertes au joueur ;
- la crédibilité des comportements autonomes.
⸻
PARAMÈTRES D'IMPLÉMENTATION

Les valeurs suivantes ne sont pas fixées par ce document : seuil de
répétitions pour formation, fenêtre temporelle de formation, Force
initiale, montant de renforcement par succès, taux d'érosion par Tick
inactif, seuil d'inactivité déclenchant l'érosion, amplitude minimale
d'un événement pour perturber une Habitude. Même posture que
GDB-004C, GDB-004H : le modèle est fixé, les constantes restent des
paramètres d'équilibrage.
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée aux habitudes devra :

1. rester cohérente avec la personnalité ;
2. évoluer progressivement ;
3. éviter les routines artificielles ;
4. enrichir l'immersion ;
5. favoriser les histoires émergentes.
⸻
CRITÈRE DE VALIDATION

Cette mécanique donne-t-elle l'impression que les habitants vivent
selon leurs propres habitudes plutôt que selon des scripts visibles ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : passage en Maturité 2. Ajout du MODÈLE (cinq attributs :
Déclencheur, Intent produit, Force 0-100, Tick de dernière activation,
Tick de création), des règles de FORMATION (seuils paramétrisés, Force
initiale modérée), d'ÉVOLUTION (renforcement décroissant, érosion par
inactivité, perturbation par événement significatif), d'ARBITRAGE (place
des Habitudes dans la chaîne GDB-004A/B, tie-break déterministe par
Force puis ancienneté), et des frontières explicites avec GDB-004D
(Personnalités) et GDB-004F (Ambitions). Section PARAMÈTRES
D'IMPLÉMENTATION ajoutée. En-tête mis en conformité avec MASTER-004
(Maturité et Bibliothèque absents de la v1.0).

Version 1.0 : création du document.
