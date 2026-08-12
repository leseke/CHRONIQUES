GDB-004D --- Les Personnalités

Version : 1.2
Statut : Officiel
Type : Population du Monde
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir les principes qui gouvernent les personnalités des habitants de
Chroniques, avec une précision suffisante pour être implémentées sans
interprétation (MASTER-007, Maturité 2).

La personnalité influence durablement les décisions, les relations et
les réactions de chaque individu.
⸻
PRINCIPE

Chaque habitant possède une personnalité qui lui est propre.

Elle guide ses choix sans les rendre totalement prévisibles.
⸻
COMPOSITION

Une personnalité est influencée par :

- le caractère ;
- les expériences vécues ;
- l'éducation ;
- la culture ;
- les relations ;
- les ambitions.
⸻
MODÈLE DE TRAITS

Une personnalité est représentée par un ensemble de Traits. Chaque Trait
possède trois attributs :

- **Nom.** Identifiant unique du Trait dans le système (ex. :
  « impulsivité », « curiosité », « loyauté »). Le nom décrit une
  disposition comportementale stable, jamais un état émotionnel
  transitoire (la colère est un état émotionnel ; l'impulsivité est un
  Trait).

- **Valeur.** Valeur continue bornée entre 0 et 100. 0 représente
  l'absence totale de cette disposition ; 100 la disposition maximale.
  La Valeur n'est pas bipolaire (0 n'est pas l'opposé de 100 ---
  l'opposé d'un Trait est un autre Trait distinct avec son propre nom
  et sa propre Valeur). Un habitant peut ainsi avoir une Valeur
  d'impulsivité à 80 et une Valeur de prudence à 60 --- les deux Traits
  coexistent et interagissent selon les règles de la section IMPACT.

- **Poids de référence.** La Valeur stabilisée vers laquelle le Trait
  tend naturellement lorsqu'aucune Inflexion n'est en cours. Ce poids
  est fixé à la Stabilisation (voir CYCLE DE VIE). Il ne change jamais
  spontanément --- seule une nouvelle Inflexion peut le modifier.

Le nombre de Traits d'un habitant n'est pas fixé par ce document. Un
sous-ensemble minimal suffit pour le premier lot d'implémentation ; de
nouveaux Traits peuvent être ajoutés sans modifier le modèle de base.
⸻
CYCLE DE VIE D'UN TRAIT

Un trait de personnalité traverse quatre étapes :

Formation → Stabilisation → Inflexion → Nouvelle stabilisation

- **Formation.** Le trait se constitue durant les jeunes années d'un
  individu, sous l'influence de l'éducation, de la culture et des
  premières expériences [réf: GDB-004G pour les connaissances acquises
  durant cette période]. La Valeur n'a pas encore atteint son poids de
  référence définitif et peut varier plus largement.

- **Stabilisation.** À l'âge adulte, la Valeur converge vers le poids
  de référence. Elle ne varie plus qu'à la marge (± une amplitude
  journalière paramétrisée) tant qu'aucun événement majeur ne la remet
  en question. C'est l'état par défaut d'un habitant pendant la majeure
  partie de sa vie.

- **Inflexion.** Un événement d'ampleur suffisante [réf: GDB-002B pour
  les seuils de significativité qui définissent une telle ampleur] ---
  un deuil, une trahison, un exploit, une ruine --- déplace
  temporairement la Valeur du Trait, puis, si l'amplitude de
  l'événement dépasse un second seuil, modifie également le poids de
  référence. Cette étape est toujours déclenchée par un fait précis et
  racontable, jamais par une dérive silencieuse.

  Deux cas d'Inflexion à distinguer :
  - **Inflexion légère** (amplitude < seuil de modification de
    référence) : la Valeur est déplacée temporairement, mais le poids
    de référence ne change pas. La Valeur reviendra progressivement vers
    son poids de référence d'origine.
  - **Inflexion profonde** (amplitude ≥ seuil de modification de
    référence) : la Valeur est déplacée et le poids de référence est
    mis à jour vers une nouvelle valeur. Le Trait ne reviendra jamais
    automatiquement à son poids d'avant l'Inflexion.

- **Nouvelle stabilisation.** La Valeur converge vers le nouveau poids
  de référence. Le cycle peut recommencer si un nouvel événement
  d'ampleur suffisante survient.

