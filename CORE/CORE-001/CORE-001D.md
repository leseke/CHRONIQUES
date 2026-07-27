# CORE-001-D — Les lois du Kernel

Version : 1.0

Statut : Fondation

Type : Invariants

Bibliothèque : CORE

---

# Objectif

Définir les lois immuables gouvernant toutes les primitives du noyau.

Ces lois constituent les invariants fondamentaux de Chroniques.

Aucune bibliothèque ne peut les contourner.

---

# Loi 1 — Toute information appartient à une Entity

Une information n'existe jamais seule.

Elle est toujours portée par une Entity.

---

# Loi 2 — Une Entity est définie par ses Components

Une Entity ne décrit pas directement ses propriétés.

Elle référence des Components.

---

# Loi 3 — Un Component possède un State

Chaque Component peut posséder un état.

L'état représente sa condition à un instant donné.

---

# Loi 4 — Un State est composé de Values

Le State ne contient que des valeurs.

Il ne contient aucune logique.

---

# Loi 5 — Les Values sont atomiques

Une Value représente une mesure élémentaire.

Exemples :

12

Rouge

Actif

145 kg

37 °C

---

# Loi 6 — Les Relations relient des Entities

Une Relation possède toujours :

une origine

une destination

un type

---

# Loi 7 — Les Events décrivent un changement

Un Event n'est jamais une commande.

Il représente un fait accompli.

---

# Loi 8 — Le Temps ordonne les Events

Le Temps ne provoque rien.

Il permet uniquement d'ordonner les changements.

---

# Loi 9 — L'Espace localise les Entities

L'Espace influence le contexte.

Il ne modifie jamais directement les règles métier.

---

# Loi 10 — Les References assurent la traçabilité

Toute référence possède une origine.

Toute référence possède une destination.

---

# Loi 11 — Le Lifecycle décrit les transitions

Le Lifecycle ne décrit jamais les données.

Il décrit uniquement les changements d'état.

---

# Loi 12 — Les Systems appliquent les règles

Le Kernel ne contient aucune logique métier.

Les comportements sont réalisés par des Systems définis dans TECH.

---

# Contrat

Toute évolution de CORE doit respecter l'ensemble de ces lois.

---

# Validation

Le document est conforme si :

✓ aucune loi n'entre en contradiction avec une autre ;

✓ chaque primitive possède une responsabilité unique ;

✓ aucune logique métier n'est introduite dans CORE.
