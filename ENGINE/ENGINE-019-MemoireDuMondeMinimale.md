# ENGINE-019 — Mémoire du Monde minimale

> Version : 1.2
> Statut : Validée
> Maturité : 4
> Bibliothèque : ENGINE
> Dépendances : GDB-002B v1.3, GDB-002C, GDB-002D, ENGINE-003, ENGINE-004, ENGINE-005, ENGINE-009
> Implémentation : `CHRONIQUES-ENGINE`
> Validation : 370 / 370 tests réussis

---

# 1. Objectif

Implémenter un framework générique de Mémoire du Monde sans inventer de Type de mémoire concret ni de score universel de significativité.

```text
règle de mémoire injectée
↓
candidate qualifiée
↓
Entity + WorldMemoryComponent
↓
Anecdote
↓
marqueur générationnel + preuves qualifiées
↓
transition déterministe
↓
Souvenir / Légende / Tradition / oublié
```

---

# 2. Représentation validée

Chaque élément de Mémoire du Monde est une `Entity` neutre portant `WorldMemoryComponent`.

`World` reste un conteneur sans donnée métier.

Le Component persiste :

```text
MemoryTypeId
MemoryKey
Payload
Tier
IsForgotten
SourceRefs
CreatedGeneration
LastEvaluatedGeneration
ConsecutiveReferencedGenerations
ConsecutiveUnreferencedGenerations
Transitions
```

Identité métier : `MemoryTypeId + MemoryKey`.

---

# 3. Paliers

```csharp
public enum WorldMemoryTier
{
    Anecdote,
    Memory,
    Legend,
    Tradition,
}
```

`Memory` correspond au palier conceptuel **Souvenir**.

Tout nouvel élément commence `Anecdote` active.

---

# 4. Création

```csharp
public sealed record WorldMemoryCreationCandidate(
    string MemoryTypeId,
    string MemoryKey,
    string Payload,
    IReadOnlyList<string> SourceRefs);
```

Contraintes validées : Type/clé non vides, payload non null, Type conforme à la règle productrice, au moins une source stable non vide, pas de source dupliquée, pas de duplication d'identité existante même oubliée.

Aucun Event n'est transformé automatiquement en souvenir.

---

# 5. Règle générique

```csharp
public interface IWorldMemoryRule
{
    string MemoryTypeId { get; }

    IReadOnlyList<WorldMemoryCreationCandidate> FindCreationCandidates(
        World world,
        Tick currentTick,
        long currentGeneration);

    WorldMemoryGenerationEvidence EvaluateGeneration(
        Entity memoryEntity,
        WorldMemoryComponent memory,
        World world,
        long generation);
}
```

Aucune règle métier n'est fournie par défaut.

---

# 6. Preuves générationnelles

```csharp
public sealed record WorldMemoryGenerationEvidence(
    bool HasLinkOrTransmission,
    bool HasQualifyingReference,
    bool HasRegionalInfluence,
    bool HasEqualOrGreaterContradiction,
    bool HasQualifyingPractice,
    IReadOnlyList<string> SourceRefs);
```

Toute preuve positive exige au moins une source stable.

Les combinaisons impossibles pour le palier courant sont rejetées.

---

# 7. Génération

```csharp
public interface IWorldMemoryGenerationResolver
{
    long ResolveGeneration(World world, Tick currentTick);
}
```

Le marqueur est non négatif et ne peut pas régresser par rapport à l'historique persisté.

Aucune conversion `N Ticks = génération` n'est introduite.

Les générations manquantes sont évaluées une par une.

---

# 8. WorldMemoryEvolutionSystem

Le System validé :

1. résout la génération ;
2. valide les mémoires persistées ;
3. crée les candidates non dupliquées ;
4. laisse une mémoire sans règle inchangée ;
5. évalue chaque génération manquante dans l'ordre ;
6. valide les preuves ;
7. applique uniquement les transitions GDB-002B ;
8. maintient les compteurs ;
9. fusionne les sources sans doublon ;
10. trace promotion, régression ou oubli ;
11. n'avance jamais le Tick ;
12. ne publie aucun Event implicite.

---

# 9. Transitions validées

```text
Anecdote
liaison/transmission ?
├── oui → Memory
└── non → oublié
```

```text
Memory
influence régionale ?
├── oui → Legend
└── référence/transmission ?
    ├── oui → compteur référencé +1 → Legend à 2
    └── non → compteur absence +1 → oublié à 2
```

```text
Legend
pratique ?
├── oui → Tradition
└── contradiction ?
    ├── oui → Memory
    └── non → Legend
```

```text
Tradition
pratique toujours présente ?
├── oui → Tradition
└── non → Legend
```

Une seule transition de palier est possible par génération.

---

# 10. Traces et oubli

```csharp
public sealed record WorldMemoryTransitionTrace(
    long Generation,
    WorldMemoryTier PreviousTier,
    WorldMemoryTier NewTier,
    bool BecameForgotten,
    IReadOnlyList<string> EvidenceSourceRefs);
```

Une mémoire oubliée reste persistée comme trace technique, n'est plus évaluée et ne peut pas être recréée implicitement avec la même identité.

Aucune API générale de suppression d'Entity n'a été ajoutée au Kernel.

---

# 11. Persistance

`WorldMemoryComponent` est pris en charge par `EntitySnapshot` et `WorldRepository`.

La sauvegarde/recharge conserve identité, payload, palier, oubli, sources, marqueurs générationnels, compteurs et traces.

---

# 12. Frontières maintenues

ENGINE-019 ne définit pas :

- Type concret de mémoire ;
- seuil universel de significativité ;
- analyse ou regroupement automatique d'Events ;
- durée universelle d'une génération ;
- événement dynamique générique complet ;
- pratique culturelle concrète ;
- mapping automatique vers Personnalité/Habitudes/Ambitions ;
- nouveau Pattern ou Verbe ACT.

---

# 13. QA validée

```text
Engine019WorldMemoryTests.cs
→ 24 tests comportementaux

Engine019WorldMemoryInvariantTests.cs
→ 16 tests d'invariants
```

Soit **40 nouveaux tests**.

Validation locale finale :

```text
dotnet build
→ succès

dotnet test
→ 370 / 370 tests réussis
→ 0 échec
```

Les 330 tests historiques restent verts.

---

# 14. Critères de validation

Les critères sont satisfaits :

- build réussi ;
- suite historique intacte ;
- 40 tests ENGINE-019 verts ;
- création, déduplication et persistance confirmées ;
- les quatre paliers et l'oubli sont démontrés ;
- les générations sautées sont rejouées séquentiellement ;
- aucune règle concrète de mémoire ni durée arbitraire de génération n'est introduite.

ENGINE-019 est donc **Validée / Maturité 4**.

---

# Historique

## Version 1.2

- ENGINE-019 passe à **Validée / Maturité 4** ;
- validation locale enregistrée à **370 / 370 tests réussis** ;
- 40 tests ENGINE-019 confirmés ;
- persistance, paliers, compteurs, oubli et replay générationnel validés ;
- frontières avec Types concrets, génération universelle et événements dynamiques maintenues.

## Version 1.1

- synchronisation avec l'implémentation candidate ;
- `WorldMemoryComponent`, règles, génération et System ajoutés ;
- persistance intégrée ;
- 40 tests candidats ajoutés ;
- total attendu fixé à 370 / 370.

## Version 1.0

- création d'ENGINE-019 ;
- représentation mémoire par Entity + Component ;
- règles et génération injectées ;
- paliers et compteurs GDB-002B v1.3 spécifiés.

---

Fin du document
