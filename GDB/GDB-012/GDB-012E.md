# GDB-012E — Les Productions

> Version : 1.1
> Statut : Officiel
> Type : Métiers & Activités
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes fondamentaux des productions dans Chroniques.

Les productions représentent l'ensemble des biens, œuvres et ressources créés par les personnages. Elles alimentent l'économie, les communautés et le développement des civilisations.

---

# PRINCIPE

Toute production résulte d'une opération explicable mobilisant des éléments réels du monde.

Selon la production, cette opération peut dépendre notamment :

- de ressources ou produits intermédiaires ;
- de compétences ;
- de connaissances ;
- d'outils ;
- de temps ;
- de conditions de lieu ou d'organisation.

Ces dimensions ne sont pas toutes universellement obligatoires pour chaque production.

Le contrat exact appartient à l'opération de production correspondante [réf: GDB-005C].

Le premier lot productif minimal peut donc exécuter une opération qui ne possède encore aucun bonus de compétence ou d'outil, tant que ses entrées, sorties et conditions réellement nécessaires sont explicites.

---

# FORMES DE PRODUCTION

Les productions peuvent être :

- artisanales ;
- agricoles ;
- industrielles ;
- artistiques ;
- scientifiques ;
- culturelles ;
- alimentaires.

Chaque production répond à un besoin ou à une utilité réelle.

---

# PRODUCTION EXÉCUTABLE

Une production devient exécutable lorsque :

- l'opération de production est connue ;
- ses entrées obligatoires existent ;
- les quantités nécessaires sont disponibles ;
- ses conditions obligatoires sont satisfaites ;
- les sorties prévues peuvent être représentées dans le monde.

```text
opération valide
+
entrées disponibles
+
conditions satisfaites
→ production tentable
```

La réussite applique les consommations et productions décrites par GDB-005C.

---

# QUALITÉ ET RENDEMENT

La qualité ou le rendement peuvent dépendre de :

- la compétence ;
- les outils ;
- les connaissances ;
- la qualité des entrées ;
- les conditions de production.

Aucun coefficient implicite n'est créé par cette version.

En l'absence de règle chiffrée dédiée, le premier lot minimal utilise exactement les quantités d'entrée et de sortie de l'opération configurée.

---

# PROVENANCE

Toute production matérielle doit conserver une provenance exploitable jusqu'aux entrées consommées conformément à GDB-005C.

Cette provenance sert notamment à préserver :

- la causalité ;
- la crédibilité de la valeur ;
- les futures règles de qualité ;
- les histoires émergentes liées à la production.

---

# ÉVOLUTION

Les productions évoluent grâce :

- aux spécialisations ;
- aux innovations ;
- aux outils ;
- aux échanges ;
- aux générations.

---

# IMPACT

Les productions influencent :

- l'économie ;
- les métiers ;
- les échanges ;
- les communautés ;
- les histoires émergentes.

---

# FRONTIÈRE AVEC LE COMMERCE

Produire ne signifie pas vendre.

Le premier lot productif autonome peut créer une sortie réelle sans fixer :

- un prix ;
- un salaire ;
- un acheteur ;
- une transaction ;
- une entreprise.

Ces mécanismes appartiennent notamment à GDB-019 et nécessitent leurs propres règles exécutables avant implémentation.

---

# INVARIANTS

- Toute production possède une opération explicable.
- Une production matérielle ne crée pas ses entrées.
- Les conditions réellement requises doivent être satisfaites avant exécution.
- Les quantités produites suivent les données de l'opération tant qu'aucun modificateur documenté ne s'applique.
- Une production conserve une provenance exploitable.
- Produire n'implique ni vente ni rémunération automatique.

---

# RÈGLES DE CONCEPTION

Toute mécanique liée aux productions devra :

1. valoriser la qualité lorsque sa règle existe ;
2. produire des biens ayant une utilité concrète ;
3. interagir avec les autres systèmes ;
4. évoluer avec le monde ;
5. enrichir durablement le gameplay ;
6. préserver l'origine et la traçabilité de ce qui est produit.

---

# CRITÈRE DE VALIDATION

Cette production crée-t-elle une véritable valeur pour le monde à partir d'une opération, d'entrées et de conditions réelles, plutôt qu'une simple ressource chiffrée apparue sans cause ?

Si la réponse est non, elle devra être repensée.

---

# HISTORIQUE

## Version 1.1

- en-tête mis en conformité avec MASTER-004 ;
- clarification que compétences, outils et autres dimensions sont des exigences ou modificateurs propres aux opérations, pas des obligations universelles identiques ;
- définition de la production exécutable minimale ;
- provenance rendue explicitement obligatoire ;
- frontière production / commerce clarifiée.

## Version 1.0

- création du document.

---

Fin du document

Statut : Validé — Référence officielle.
