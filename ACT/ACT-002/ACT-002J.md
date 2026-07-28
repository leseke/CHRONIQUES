# ACT-002-J — Gouvernance du modèle

> Version : 1.0
>
> Statut : Fondation
>
> Type : Gouvernance
>
> Bibliothèque : ACT

---

# 1. Objectif

Garantir la stabilité et l'évolutivité du modèle universel des actions.

---

# 2. Principes

Le modèle universel constitue la référence officielle de toutes les actions de Chroniques.

Toute évolution doit préserver :

- la séparation des responsabilités ;
- la traçabilité ;
- la réutilisabilité ;
- la compatibilité documentaire.

---

# 3. Évolution

Les évolutions doivent privilégier :

- la composition ;
- la spécialisation ;
- les contrats.

L'introduction de nouveaux niveaux d'abstraction est exceptionnelle et nécessite une décision d'architecture (ADR).

---

# 4. Compatibilité

Les modifications ne doivent pas rompre les documents ACT existants sans procédure de migration documentée.

---

# 5. Dépendances

Le modèle ACT ne dépend jamais :

- d'une implémentation TECH ;
- d'un moteur graphique ;
- d'un protocole réseau ;
- d'une interface utilisateur.

---

# 6. Validation

Toute évolution du modèle doit démontrer :

- un bénéfice architectural clair ;
- l'absence de duplication ;
- une amélioration de la maintenabilité.

---

# 7. Traçabilité

Chaque évolution est :

- justifiée ;
- documentée ;
- historisée ;
- reliée à un ADR.

---

# 8. Contrat

ACT reste la référence conceptuelle du système d'actions.

Les autres bibliothèques s'y conforment sans le modifier.

---

# Historique

Version 1.0
