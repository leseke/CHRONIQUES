# ACT-002-E — Action Contract

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT

---

# 1. Objectif

Définir le contrat fonctionnel qui décrit intégralement une action exécutable.

L'Action Contract constitue l'interface officielle entre la définition d'une action et son exécution.

---

# 2. Principe

Une Action Definition ne contient pas directement sa logique.

Elle référence un Action Contract.

Le contrat décrit :

- ce qui est nécessaire ;
- ce qui est autorisé ;
- ce qui est produit.

---

# 3. Structure

Action Contract

↓

Inputs

↓

Preconditions

↓

Constraints

↓

Costs

↓

Execution Rules

↓

Outputs

↓

Effects

↓

Events

↓

Postconditions

---

# 4. Inputs

Définissent les données attendues.

Exemples :

- acteur ;
- cible ;
- outil ;
- matériau ;
- quantité.

---

# 5. Preconditions

Conditions devant être satisfaites avant toute exécution.

Exemples :

- posséder un marteau ;
- être vivant ;
- disposer d'assez d'énergie.

---

# 6. Constraints

Règles qui limitent l'exécution.

Exemples :

- distance maximale ;
- poids maximal ;
- température ;
- heure.

---

# 7. Costs

Définissent les ressources consommées.

Exemples :

- endurance ;
- mana ;
- argent ;
- temps ;
- matériaux.

---

# 8. Execution Rules

Décrivent les règles d'exécution.

Elles précisent notamment :

- durée ;
- interruption ;
- reprise ;
- parallélisation ;
- priorité.

---

# 9. Outputs

Décrivent les résultats attendus.

Exemples :

- objet créé ;
- information obtenue ;
- position modifiée.

---

# 10. Effects

Définissent les modifications apportées au monde.

Ils sont exécutés uniquement après validation.

---

# 11. Events

Décrivent les événements publiés.

Ils permettent aux autres systèmes de réagir sans couplage direct.

---

# 12. Postconditions

Conditions garanties après la résolution.

---

# 13. Contrat

Chaque composant est indépendant.

Chaque composant peut être partagé entre plusieurs contrats.

---

# 14. Validation

Un contrat est valide si :

✓ il est complet ;

✓ chaque composant est cohérent ;

✓ aucune dépendance circulaire n'existe.

---

# Historique

Version 1.0