Invariant : un trait ne peut entrer en Inflexion que si un événement
identifiable en est la cause. L'absence d'une telle cause interdit toute
variation de la Valeur au-delà de l'amplitude journalière paramétrisée.
⸻
IMPACT SUR LES DÉCISIONS

La personnalité influence les décisions à deux niveaux :

1. **Modification de l'Intensité des Ambitions.** Un Trait peut augmenter
   ou diminuer l'Intensité d'une Ambition compatible avec lui [réf:
   GDB-004F]. Par exemple, un Trait de curiosité élevée peut augmenter
   l'Intensité de toute Ambition d'exploration ou d'apprentissage. Ce
   lien est défini par les règles propres à chaque couple (Trait,
   Ambition) --- pas par ce document.

2. **Modification du seuil de formation des Habitudes.** Un Trait peut
   abaisser ou relever le nombre de répétitions nécessaires pour former
   une Habitude compatible [réf: GDB-004E]. Par exemple, un Trait de
   rigueur élevée peut réduire le seuil de formation des Habitudes
   professionnelles.

La personnalité n'intervient jamais directement dans l'arbitrage de la
chaîne GDB-004A (besoins → transfert → production → Habitudes →
Ambitions). Elle agit en amont, en modulant le poids des Ambitions et
la vitesse de formation des Habitudes, pas en court-circuitant la
chaîne.
⸻
FRONTIÈRE AVEC GDB-004E (HABITUDES)

La personnalité module la formation des Habitudes (seuil de répétition,
sensibilité du déclencheur) mais ne définit pas les Habitudes
elles-mêmes. GDB-004E reste l'autorité sur les comportements acquis par
répétition.
⸻
FRONTIÈRE AVEC GDB-004F (AMBITIONS)

La personnalité module l'Intensité des Ambitions mais ne les crée pas.
GDB-004F reste l'autorité sur les directions de vie.
⸻
DIVERSITÉ

Deux habitants partageant le même métier ou le même environnement
peuvent adopter des comportements très différents en raison de leurs
Traits distincts.

La personnalité participe à cette diversité.
⸻
PARAMÈTRES D'IMPLÉMENTATION

Les valeurs suivantes ne sont pas fixées par ce document : amplitude
journalière de variation en Stabilisation, seuil d'amplitude d'un
événement pour déclencher une Inflexion légère, seuil supérieur pour
une Inflexion profonde, vitesse de convergence vers le poids de
référence après Inflexion, ampleur de modification du modificateur
d'Intensité d'Ambition ou de seuil d'Habitude par unité de Valeur de
Trait. Même posture que GDB-004C, GDB-004E : le modèle est fixé, les
constantes restent des paramètres d'équilibrage.
⸻
IMPACT (SYSTÈMES INFLUENCÉS)

La personnalité influence notamment :

- les décisions ;
- les réactions émotionnelles ;
- les relations ;
- les priorités ;
- la résolution des conflits.
⸻
RÈGLES DE CONCEPTION

Toute mécanique liée aux personnalités devra :

1. préserver la cohérence des comportements ;
2. permettre une évolution progressive ;
3. éviter les réactions totalement aléatoires ;
4. enrichir les histoires émergentes ;
5. renforcer l'identité des habitants.
⸻
CRITÈRE DE VALIDATION

Cette mécanique permet-elle aux habitants d'agir comme des individus
crédibles plutôt que comme de simples fonctions de gameplay ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.2 : ajout du MODÈLE DE TRAITS (Nom, Valeur 0-100, Poids de
référence), enrichissement du CYCLE DE VIE avec deux cas d'Inflexion
distincts (légère : déplacement temporaire sans modification du poids ;
profonde : déplacement + nouveau poids de référence), ajout de la
section IMPACT SUR LES DÉCISIONS (modification de l'Intensité des
Ambitions via GDB-004F, modification du seuil de formation des
Habitudes via GDB-004E), frontières explicites avec GDB-004E et
GDB-004F, section PARAMÈTRES D'IMPLÉMENTATION. Le modèle devient
suffisamment précis pour être implémenté sans interprétation.

Version 1.1 : ajout du cycle de vie d'un trait (Formation →
Stabilisation → Inflexion → Nouvelle stabilisation) et de son invariant
de causalité. Corrige GDB-004-C02. En-tête mis en conformité avec
MASTER-004.

Version 1.0 : création du document.
