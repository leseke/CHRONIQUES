# CORE-008-D — Composition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir la composition conceptuelle de Time.

---

# 2. Principe

Time est composé d'Instants ordonnés.

CORE ne définit pas leur représentation.

---

# 3. Instant

Un Instant représente une position unique dans Time.

Il ne possède aucune signification métier.

---

# 4. Ordre

Les Instants peuvent être comparés.

Cette comparaison permet uniquement d'établir leur ordre.

---

# 5. Neutralité

CORE ne définit :

- aucune unité ;
- aucune fréquence ;
- aucune précision.

Ces notions appartiennent aux bibliothèques spécialisées.

---

# 6. Validation

Time est conforme si :

✓ les Instants sont ordonnables ;

✓ leur représentation reste libre ;

✓ aucune implémentation n'est imposée.

---

# Historique

Version 1.0
