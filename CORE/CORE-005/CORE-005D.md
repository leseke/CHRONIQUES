# CORE-005-D — Composition

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat conceptuel
>
> Bibliothèque : CORE

---

# 1. Objectif

Définir la composition interne d'un State.

---

# 2. Principe

Un State est composé d'une ou plusieurs Values.

Ces Values décrivent collectivement une condition cohérente.

---

# 3. Cohérence

Toutes les Values appartenant à un même State doivent décrire le même aspect de l'Entity ou du Component.

Un State ne doit jamais mélanger plusieurs responsabilités.

---

# 4. Minimalisme

Un State contient uniquement les Values nécessaires à la représentation de sa condition.

Toute information étrangère à cette condition appartient à un autre State.

---

# 5. Organisation

CORE ne prescrit aucun format d'organisation.

La structure interne relève des bibliothèques dépendantes ou de l'implémentation technique.

---

# 6. Validation

La composition est conforme si :

✓ toutes les Values participent à une même condition ;

✓ aucune logique n'est embarquée ;

✓ la responsabilité reste unique.

---

# Historique

Version 1.0
