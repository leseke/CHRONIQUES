# ENGINE-019 — Mémoire du Monde minimale

> Version : 1.0
> Statut : Proposition
> Maturité : 2
> Bibliothèque : ENGINE
> Dépendances : GDB-002B v1.3, GDB-002C, GDB-002D, ENGINE-003, ENGINE-004, ENGINE-005, ENGINE-009

---

# 1. Objectif

Implémenter un framework générique de Mémoire du Monde sans inventer de Type de mémoire concret ni de score universel de significativité.

Flux visé :

```text
règle de mémoire injectée
↓
candidate qualifiée
↓
Entity + WorldMemoryComponent
↓
Anecdote
↓
marqueur générationnel
+
preuves qualifiées
↓
transition déterministe
↓
Souvenir / Légende / Tradition / oublié
```

---

# 2. Représentation

Chaque élément de Mémoire du Monde est une `Entity` neutre portant :

```csharp
public sealed class WorldMemoryComponent : IComponent
```

Cette architecture respecte le Kernel : `World` reste un conteneur sans donnée métier.

---

# 3. Données persistantes

Le Component contient au minimum :

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

Identité métier d'un élément :

```text
MemoryTypeId + MemoryKey
```

Aucune seconde Entity de mémoire ne peut porter la même identité.

---

# 4. Paliers

```csharp
public enum WorldMemoryTier
{
    Anecdote,
    Memory,
    Legend,
    Tradition,
}
```

Le nom technique `Memory` correspond au palier conceptuel **Souvenir**.

Tout nouvel élément commence en `Anecdote` active.

---

# 5. Candidate de création

Une règle peut produire :

```csharp
public sealed record WorldMemoryCreationCandidate(
    string MemoryTypeId,
    string MemoryKey,
    string Payload,
    IReadOnlyList<string> SourceRefs);
```

Contraintes :

- Type et clé non vides ;
- Type identique à celui de la règle productrice ;
- payload non null ;
- au moins une source stable non vide ;
- aucune source dupliquée ;
- aucune identité déjà présente, même oubliée.

Le moteur ne déduit jamais une candidate depuis `World.Events` sans règle.

---

# 6. IWorldMemoryRule

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

Aucune implémentation métier n'est fournie par défaut.

---

# 7. Preuves générationnelles

```csharp
public sealed record WorldMemoryGenerationEvidence(
    bool HasLinkOrTransmission,
    bool HasQualifyingReference,
    bool HasRegionalInfluence,
    bool HasEqualOrGreaterContradiction,
    bool HasQualifyingPractice,
    IReadOnlyList<string> SourceRefs);
```

Si au moins un booléen est vrai, `SourceRefs` doit contenir au moins une source stable non vide.

Pour une Légende :

```text
HasQualifyingPractice = true
+
HasEqualOrGreaterContradiction = true
→ invalide
```

ENGINE ne qualifie jamais lui-même une preuve.

---

# 8. Génération

```csharp
public interface IWorldMemoryGenerationResolver
{
    long ResolveGeneration(World world, Tick currentTick);
}
```

Le marqueur doit être entier, non négatif et ne peut pas être antérieur aux générations déjà persistées.

Aucune règle `N Ticks = 1 génération` n'est fournie.

Si le marqueur reste inchangé, aucune transition générationnelle n'est appliquée.

Si plusieurs générations ont été sautées, elles sont évaluées une par une.

---

# 9. WorldMemoryEvolutionSystem

Le System :

1. résout la génération courante ;
2. valide les éléments de mémoire existants ;
3. demande les candidates de création à chaque règle ;
4. crée les nouvelles `Entity` mémoire non dupliquées ;
5. pour chaque mémoire active disposant de sa règle, rejoue chaque génération manquante dans l'ordre ;
6. demande les preuves de la génération à la règle ;
7. applique exactement la transition définie par GDB-002B ;
8. met à jour les compteurs ;
9. ajoute les sources nouvelles sans doublon ;
10. trace toute promotion, régression ou oubli ;
11. n'avance jamais le Tick.

Une mémoire dont la règle n'est plus enregistrée reste persistée et n'évolue pas.

---

