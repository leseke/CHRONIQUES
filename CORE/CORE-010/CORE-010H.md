# CORE-010-H — Relations

> Version : 1.0
>
> Statut : Fondation
>
> Type : Relations
>
> Bibliothèque : CORE

---

# 1. Objectif

Décrire les relations entre Lifecycle et les autres primitives du Kernel.

---

# 2. Relations

Lifecycle :

- concerne une primitive évolutive ;
- organise des States ;
- référence des Events ;
- s'inscrit dans le Time ;
- peut être contextualisé dans le Space lorsque la continuité possède une dimension spatiale.

---

# 3. Dépendances

Lifecycle dépend des primitives fondamentales du Kernel sans modifier leurs responsabilités.

Il organise leur continuité de manière purement descriptive.

---

# 4. Validation

Les relations sont conformes si elles respectent les responsabilités définies dans CORE.

---

# Historique

Version 1.0
