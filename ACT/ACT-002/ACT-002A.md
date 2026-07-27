# ACT-002-A — Mission du modèle universel

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# 1. Objectif

Définir le modèle universel permettant de représenter toutes les actions de Chroniques.

Ce modèle constitue la grammaire officielle du gameplay.

Toute action documentée dans ACT doit être compatible avec ce modèle.

---

# 2. Mission

Le modèle universel permet :

- de normaliser les actions ;
- de limiter les duplications ;
- de favoriser la réutilisation des mécaniques ;
- de simplifier l'implémentation technique ;
- d'assurer une cohérence entre les systèmes.

---

# 3. Principe

Une action n'est jamais créée isolément.

Elle appartient toujours à une structure hiérarchique.

Cette hiérarchie permet :

- la réutilisation ;
- l'héritage ;
- la composition ;
- la spécialisation.

---

# 4. Les quatre niveaux

Toute action appartient aux niveaux suivants :

Principe

↓

Pattern

↓

Verbe

↓

Action exécutée

Chaque niveau possède une responsabilité propre.

---

# 5. Universalité

Le modèle est indépendant :

- des civilisations ;
- des époques ;
- des métiers ;
- des technologies ;
- des scénarios.

Il est valable pour tout Chroniques.

---

# 6. Responsabilités

Le modèle définit :

- la structure des actions ;
- les relations entre les concepts ;
- les règles de spécialisation ;
- les règles de composition.

---

# 7. Hors périmètre

Le modèle ne définit pas :

- les entités (GDB) ;
- les algorithmes (TECH) ;
- les interfaces (UX).

---

# 8. Contrat

Toute nouvelle mécanique doit être représentable par ce modèle.

Dans le cas contraire, le modèle doit évoluer avant la mécanique.

---

# 9. Validation

Le modèle est valide si :

✓ toutes les actions y trouvent leur place ;

✓ aucune duplication conceptuelle n'apparaît ;

✓ la structure reste extensible.

---

# 10. Historique

Version 1.0

Création du modèle universel des actions.
