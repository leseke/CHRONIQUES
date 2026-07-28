# CORE-000-D — Dépendances

Les dépendances autorisées sont les suivantes :

Entity
→ Component

Component
→ State

State
→ Value

Relation
→ Entity
→ State

Event
→ Time

Lifecycle
→ Event
→ State
→ Time

Space est orthogonal.

Time est orthogonal.

Aucune dépendance circulaire n'est autorisée.
