# GDB-008G --- L'Héritage

> Version : 1.2
> Statut : Officiel
> Type : Temps & Générations
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir la portée générationnelle de l'héritage dans Chroniques, en cohérence avec la frontière de génération de `GDB-008D` et le mécanisme individuel de `GDB-004J`.

---

# FRONTIÈRE AVEC GDB-004J

`GDB-004J` fait autorité sur :

- la désignation de l'héritier ;
- la transmission entre un défunt et son successeur ;
- les cas d'échec : absence, refus, transmission incomplète.

Le présent document ne redéfinit jamais cet algorithme.

---

# FRONTIÈRE AVEC GDB-008D

`GDB-008D` fait autorité sur la **continuité générationnelle**.

Une transmission individuelle ne devient une frontière de génération pour une continuité donnée que si cette continuité adopte effectivement le successeur comme nouveau porteur.

```text
GDB-004J
→ héritier valide A → B

GDB-008D
→ continuité L adopte B
→ génération L + 1
```

Une transmission concernant une autre lignée n'avance pas automatiquement la continuité L.

---

# PRINCIPE

Un héritage n'est jamais une copie parfaite du passé.

Il constitue une base sur laquelle la génération suivante peut s'appuyer, évoluer ou prendre une direction différente.

---

# CE QUI PEUT ÊTRE TRANSMIS

Un héritage peut comprendre :

- patrimoine ;
- connaissances ;
- compétences ;
- réputation ;
- traditions ;
- relations ;
- œuvres ;
- souvenirs au sens de `GDB-002B`.

Chaque domaine conserve ses propres règles de transmission.

---

# LIBERTÉ DES DESCENDANTS

Recevoir un héritage n'oblige jamais à reproduire les choix des générations précédentes.

Chaque descendant reste libre d'honorer, transformer ou abandonner cet héritage.

---

# PORTÉE GÉNÉRATIONNELLE

Le passage générationnel ne copie pas automatiquement l'intégralité des Components du porteur précédent vers le suivant.

Le marqueur de génération indique uniquement qu'une continuité identifiée est passée d'un porteur à son successeur.

Toute donnée réellement transmise doit rester couverte par son autorité métier propre.

---

# DÉTERMINISME

À même continuité et même transmission adoptée :

- le même passage générationnel est reconnu ;
- il n'est reconnu qu'une fois ;
- aucune autre transmission du World n'est implicitement agrégée à cette continuité.

---

# RÈGLES DE CONCEPTION

Toute mécanique liée à l'héritage doit :

1. respecter la liberté du successeur ;
2. valoriser la transmission ;
3. créer des conséquences à long terme ;
4. éviter les bonus automatiques excessifs ;
5. renforcer la continuité du monde ;
6. distinguer la transmission individuelle de `GDB-004J` de l'avancement d'une continuité générationnelle de `GDB-008D`.

---

# INVARIANTS

- Une transmission individuelle n'est pas automatiquement un changement de génération global.
- Une continuité n'avance que lorsqu'elle adopte effectivement un successeur.
- Un passage générationnel n'implique aucune copie automatique de données métier.
- Les souvenirs transmis restent gouvernés par `GDB-002B`.

---

# CRITÈRE DE VALIDATION

Cette mécanique assure-t-elle une continuité générationnelle traçable sans transformer l'héritage en copie automatique du passé ou en compteur global du World ?

Si la réponse est non, elle doit être repensée.

---

# HISTORIQUE

## Version 1.2

- passage en Maturité 2 ;
- alignement explicite sur `GDB-008D v1.1` ;
- séparation transmission individuelle / frontière générationnelle ;
- interdiction de toute copie automatique de Components à chaque génération.

## Version 1.1

- ajout de la frontière avec GDB-004J.

## Version 1.0

- création du document.

---

Fin du document
