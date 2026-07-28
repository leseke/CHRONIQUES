GDB-005C --- Les Chaînes de Production

Version : 1.1
Statut : Officiel
Type : Économie & Progression
Maturité : 2
Bibliothèque : GDB
⸻


OBJECTIF

Définir les principes fondamentaux des chaînes de production dans 
Chroniques.

Les chaînes de production relient les ressources, les métiers, les 
outils et les produits afin de créer une économie crédible.
⸻
PRINCIPE

Aucun objet complexe ne doit apparaître sans origine.

Chaque produit résulte d'une succession logique d'étapes de production.
⸻
STRUCTURE

Une chaîne de production comprend généralement :

	⁃	l'obtention des ressources ;
	⁃	leur transformation ;
	⁃	leur assemblage éventuel ;
	⁃	leur distribution ;
	⁃	leur utilisation ou leur recyclage.

Chaque étape peut être réalisée par des métiers différents.
⸻
INTERDÉPENDANCE

Les chaînes de production favorisent les échanges.

Elles créent naturellement des besoins entre les habitants, les joueurs 
et les différents secteurs économiques.
⸻
ÉVOLUTION

Les chaînes de production évoluent avec :

	⁃	les innovations ;
	⁃	les nouvelles connaissances ;
	⁃	les ressources disponibles ;
	⁃	les conséquences du monde.
⸻
ROBUSTESSE

Plusieurs méthodes doivent pouvoir produire un résultat similaire.

Le système évite les dépendances uniques qui bloquent inutilement la 
progression.
⸻
INVARIANTS RESSOURCE → PRODUIT

Toute chaîne de production respecte les invariants suivants, sans
exception :

- **Aucun produit sans ressource.** Un Produit [réf: GDB-005E] ne peut
  jamais être créé sans qu'au moins une Ressource [réf: GDB-005B] ait
  été consommée en amont de la chaîne. Un système qui ferait apparaître
  un produit « depuis rien » viole cet invariant.
- **Conservation à chaque étape.** Une étape de transformation consomme
  une quantité déterminée de ressources ou de produits intermédiaires
  pour produire une quantité déterminée de résultat. Le rendement peut
  varier selon la compétence [réf: GDB-004H] et l'outil [réf: GDB-005D]
  employés, mais jamais produire davantage de valeur en sortie qu'il n'y
  a de ressources en entrée sans une justification explicite (un métier,
  un savoir-faire ou une innovation qui augmente le rendement).
- **Traçabilité.** Chaque Produit conserve une chaîne de provenance
  jusqu'à ses Ressources d'origine. Cette traçabilité n'a pas besoin
  d'être visible du joueur en permanence, mais elle doit exister pour
  que la Valeur [réf: GDB-005I] et la Qualité (voir GDB-005E) restent
  crédibles.
⸻
RÈGLES DE CONCEPTION

Toute chaîne de production devra :

	1.	être crédible ;
	2.	posséder des étapes logiques ;
	3.	favoriser la coopération entre métiers ;
	4.	rester évolutive ;
	5.	enrichir les histoires émergentes.
⸻
CRITÈRE DE VALIDATION

Cette chaîne de production renforce-t-elle l'économie du monde plutôt 
qu'une simple fabrication d'objets ?

Si la réponse est non, elle devra être repensée.
⸻
Fin du document

Statut : Validé -- Référence officielle.
⸻
HISTORIQUE

Version 1.1 : ajout des invariants Ressource → Produit (aucun produit sans
ressource, conservation à chaque étape, traçabilité). Corrige GDB-005-C01. En-tête
mis en conformité avec MASTER-004.

Version 1.0 : création du document.
