# CORE-000-F — Architecture

Le Kernel peut être représenté comme :

```text
                Entity
                   │
             Component
                   │
                State
                   │
                Value

Relation ──────────┘

Event ─────── Time

Space

Lifecycle
    │
    ├── Event
    ├── State
    └── Time
```

Chaque primitive répond à une responsabilité indépendante.
