# CORE-004-D — Caractéristiques

> Version : 1.0
>
> Statut : Fondation
>
> Type : Caractéristiques
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les propriétés fondamentales de la primitive Value.

---

# 2. Atomicité

Une Value représente une information indivisible pour le Kernel.

Le Kernel ne décompose jamais une Value.

---

# 3. Neutralité

Une Value ne possède aucune signification métier intrinsèque.

Sa signification dépend exclusivement du contexte dans lequel elle est utilisée.

---

# 4. Immutabilité conceptuelle

Une Value ne change pas.

Lorsqu'une information évolue, l'ancienne Value est remplacée par une nouvelle.

---

# 5. Réutilisabilité

Une même définition de Value peut être utilisée dans plusieurs Components et plusieurs States.

---

# 6. Comparabilité

Deux Values peuvent être comparées lorsqu'elles appartiennent au même domaine.

Le mode de comparaison relève de l'implémentation.

---

# 7. Validation

Une Value respecte ces caractéristiques si :

✓ elle reste atomique ;

✓ elle demeure indépendante du métier ;

✓ elle conserve une signification unique.

---

# Historique

Version 1.0
