# CORE-003-A — Mission

> Version : 1.0
>
> Statut : Fondation
>
> Type : Mission
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir officiellement la primitive **Component**.

Le Component est l'unité de composition d'une Entity.

---

# 2. Mission

Un Component décrit une caractéristique, une capacité ou une propriété d'une Entity.

Il ne possède pas d'existence autonome.

---

# 3. Principe

Une Entity est définie par l'ensemble des Components qui la composent.

Les Components représentent les informations du monde.

Les comportements sont assurés par les Systems.

---

# 4. Portée

Un Component peut représenter :

- une donnée ;
- un état ;
- une capacité ;
- une classification ;
- un marqueur.

---

# 5. Responsabilités

Un Component :

- décrit ;
- stocke des informations ;
- participe à la composition d'une Entity.

Il ne prend jamais de décision.

---

# 6. Validation

Un Component est conforme si :

✓ il possède une responsabilité unique ;

✓ il est indépendant de la logique métier ;

✓ il peut être réutilisé par plusieurs types d'Entities.

---

# Historique

Version 1.0

Première définition officielle de la primitive Component.
