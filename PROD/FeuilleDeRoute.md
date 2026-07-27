# Chroniques --- Feuille de Route V2

> Version : 2.1
> Statut : Officiel
> Type : Roadmap
> Maturité : 2
> Bibliothèque : PROD

---

# Vision

Chroniques n'est pas simplement un jeu.

Chroniques est un moteur de simulation narratif sur lequel un jeu est construit.

Le jeu n'est que la première utilisation de ce moteur.

---

# Ce qui change par rapport à la V1

La V1 était juste sur l'architecture, mais laissait deux points implicites, désormais
tranchés par ADR-002 [réf: ADR-002] :

1. La couche de rendu et l'ordre de développement des systèmes de profondeur.
2. L'alignement de l'ordre de développement sur MASTER-005 : produire d'abord une vie
   entière jouable, avant d'ajouter la profondeur.

Le détail de ces choix techniques vit exclusivement dans ADR-002 --- il n'est pas
répété ici, pour éviter que deux documents fassent autorité sur la même décision.

Le reste de la V1 (principes, architecture en couches, data-driven, déterminisme) est
conservé.

---

# Les quatre principes

## 1. Le code suit les spécifications

Aucun module n'est développé sans être relié à une spécification existante.

CORE → ACT → Implémentation → Tests → Documentation TECH

## 2. Documentation vivante

Une fonctionnalité est terminée uniquement lorsqu'elle est spécifiée, implémentée,
testée et documentée.

## 3. Data-driven

Le moteur ne contient aucune donnée métier. Objets, PNJ, métiers, compétences, événements,
villes, bâtiments : tout est défini par des données externes. Le moteur ne connaît que
leur structure.

## 4. Déterminisme

À état identique et mêmes entrées, résultat identique.

Cela garantit sauvegardes fiables, replays, débogage, tests et futur multijoueur.

---

# Architecture générale

```
Chroniques
│
├── Simulation   (C# pur --- tout le gameplay, aucune dépendance graphique)
├── Content      (données externes --- aucune donnée codée en dur)
├── Rendering    (adaptateur Godot/C# --- lit l'état, l'affiche)
├── Tools        (éditeur, débogueur)
├── Documentation
└── Tests
```

La règle d'or : **la simulation ignore comment elle est affichée.**

Le détail de ces choix (langage, moteur de rendu, tests, sauvegarde, intégration
continue) est défini une seule fois, dans ADR-002 [réf: ADR-002]. Cette section ne
fait que rappeler la structure qui en découle, pour la lecture de la feuille de route.

---

# Couche simulation

Toute la logique de jeu vit ici, en C# pur.

Elle implémente directement les spécifications CORE, GDB et ACT.

Elle est organisée en systèmes, ajoutés progressivement selon l'ordre ci-dessous --- et
non tous en même temps.

---

# Feuille de route par versions

L'objectif directeur est le critère de sortie de la Phase 1 de MASTER-005 :
**une vie entière jouable, du premier choix au dernier.**

Les versions y mènent d'abord, puis ajoutent la profondeur.

L'ordre des versions ci-dessous suit celui des phases de MASTER-005 : Phase 3 (le
monde vivant) précède Phase 4 (la profondeur). Une version précédente de ce document
inversait cet ordre (v0.4 *La profondeur* avant v0.5 *Le monde vivant*), en
contradiction avec MASTER-005, document de rang supérieur selon MASTER-003. L'ordre
ci-dessous corrige cet écart.

## v0.1 --- Le noyau

Le Kernel technique, sans aucune règle de jeu.

- Entity, Component, State, Value
- Relation, Event
- Time, Space, Lifecycle
- World (conteneur)
- RNG déterministe à graine
- Sérialisation JSON
- Un test par loi du Kernel

Critère de sortie : le noyau tourne, tous les tests de lois passent, un World vide se
sauvegarde et se recharge à l'identique.

## v0.2 --- Un être vivant

Le strict nécessaire pour qu'un personnage existe et traverse le temps.

- Personnage (Entity + Components)
- Besoins (faim, fatigue, santé, moral)
- Cycle de vie : naître → grandir → vieillir → mourir
- Scheduler et tick temporel
- Systèmes de besoins qui évoluent avec le temps

Critère de sortie : un personnage naît, vit ses besoins année après année, et meurt.
Tout est observable sans aucun rendu.

## v0.3 --- Une vie entière

La boucle de vie complète et jouable. **Atteint le critère de Phase 1 de MASTER-005.**

- Actions (moteur ACT : Intent → Plan → Action → Outcome → Effects → Events)
- Relations sociales et mémoire relationnelle
- Compétences et apprentissage
- Première transmission de lignée (héritage minimal à la mort)
- Interface de rendu minimale sous Godot pour jouer réellement

Critère de sortie : un joueur peut vivre une vie entière, du premier choix au dernier,
et poursuivre avec un héritier.

## v0.4 --- Le monde vivant

Le monde évolue indépendamment du joueur. **Correspond à la Phase 3 de MASTER-005.**

- PNJ autonomes qui vivent leur propre vie
- Économie qui bouge seule
- Événements du monde
- Mémoire du monde

Critère de sortie : le monde évolue de façon crédible sur plusieurs générations sans
intervention du joueur.

## v0.5 --- La profondeur

Seulement maintenant, les grands systèmes de la couche Simulation. **Correspond à la
Phase 4 de MASTER-005.**

- Économie et métiers
- Santé et médecine approfondies
- Crime et justice
- Combat
- Politique, religion

Critère de sortie : trois vies radicalement différentes produisent trois histoires
également riches.

## v0.6 --- Les outils

- Éditeur de contenu (objets, métiers, événements, dialogues) sans toucher au code
- Débogueur de simulation
- Visualisation de l'état du monde

## v1.0 --- Première alpha jouable

- Boucle complète
- Sauvegarde stable et versionnée
- Équilibrage initial
- Direction artistique et interface abouties

---

# Workflow par fonctionnalité

```
Spécification → Implémentation → Tests → Documentation TECH → Validation → Intégration
```

Aucun document TECH ne décrit une fonctionnalité inexistante.

---

# Objectif long terme

Un moteur de simulation capable de faire vivre un monde dynamique où chaque personnage
agit selon ses besoins, où l'économie évolue, où les relations changent, où les
événements et les actions du joueur modifient durablement le monde.

Le jeu n'est que la première utilisation de ce moteur.

---

# Historique

## Version 2.1

- suppression de la section « Choix techniques (ADR-002) », qui reproduisait
  intégralement des décisions déjà actées dans ADR-002 sans y référer --- remplacée par
  des renvois `[réf: ADR-002]` (corrige PROD-C01, PROD-C02) ;
- inversion de v0.4 (*La profondeur*) et v0.5 (*Le monde vivant*) pour corriger une
  contradiction avec l'ordre des phases de MASTER-005, document de rang supérieur
  (corrige PROD-C03) ;
- ajout de l'en-tête conforme à MASTER-004.

## Version 2.0 (post ADR-002)

- Remplace la V1. Intègre le choix de plateforme et l'ordre aligné sur MASTER-005
  (non détaillé rétroactivement).
