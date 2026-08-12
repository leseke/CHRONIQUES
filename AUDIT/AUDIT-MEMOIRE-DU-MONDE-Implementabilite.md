# AUDIT — Implémentabilité de la Mémoire du Monde

> Version : 1.0
> Statut : Clos
> Type : Audit ciblé d'implémentabilité
> Maturité : 4
> Bibliothèque : AUDIT
> Périmètre : GDB-002B/C/D, CORE Entity/World, ENGINE-003/004/005/009

---

# 1. Objet

Déterminer si la Mémoire du Monde peut être implémentée sans que `CHRONIQUES-ENGINE` invente :

- un score universel de significativité ;
- une similarité automatique entre événements ;
- une durée arbitraire de génération ;
- une importance régionale implicite ;
- une pratique culturelle implicite.

---

# 2. Constat initial

`GDB-002B v1.1` possédait déjà les quatre paliers :

```text
Anecdote
↓
Souvenir
↓
Légende
↓
Tradition
```

mais trois notions restaient insuffisamment déterministes malgré le statut M2 :

```text
« seuil de significativité »
« reliée à un autre événement »
« génération suivante »
```

Une implémentation directe aurait obligé ENGINE à choisir des règles métier absentes.

Verdict initial : **bloqué avant correction GDB**.

---

# 3. Corrections d'autorité

`GDB-002B` a été porté à **v1.3**.

Les corrections principales sont :

- significativité déléguée à un Type/règle de mémoire concret ;
- identité stable et payload de mémoire explicités ;
- sources de preuve obligatoirement traçables ;
- liaison/transmission/référence/influence régionale/contradiction/pratique qualifiées uniquement par la règle concrète ;
- marqueur de génération fourni par une autorité/runtime externe, jamais déduit d'un nombre de Ticks ;
- générations sautées évaluées une par une ;
- compteurs du palier Souvenir rendus explicites ;
- transitions exactes de chaque palier fixées ;
- oubli distingué de la suppression technique de la trace.

Après correction, ENGINE peut appliquer les transitions sans choisir leur sens métier.

---

# 4. Frontière avec GDB-002C

`GDB-002C — Les Conséquences du Monde` reste philosophique.

Il définit qu'une conséquence doit être naturelle et proportionnée, mais ne fournit aucun algorithme de significativité.

Conclusion :

```text
conséquence réelle
≠
souvenir automatique
```

Une règle de mémoire concrète doit toujours qualifier explicitement le fait.

---

# 5. Frontière avec GDB-002D

`GDB-002D — Les Événements Dynamiques` définit comment un monde peut produire des situations sans script imposé.

Il ne fournit pas de règle automatique de mémorisation.

Conclusion : un événement dynamique peut devenir **source** de mémoire, jamais mémoire par simple existence.

---

# 6. Stockage dans le moteur

Le Kernel actuel impose que `World` reste un conteneur sans donnée métier.

En revanche, `Entity` est explicitement un point d'ancrage identifiable et neutre dont la nature est définie par ses Components.

Architecture retenue :

```text
Entity neutre
+
WorldMemoryComponent
=
élément de Mémoire du Monde
```

Cette solution :

- préserve `World` ;
- réutilise l'identité stable et la persistance Entity existantes ;
- ne nécessite aucun singleton métier global ;
- n'impose aucune modification de CORE ;
- permet à chaque souvenir de posséder une identité technique stable.

---

# 7. Oubli

Le Kernel ne possède pas actuellement d'API générale de suppression d'Entity, et l'ajouter uniquement pour les souvenirs serait prématuré.

GDB-002B v1.3 autorise donc une distinction :

```text
mémoire active
→ participe au système narratif

mémoire oubliée
→ ne participe plus
→ trace technique persistante conservable
```

ENGINE-019 pourra représenter cet état dans `WorldMemoryComponent` sans détourner `Lifecycle` ni modifier le Kernel.

---

# 8. Générations

La simulation ne possède pas encore une horloge universelle `GenerationIndex` dans `World`.

ENGINE ne doit pas l'inventer.

La frontière autorisée est un resolver injecté :

```text
World + Tick
↓
marqueur de génération non négatif et monotone
```

Sans progression du marqueur :

```text
mémoire créée/persistée
mais
aucune évolution générationnelle de palier
```

Cela permet d'implémenter immédiatement la Mémoire du Monde sans confondre mort, héritage et génération universelle.

---

# 9. Contrat minimal implémentable

ENGINE-019 peut désormais fournir génériquement :

```text
règle concrète de mémoire
↓
candidate qualifiée
↓
Entity + WorldMemoryComponent
↓
Anecdote
↓
preuves générationnelles injectées
↓
transitions déterministes GDB-002B
↓
Souvenir / Légende / Tradition / oublié
```

Le moteur générique peut gérer :

- identité ;
- persistance ;
- déduplication ;
- compteurs ;
- ordre des paliers ;
- replay de générations sautées ;
- historique des transitions.

Il ne gère pas la sémantique concrète de la significativité.

---

# 10. Non-autorisations

L'audit n'autorise pas :

- un Type concret de mémoire ;
- un seuil numérique universel de significativité ;
- une analyse sémantique de texte ;
- un regroupement automatique d'Events ;
- une règle `N Ticks = génération` ;
- un événement dynamique générique complet ;
- une fête, légende ou tradition concrète ;
- une intégration automatique avec Personnalité/Habitudes/Ambitions.

---

# 11. Verdict

```text
GDB-002B v1.1
→ insuffisant pour ENGINE

GDB-002B v1.3
→ implémentable génériquement

Stockage mémoire comme Entity + Component
→ conforme au Kernel

ENGINE-019 — Mémoire du Monde minimale
→ AUTORISÉ
```

Aucun P0/P1 restant n'empêche l'ouverture d'ENGINE-019 dans ce périmètre générique.

---

# Historique

## Version 1.0

- audit ciblé de GDB-002B/C/D ;
- identification des ambiguïtés de significativité, liaison et génération ;
- corrections GDB-002B v1.2 puis v1.3 ;
- choix d'une représentation `Entity + WorldMemoryComponent` ;
- oubli actif/technique clarifié ;
- ENGINE-019 autorisé.
