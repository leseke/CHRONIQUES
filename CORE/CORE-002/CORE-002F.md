# CORE-002-F — Contraintes

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contraintes
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir les contraintes auxquelles toute Entity doit respecter.

---

# 2. Contraintes

Une Entity :

- possède une identité unique ;
- est composée de Components ;
- peut évoluer ;
- ne contient aucune logique métier.

---

# 3. Interdictions

Une Entity ne doit jamais :

- exécuter une règle métier ;
- contenir un algorithme ;
- dépendre d'une implémentation technique.

---

# 4. Validation

Une Entity est valide si toutes ces contraintes sont respectées.

---

# Historique

Version 1.0
