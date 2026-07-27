# CORE-004-A — Mission

> Version : 1.0
>
> Statut : Fondation
>
> Type : Mission
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir officiellement la primitive **Value**.

Une Value représente la plus petite unité d'information du modèle conceptuel de Chroniques.

---

# 2. Mission

Une Value décrit une information atomique.

Elle ne possède aucune structure interne pertinente pour le Kernel.

---

# 3. Principe

Les Values constituent les éléments de base permettant de construire les States.

---

# 4. Portée

Une Value peut représenter :

- une quantité ;
- une mesure ;
- un texte ;
- un booléen ;
- une référence ;
- toute donnée atomique.

---

# 5. Responsabilités

Une Value :

- représente une information ;
- peut être comparée ;
- peut être remplacée.

Elle ne possède aucun comportement.

---

# 6. Validation

Une Value est conforme si :

✓ elle est atomique ;

✓ elle est indépendante du métier ;

✓ elle peut être utilisée dans plusieurs Components.

---

# Historique

Version 1.0
