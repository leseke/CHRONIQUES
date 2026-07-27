# ACT-002-B — Niveaux d'abstraction

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# 1. Objectif

Définir les différents niveaux d'abstraction utilisés pour représenter une action dans Chroniques.

Ces niveaux permettent de passer d'un concept universel à une action concrète exécutée dans la simulation.

---

# 2. Principe

Une action n'existe jamais isolément.

Elle est toujours l'instanciation d'une chaîne de concepts.

Chaque niveau possède une responsabilité unique.

---

# 3. Hiérarchie officielle

Principe

↓

Pattern

↓

Verbe

↓

Action

Aucun niveau supplémentaire n'est défini dans cette version.

---

# 4. Principe

Le Principe représente une idée universelle.

Exemples :

- Déplacement
- Transformation
- Communication
- Échange
- Observation
- Protection

Le Principe n'est jamais exécutable.

---

# 5. Pattern

Le Pattern représente une mécanique réutilisable.

Il décrit une manière générique de mettre en œuvre un Principe.

Le Pattern reste indépendant des acteurs, des objets et du contexte.

---

# 6. Verbe

Le Verbe représente une capacité exprimable.

Il constitue l'interface entre une mécanique abstraite et une action exécutable.

Exemples :

- Marcher
- Construire
- Fabriquer
- Acheter
- Observer
- Convaincre

---

# 7. Action

L'Action représente une exécution réelle.

Elle possède :

- un acteur ;
- des cibles ;
- un contexte ;
- des paramètres ;
- un instant d'exécution.

Exemple :

"Le forgeron fabrique une épée."

---

# 8. Progression

Chaque niveau spécialise le précédent.

Principe

↓

Pattern

↓

Verbe

↓

Action exécutée

L'information augmente progressivement.

L'abstraction diminue progressivement.

---

# 9. Responsabilités

Chaque niveau définit uniquement son propre domaine.

Aucun niveau ne duplique les responsabilités d'un autre.

---

# 10. Contrat

Toute Action doit pouvoir remonter jusqu'à un Principe.

Toute rupture de cette chaîne constitue une incohérence documentaire.

---

# 11. Validation

Le modèle est valide si :

✓ chaque niveau possède une responsabilité propre ;

✓ aucune duplication n'apparaît ;

✓ toutes les actions peuvent être classées.

---

# 12. Historique

Version 1.0

Première définition officielle des niveaux d'abstraction.
