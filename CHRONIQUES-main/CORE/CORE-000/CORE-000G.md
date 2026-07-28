# CORE-000-G — Invariants globaux

Le Kernel respecte toujours les invariants suivants :

- aucune logique métier ;
- aucune primitive ne provoque une action ;
- les Events sont immuables ;
- les States représentent une condition ;
- Time fournit un ordre ;
- Space fournit une localisation ;
- Lifecycle représente une continuité.