# 10. Transitions

## Anecdote

```text
liaison/transmission ?
├── oui → Memory
└── non → IsForgotten = true
```

## Memory / Souvenir

```text
influence régionale ?
├── oui → Legend
└── non
    ↓
référence ou transmission ?
├── oui
│   → referenced + 1
│   → unreferenced = 0
│   → si referenced == 2 : Legend
└── non
    → referenced = 0
    → unreferenced + 1
    → si unreferenced == 2 : oublié
```

## Legend / Légende

```text
pratique ?
├── oui → Tradition
└── non
    ↓
contradiction ?
├── oui → Memory
└── non → reste Legend
```

## Tradition

```text
pratique toujours existante ?
├── oui → reste Tradition
└── non → Legend
```

Une seule transition de palier est possible par génération.

---

# 11. TransitionTrace

Chaque changement réel ajoute une trace persistante :

```csharp
public sealed record WorldMemoryTransitionTrace(
    long Generation,
    WorldMemoryTier PreviousTier,
    WorldMemoryTier NewTier,
    bool BecameForgotten,
    IReadOnlyList<string> EvidenceSourceRefs);
```

Un oubli conserve `PreviousTier == NewTier` et `BecameForgotten = true`.

Les générations sans changement de palier ne créent pas de trace de transition.

---

# 12. Persistance

`WorldMemoryComponent` est ajouté à `EntitySnapshot` comme champ optionnel.

La sauvegarde/recharge préserve :

- identité ;
- payload ;
- palier ;
- oubli ;
- sources ;
- génération de création ;
- dernière génération évaluée ;
- compteurs ;
- traces de transition.

Les règles et le resolver de génération restent runtime.

---

# 13. Oubli

Une mémoire oubliée :

```text
IsForgotten = true
```

Elle :

- reste persistée comme trace technique ;
- n'est plus évaluée ;
- n'est plus considérée comme mémoire active ;
- ne peut pas être recréée avec la même identité.

ENGINE-019 n'ajoute aucune API générale de suppression d'Entity au Kernel.

---

# 14. Frontières

ENGINE-019 ne définit pas :

- Type concret de mémoire ;
- seuil de significativité ;
- regroupement automatique d'Events ;
- analyse sémantique ;
- durée d'une génération ;
- événement dynamique générique ;
- pratique culturelle concrète ;
- mapping automatique vers Personnalité/Habitudes/Ambitions ;
- nouveau Pattern ou Verbe ACT.

---

# 15. Invariants

- `World` reste sans donnée métier de Mémoire.
- Toute mémoire est portée par une Entity identifiable.
- Identité = `MemoryTypeId + MemoryKey`.
- Tout nouvel élément commence Anecdote active.
- Aucun saut de palier.
- Une transition maximum par génération.
- Les générations sautées sont évaluées une par une.
- Une mémoire oubliée ne redevient pas active implicitement.
- Une règle absente bloque l'évolution sans supprimer la mémoire.
- Toute preuve positive possède une source stable.
- Aucun Event n'est mémorisé automatiquement.
- Le System n'avance jamais le Tick.

---

# 16. Critère de validation

ENGINE-019 pourra passer Validée / Maturité 4 lorsque, avec uniquement des règles factices déterministes, le moteur démontrera :

- création et déduplication ;
- persistance ;
- Anecdote → Souvenir ;
- oubli d'une Anecdote ;
- Souvenir → Légende par deux références consécutives ;
- Souvenir → Légende par influence régionale ;
- oubli d'un Souvenir après deux absences ;
- Légende → Tradition ;
- Légende → Souvenir par contradiction ;
- Tradition → Légende si la pratique disparaît ;
- replay de générations sautées ;
- validation des preuves et compteurs ;
- absence de règle concrète par défaut ;
- absence de mutation du Kernel autre que via les primitives existantes.

Base validée avant ce lot :

```text
330 / 330
```

---

# Historique

## Version 1.0

- création d'ENGINE-019 ;
- représentation mémoire par Entity + Component ;
- règles et génération injectées ;
- paliers et compteurs GDB-002B v1.3 spécifiés ;
- oubli conservé comme trace technique.
