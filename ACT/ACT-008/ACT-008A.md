# ACT-008-A — Familles de verbes

> Version : 1.0
>
> Statut : Proposition
>
> Type : Contrat d'architecture
>
> Maturité : 2
>
> Bibliothèque : ACT
>
> Dépendances :
> - ACT-001-G, section 13 (critères d'entrée d'une mécanique dans ACT)
> - ACT-002-A (Mission du modèle universel)
> - ACT-002-B (Niveaux d'abstraction --- Principe, Pattern, Verbe, Action)
> - ACT-002-C, sections 3, 4 et 8 (Relations autorisées, Spécialisation,
>   Relations interdites)
>
> Utilisé par :
> - GDB (future bibliothèque VERBS)
> - TECH
> - QA

---

# 1. Objectif

Définir les règles d'organisation des Verbes en familles partageant un
même Pattern, et les critères permettant de décider si un besoin
justifie un nouveau Verbe plutôt que la réutilisation d'un Verbe
existant.

Ce document n'introduit aucun nouvel axiome. ACT-002-B définit déjà ce
qu'est un Verbe (« une capacité exprimable [...] l'interface entre une
mécanique abstraite et une action exécutable ») et ACT-002-C établit déjà
la relation de spécialisation Pattern → Verbe. Aucun des deux ne définit
comment plusieurs Verbes cohabitent sous un même Pattern, ni quand créer
un nouveau Verbe plutôt qu'en réutiliser un existant --- c'est l'objet de
ce document.

Ce document ne contient et ne contiendra jamais l'énumération des
Verbes concrets du jeu : cette responsabilité appartient à la future
bibliothèque VERBS (ACT/CATALOG.md), pilotée par GDB. ACT-008 définit
uniquement les règles que cette bibliothèque devra respecter.

---

# 2. Principe

Un Pattern est generique par construction (ACT-002-B, section 5 : « Le
Pattern reste indépendant des acteurs, des objets et du contexte »). Un
même Pattern peut donc être spécialisé par plusieurs Verbes distincts,
chacun l'exprimant différemment --- c'est ce que ce document appelle une
**famille de Verbes**.

---

# 3. Multiplicité

Un Verbe spécialise toujours exactement un Pattern (ACT-002-C, section 4
--- la chaîne de spécialisation ne se ramifie jamais vers le haut,
section 8 : « un Pattern ne dépend jamais d'une Action »).

Un Pattern peut être spécialisé par zéro, un, ou plusieurs Verbes. Deux
Verbes d'une même famille (même Pattern) partagent la même structure de
contrat --- les mêmes catégories d'Inputs, de Preconditions et
d'Effects attendus (ACT-002-E) --- mais peuvent différer sur leurs
valeurs concrètes de Constraints et de Costs (ACT-002-E, sections 5 et
6). Exemple : un Pattern « Déplacement terrestre » spécialisé par
« Marcher » et « Courir » --- même structure de contrat (un Acteur, une
destination, un coût en énergie), Constraints différentes (vitesse,
distance maximale).

---

# 4. Critère de nouveau Verbe

Avant de créer un nouveau Verbe, la bibliothèque VERBS doit vérifier,
dans l'ordre :

1. **Paramétrage.** Le besoin peut-il être couvert par un Verbe
   existant, avec des valeurs différentes de Constraints ou de Costs ?
   Si oui, aucun nouveau Verbe n'est créé.
2. **Composition.** Le besoin peut-il être couvert par une composition
   de Verbes existants (ACT-009) ? Si oui, aucun nouveau Verbe n'est
   créé.
3. **Pattern existant.** Le besoin correspond-il à un Pattern déjà
   spécialisé par d'autres Verbes, mais sous un angle non couvert ? Si
   oui, un nouveau Verbe rejoint la famille existante.
4. **Nouveau Pattern.** Seul un besoin ne correspondant à aucun Pattern
   existant justifie la création d'un nouveau Pattern --- et par
   conséquent d'un nouveau Verbe fondateur de cette famille.

Ces quatre tests reprennent l'esprit des critères d'entrée d'une
mécanique dans ACT (ACT-001-G, section 13), appliqués spécifiquement au
niveau Verbe plutôt qu'au niveau des chapitres ACT eux-mêmes.

---

# 5. Polysémie interdite

Un Verbe n'appartient jamais qu'à une seule famille (un seul Pattern).
Deux usages apparemment proches d'un même mot (ex. : « Construire » un
bâtiment contre « Construire » une réputation) ne sont jamais un seul
Verbe polysémique --- ce sont deux Verbes distincts, appartenant chacun
à sa propre famille, qui peuvent partager un nom proche dans le
vocabulaire GDB sans jamais partager de contrat.

---

# 6. Contrat

Un Verbe ne peut jamais spécialiser plus d'un Pattern.

Deux Verbes d'une même famille partagent toujours la même structure de
contrat --- jamais deux structures différentes pour un même Pattern.

La création d'un nouveau Verbe ne peut jamais court-circuiter les
quatre tests de la section 4 dans leur ordre.

---

# 7. Contrat TECH

Le moteur doit être capable de :

- rattacher tout Verbe implémenté à exactement un Pattern ;
- garantir qu'un même Pattern implémenté par plusieurs Verbes expose la
  même structure de contrat (mêmes catégories d'Inputs/Preconditions/
  Effects), quelles que soient les valeurs propres à chaque Verbe.

---

# 8. Contrat QA

Les tests devront vérifier :

✓ qu'aucun Verbe catalogué (VERBS) ne référence plus d'un Pattern ;

✓ que deux Verbes d'une même famille exposent une structure de contrat
identique, même avec des valeurs différentes ;

✓ qu'aucune paire de Verbes ne partage un nom identique sans partager
aussi un Pattern (la polysémie de nom sans polysémie de Pattern est
permise --- section 5 --- mais jamais l'inverse).

---

# 9. Critères de validation

Ce document est conforme si :

✓ il n'introduit aucun axiome déjà posé par ACT-002-A, B ou C ;

✓ il ne redéfinit aucune règle déjà couverte par ACT-002-E (Action
Contract) ;

✓ il n'énumère aucun Verbe concret --- cette responsabilité appartient
à VERBS, pilotée par GDB ;

✓ les quatre tests de la section 4 couvrent tout besoin, sans laisser
de cas ambigu entre « paramétrage » et « nouveau Pattern ».

---

# 10. Historique

## Version 1.0

- Création du document. Élabore ACT-002-B et ACT-002-C avec des règles
  de multiplicité Pattern/Verbe, un critère de nouveau Verbe en quatre
  tests, et une règle de non-polysémie, absentes des deux documents
  source. Statut Proposition : n'a pas encore traversé les étapes
  Validée/Spécifiée du cycle de vie documentaire d'une mécanique
  (ACT-001-G, section 14).
