# ACT-001-A — Mission

> Version : 1.0
>
> Statut : Fondation
>
> Bibliothèque : ACT
>
> Références :
> - MASTER
> - GDB
> - TECH

---

# 1. Mission

La bibliothèque **ACT** définit le langage universel des actions de Chroniques.

Elle formalise toutes les possibilités d'interaction entre les acteurs, le monde et les systèmes.

ACT constitue la référence officielle du gameplay.

Toute mécanique implémentée dans le moteur doit être décrite dans ACT avant son développement.

---

# 2. Objectifs

ACT poursuit les objectifs suivants :

- décrire toutes les actions possibles ;
- normaliser les mécaniques de gameplay ;
- favoriser la réutilisation des systèmes ;
- limiter les duplications ;
- fournir une spécification exploitable par le développement ;
- garantir la cohérence du gameplay.

---

# 3. Rôle

ACT répond à une seule question :

> **Que peut entreprendre un acteur ?**

Elle ne répond jamais aux questions :

> Qu'est-ce qui existe ?

→ GDB

ou

> Comment cela fonctionne techniquement ?

→ TECH

---

# 4. Position dans l'architecture

MASTER

↓

GDB

↓

ACT

↓

TECH

↓

CODE

Chaque niveau dépend uniquement du niveau supérieur.

Aucune couche ne doit empiéter sur la responsabilité d'une autre.

---

# 5. Responsabilités

ACT est responsable :

- des actions ;
- des interactions ;
- des comportements ;
- des conséquences ;
- des événements produits ;
- des règles de composition des actions.

---

# 6. Hors périmètre

ACT ne documente jamais :

- les objets ;
- les bâtiments ;
- les métiers ;
- les organisations ;
- les personnages ;
- les ressources ;
- les données techniques ;
- les algorithmes ;
- le code source.

Ces éléments appartiennent respectivement à GDB ou TECH.

---

# 7. Principes fondateurs

Toute action :

- possède un acteur ;
- possède une ou plusieurs cibles ;
- s'exécute dans un contexte ;
- possède des conditions ;
- produit des conséquences ;
- peut générer des événements.

---

# 8. Universalité

Les actions documentées dans ACT doivent être indépendantes :

- des civilisations ;
- des époques ;
- des professions ;
- des cultures ;
- des technologies.

Une même action peut être réutilisée dans plusieurs contextes.

---

# 9. Réutilisation

Une mécanique ne doit être décrite qu'une seule fois.

Les systèmes spécialisés réutilisent les mécanismes existants au lieu de créer de nouvelles règles.

---

# 10. Impact technique

Cette mission sert directement à :

- GAME DESIGN
- IA
- TECH
- QA
- UX

---

# 11. Critères de validation

La mission d'ACT est considérée comme respectée si :

✓ Toute action est documentée.

✓ Aucun doublon mécanique n'existe.

✓ Chaque verbe appartient à un pattern.

✓ Chaque pattern appartient au modèle universel.

✓ Toute implémentation TECH possède une référence ACT.

---

# 12. Évolution

Toute extension de la bibliothèque ACT doit respecter cette mission.

Aucune nouvelle mécanique ne peut être ajoutée si elle contrevient aux principes définis dans ce document.
