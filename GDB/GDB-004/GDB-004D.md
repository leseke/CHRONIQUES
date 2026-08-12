# GDB-004D --- Les Personnalités

> Version : 1.3
> Statut : Officiel
> Type : Population du Monde
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir un modèle de personnalité suffisamment précis pour être implémenté sans faire de la personnalité une source directe d'Intent.

---

# PRINCIPE

Chaque habitant possède une personnalité propre qui influence durablement son évolution et certaines données de décision, sans court-circuiter l'arbitrage autonome défini par GDB-004A.

---

# MODÈLE DE TRAITS

Une personnalité est représentée par un ensemble de Traits.

Chaque Trait possède :

- **Nom** : identifiant d'une disposition comportementale stable, jamais d'un état émotionnel transitoire ;
- **Valeur** : valeur continue bornée de 0 à 100 ;
- **Poids de référence** : valeur stabilisée vers laquelle le Trait converge lorsqu'aucune Inflexion n'est en cours.

La Valeur n'est pas bipolaire : deux dispositions opposées sont représentées par deux Traits distincts.

Le nombre de Traits n'est pas fixé par ce document.

---

# CYCLE DE VIE

```text
Formation
↓
Stabilisation
↓
Inflexion éventuelle
↓
Nouvelle stabilisation
```

## Formation

Le Trait se constitue sous l'influence de l'éducation, de la culture et des expériences vécues. Sa Valeur peut varier largement avant stabilisation.

## Stabilisation

La Valeur converge vers son Poids de référence. En l'absence d'événement significatif, seules des variations bornées par un paramètre d'équilibrage sont autorisées.

## Inflexion légère

Un événement identifiable déplace temporairement la Valeur sans modifier le Poids de référence. La Valeur converge ensuite vers la référence d'origine.

## Inflexion profonde

Un événement identifiable dépassant un seuil supérieur déplace la Valeur et modifie le Poids de référence. La nouvelle référence devient durable.

Aucune Inflexion n'existe sans cause identifiable.

---

# IMPACT SUR LES DÉCISIONS

La personnalité agit en amont de l'arbitrage GDB-004A par deux mécanismes actuellement autorisés.

## Ambitions

Un Trait peut modifier l'Intensité d'une Ambition **uniquement si le couple concret Trait/Ambition fournit une règle déterministe de modulation**.

GDB-004D ne définit aucun coefficient universel.

## Habitudes

Un Trait peut modifier le seuil de répétitions nécessaire à la **formation** d'une Habitude **uniquement si le couple concret Trait/Habitude fournit une règle déterministe de modulation**.

Cette version ne permet pas à la personnalité de modifier directement :

- le déclencheur d'une Habitude déjà formée ;
- sa Force ;
- sa position dans l'ordre des familles ;
- la priorité d'un besoin ;
- la présence d'une opportunité économique.

Toute extension de ce type devra être spécifiée explicitement avant code.

---

# FRONTIÈRE AVEC GDB-004E

GDB-004E fait autorité sur la formation, l'activation, la Force et l'évolution des Habitudes.

La personnalité peut seulement modifier un paramètre de formation lorsqu'un mapping concret le prévoit. Elle ne décide jamais qu'un déclencheur est satisfait.

---

# FRONTIÈRE AVEC GDB-004F

GDB-004F fait autorité sur les Ambitions, leur Intensité, leur Progrès et leur arbitrage interne.

La personnalité peut moduler l'Intensité lorsqu'un mapping concret le prévoit ; elle ne crée pas automatiquement une Ambition et ne produit pas son Intent.

---

# DÉTERMINISME

À Trait, données liées, événement, configuration et Tick identiques :

- la même évolution de Valeur est appliquée ;
- le même Poids de référence est conservé ou modifié ;
- les mêmes modulations explicites sont produites.

Aucun bruit aléatoire implicite n'est requis par ce document.

---

# PARAMÈTRES D'IMPLÉMENTATION

Restent paramétrables :

- amplitudes de variation en Stabilisation ;
- seuil d'Inflexion légère ;
- seuil d'Inflexion profonde ;
- vitesse de convergence ;
- mappings et amplitudes de modulation Trait/Ambition ;
- mappings et amplitudes de modulation Trait/Habitude.

Le modèle est fixé ; les constantes et mappings concrets appartiennent aux données/règles compétentes.

---

# INVARIANTS

- Un Trait possède Nom, Valeur et Poids de référence.
- Valeur et Poids restent bornés dans leur domaine configuré, avec Valeur 0..100.
- Une Inflexion exige une cause identifiable.
- La personnalité n'est jamais une source directe d'Intent.
- Aucun Trait ne modifie implicitement l'urgence d'un besoin.
- Aucun Trait ne modifie implicitement l'activation d'une Habitude existante.
- Toute modulation d'Habitude ou d'Ambition exige un mapping concret déterministe.
- GDB-004A conserve l'autorité sur l'ordre des familles d'Intent.

---

# CRITÈRE DE VALIDATION

Le modèle permet-il de représenter des dispositions durables qui évoluent avec l'histoire et modulent explicitement Habitudes/Ambitions sans devenir un score psychologique universel ou une source directe d'Intent ?

Si la réponse est non, il doit être repensé.

---

# HISTORIQUE

## Version 1.3

- clarification de la frontière avec GDB-004A ;
- suppression de toute modulation implicite de l'activation d'une Habitude déjà formée ;
- modulation des Habitudes limitée au seuil de formation via mapping concret ;
- modulation des Ambitions limitée à l'Intensité via mapping concret ;
- interdiction des coefficients psychologiques universels implicites.

## Version 1.2

- ajout du modèle de Traits, des Inflexions légère/profonde et des liens avec Habitudes/Ambitions.

## Version 1.1

- ajout du cycle de vie d'un Trait et de l'invariant de causalité.

## Version 1.0

- création du document.

---

Fin du document
