# GDB-005C — Les Chaînes de Production

> Version : 1.2
> Statut : Officiel
> Type : Économie & Progression
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir les principes fondamentaux des chaînes de production dans Chroniques et le contrat minimal d'une opération de production exécutable.

Les chaînes de production relient les ressources, les métiers, les outils et les produits afin de créer une économie crédible.

---

# PRINCIPE

Aucun produit complexe ne doit apparaître sans origine.

Chaque produit résulte d'une succession logique d'étapes de production.

---

# STRUCTURE

Une chaîne de production comprend généralement :

- l'obtention des ressources ;
- leur transformation ;
- leur assemblage éventuel ;
- leur distribution ;
- leur utilisation ou leur recyclage.

Chaque étape peut être réalisée par des métiers différents.

---

# OPÉRATION DE PRODUCTION

Une étape exécutable est représentable comme une **opération de production**.

Une opération définit au minimum :

- une identité stable ;
- une ou plusieurs entrées réellement disponibles ;
- pour chaque entrée, une quantité strictement positive à consommer ;
- une ou plusieurs sorties ;
- pour chaque sortie, une quantité strictement positive à produire ;
- les éventuelles conditions supplémentaires explicitement requises par le contexte.

```text
entrées accessibles
+
opération connue
↓
production réussie
↓
entrées consommées
+
sorties produites
```

Les identifiants et quantités exactes appartiennent aux données de l'opération ou à l'équilibrage applicable. GDB-005C ne fixe aucune recette universelle.

Une opération n'est exécutable que si toutes ses entrées obligatoires existent et sont disponibles en quantité suffisante au moment de la Validation de l'Action.

---

# CONSOMMATION DES ENTRÉES

Une opération réussie consomme exactement les quantités d'entrées prévues par cette opération pour cette exécution.

```text
stock entrée avant = Q
consommation = C
Outcome réussi
→ stock entrée après = Q - C
```

avec `C > 0` et `Q >= C` avant exécution.

Une opération échouée ne peut pas être comptabilisée comme une production réussie.

Les éventuelles pertes produites par un échec devront être spécifiées explicitement avant implémentation ; elles ne sont pas inventées dans le premier lot minimal.

---

# PRODUCTION DES SORTIES

Une réussite augmente la disponibilité des sorties conformément à l'opération exécutée.

```text
Outcome réussi
→ sortie disponible ↑
```

Une sortie ne peut jamais être ajoutée sans que les entrées prévues aient été consommées dans la même résolution réussie.

Le premier lot moteur peut utiliser des stocks de sortie déjà identifiables plutôt que créer de nouvelles Entity pendant l'Action. Ce choix technique ne change pas la règle métier : la quantité produite possède une origine traçable.

---

# INTERDÉPENDANCE

Les chaînes de production favorisent les échanges.

Elles créent naturellement des besoins entre les habitants, les joueurs et les différents secteurs économiques.

---

# ÉVOLUTION

Les chaînes de production évoluent avec :

- les innovations ;
- les nouvelles connaissances ;
- les ressources disponibles ;
- les conséquences du monde.

---

# ROBUSTESSE

Plusieurs méthodes doivent pouvoir produire un résultat similaire lorsqu'elles sont réellement définies.

Le système évite les dépendances uniques qui bloquent inutilement la progression.

---

# INVARIANTS RESSOURCE → PRODUIT

Toute chaîne de production respecte les invariants suivants :

- **Aucun produit sans ressource.** Un Produit [réf: GDB-005E] ne peut jamais être créé sans qu'au moins une Ressource [réf: GDB-005B] ou un produit intermédiaire prévu ait été consommé en amont de la chaîne.
- **Conservation à chaque étape.** Une étape consomme des quantités déterminées d'entrées pour produire des quantités déterminées de sorties. Les rendements différents doivent être explicitement définis par l'opération ou un modificateur autorisé ; ils ne peuvent pas apparaître implicitement.
- **Traçabilité.** Chaque quantité produite doit pouvoir être reliée à l'opération qui l'a créée et aux entrées réellement consommées. La représentation technique peut être un composant, un journal de provenance ou une autre structure persistante compatible avec ENGINE, mais une simple apparition sans origine est interdite.
- **Disponibilité réelle.** Une entrée existante mais non disponible dans le contexte de l'Acteur ne peut pas être consommée par son Action.
- **Pas de stock négatif.** Aucune exécution ne peut consommer davantage que la quantité disponible.

---

# FRONTIÈRE AVEC LES PRIX ET LE MARCHÉ

Cette version rend la **production** exécutable ; elle ne rend pas encore les prix ou le marché calculables.

GDB-019 fait autorité sur l'économie commerciale, l'offre, la demande et les prix.

Le premier lot productif peut donc exister avant une simulation de marché complète, tant qu'il ne fabrique aucune règle de prix, salaire ou vente.

---

# RÈGLES DE CONCEPTION

Toute chaîne de production devra :

1. être crédible ;
2. posséder des étapes logiques ;
3. favoriser la coopération entre métiers ;
4. rester évolutive ;
5. enrichir les histoires émergentes ;
6. ne jamais produire sans entrées prévues et réellement disponibles ;
7. conserver une provenance exploitable des sorties.

---

# CRITÈRE DE VALIDATION

Cette chaîne de production transforme-t-elle des entrées réelles en sorties traçables selon une opération explicite, tout en renforçant l'économie du monde plutôt qu'en faisant apparaître des objets arbitrairement ?

Si la réponse est non, elle devra être repensée.

---

# HISTORIQUE

## Version 1.2

- formalisation de l'opération de production exécutable ;
- quantités d'entrées et de sorties rendues explicites ;
- interdiction des stocks négatifs et de la production sans consommation correspondante ;
- traçabilité de provenance rendue obligatoire pour chaque production ;
- séparation explicite entre socle productif et future simulation de prix/marché de GDB-019.

## Version 1.1

- ajout des invariants Ressource → Produit ;
- en-tête mis en conformité avec MASTER-004.

## Version 1.0

- création du document.

---

Fin du document

Statut : Validé — Référence officielle.
