# AUDIT-GLOBALE.md

> Version : 3.6
> Statut : GDB et ACT (001-010, 003 excepté) clos --- ENGINE-000 à 006 créés et audités, squelette EventBus mort supprimé (ENGINE-C05) --- ENGINE-006 (Action Pipeline) validé par le porteur du projet, Maturité 4 --- ENGINE-008 (Systems de population) créé, en attente de validation d'équipe --- GDB-004C/004H/004J régénérés à Maturité 2 (Relations, Compétences, Héritage) --- ENGINE/README.md v1.2 (ENGINE-C07 clos) --- 2 constats ouverts : ENGINE-C06 (orchestration Scheduler/Action Pipeline, différé jusqu'à MASTER-005 Phase 3), GDB-CATALOG-C02 (angle mort du repérage par titre de GDB-CATALOG-C01, 3 occurrences déjà corrigées, passage dédié restant à mener) --- autres bibliothèques à approfondir
> Type : Audit
> Maturité : 1
> Bibliothèque : AUDIT
> Document canonique unique

---

# Progression de l'audit

| Bibliothèque | Statut |
|---------------|--------|
| MASTER | ✅ Audité (+ 3 passages d'audit indépendant, corrigés) |
| CORE | ✅ Audité |
| GDB (001 → 030) | ✅ Audité et corrigé intégralement |
| ACT (001 → 002) | ✅ Audité et corrigé intégralement |
| ACT-003 | ⛔ Retiré de la structure cible (redondant avec ACT-001-E et ACT-002-F à I, constaté et tracé dans ACT/CATALOG.md v1.2) --- rien à auditer, l'identifiant ne sera pas réattribué |
| ACT-004 | ✅ Audité (v1.2, 1 constat P1 trouvé et corrigé --- Maturité manquant) --- non encore validé par l'équipe (cycle documentaire ACT-001-G, section 14 : Validée reste une étape distincte de l'audit) |
| ACT-005 | ✅ Audité (v1.2, 3 constats trouvés et corrigés --- 1 P1 citation erronée, 1 P1 Maturité manquant, 1 précision de citation) --- non encore validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| PATTERNS, VERBS | ◻️ Non créés --- rien à auditer tant qu'ils n'existent pas (voir ACT/CATALOG.md) |
| ACT-008 | ✅ Audité (v1.0 ; multiplicité Pattern/Verbe, critère de nouveau Verbe, non-polysémie) --- non encore validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| ACT-009 | ✅ Audité (v1.1, 1 constat P2 corrigé --- imprécision de citation sur ACT-002-I ; tranche la frontière Action composite / Plan) --- non encore validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| ACT-010 | ✅ Audité (v1.0 ; taxonomie des événements, relation avec les Conséquences) --- non encore validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| ACT-006 | ✅ Audité (v1.1 ; taxonomie, périmètre restreint aux catégories stables et règles de composition) --- non encore validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| ACT-007 | ✅ Audité (v1.1 ; taxonomie, dimensions transverses, composition selon la forme de l'Outcome, périmètre restreint) --- non encore validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| ENGINE-000 (Principes) | ✅ Audité (v1.1, 1 constat P1 trouvé et corrigé --- Bibliothèque/Maturité manquants, non-conformité MASTER-004) |
| ENGINE-001 (Journal d'événements) | ✅ Audité (v2.1, révision complète en v2.0 : divergence constatée entre la spécification Subscribe/Handler jamais construite et le mécanisme réel implémenté --- document réécrit pour refléter le code ; v2.1 : squelette EventBus mort trouvé dans le code lors de la vérification du moteur, supprimé) |
| ENGINE-002 (Kernel) | ✅ Audité (v1.0, rédigé rétroactivement --- implémenté depuis la v0.1 du moteur, avant la création de la bibliothèque ENGINE) |
| ENGINE-003 (Scheduler) | ✅ Audité (v1.0, rédigé rétroactivement --- implémenté depuis la v0.2) |
| ENGINE-004 (Systems) | ✅ Audité (v1.0, rédigé rétroactivement, 1 constat corrigé en cours de rédaction --- affirmation erronée sur l'absence de tests NeedsDecaySystem, tests bien existants) |
| ENGINE-005 (Persistence) | ✅ Audité (v1.0, rédigé rétroactivement) |
| ENGINE-006 (Action Pipeline) | ✅ Audité et validé (v1.3, Statut Validée, Maturité 4 --- vérification identifiant pour identifiant sans écart, `PipelineIntegrationTests` observe le comportement décrit, validation du porteur du projet) |
| ENGINE-007 | ◻️ Non créé --- Resource Manager, aucun code existant (voir ENGINE/CATALOG.md). Numéro également invoqué à tort par une proposition externe non retenue (ENGINE-C06, ouvert) --- sans lien avec le Resource Manager |
| ENGINE-008 (Systems de population) | ✅ Audité (v1.0, rédigé avant tout code --- Maturité 2, traduit GDB-004C/004H/004J en architecture concrète) --- non encore implémenté, non encore validé par l'équipe |
| ADR | ✅ Audité en complément (constat ADR-C01, corrigé) |
| TECH | ✅ Audité (corrigé) |
| QA | ✅ Audité (corrigé) |
| UX | ✅ Audité (corrigé) |
| LORE | ✅ Audité (corrigé) |
| PROD | ✅ Audité (corrigé) |
| ART | ✅ Audité (corrigé) |
| AUDIO | ✅ Audité (corrigé) |
| MKT | ✅ Audité (corrigé) |

Toutes les bibliothèques du dépôt ont été auditées au moins une fois. GDB et ACT
ont en outre reçu une correction complète et itemisée de tous leurs constats.

---

# Backlog documentaire

> Ce backlog provient de l'audit initial (GDB-001 → GDB-030, ACT-001 → ACT-002), complété par un constat relevé lors du premier passage d'audit indépendant (GDB-CATALOG-C01). Il n'a pas été retouché par les sessions de correction en cours : ses 90 constats restent ouverts et attendent leur tour, un par un, conformément à MASTER-008.

## GDB-001

### GDB-001-C01 --- ✅ Clos
- **Priorité :** P1
- **Type :** Référence normative
- **Constat :** Hiérarchie Glossaire / CORE absente.
- **Correction :** section « Relation avec CORE » ajoutée à `GDB-001/Readme.md`, établissant la frontière entre philosophie de conception (GDB-001) et primitives structurelles (CORE), en complément du correctif déjà apporté à GDB-001J.

### GDB-001-C02 --- ✅ Clos
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Arbitrage des principes fondateurs absent.
- **Correction :** création de `GDB-001I-2.md` (Arbitrage des Principes Fondateurs), qui identifie et tranche quatre tensions réelles entre les principes de GDB-001A à I. Découverte pendant l'analyse d'impact : aucun format de nommage n'existait pour un second document dans une section --- formalisé dans MASTER-003 v1.3 (`GDB-001I-2`, sans onzième lettre).

---

## GDB-002

### GDB-002-C01 --- ✅ Clos
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Critères de persistance de la mémoire absents.
- **Correction :** GDB-002B enrichi d'un système à quatre paliers (Anecdote, Souvenir, Légende, Tradition) avec conditions d'entrée et de sortie explicites.

### GDB-002-C02 --- ✅ Clos
- **Priorité :** P1
- **Type :** Cycle de vie
- **Constat :** Cycle de vie des opportunités absent.
- **Correction :** GDB-002E enrichi du cycle complet Latente → Visible → (Saisie | Ignorée) → Résolue, avec renvoi vers ACT-002 et GDB-002B/D.

### GDB-002-C03 --- ✅ Clos
- **Priorité :** P1
- **Type :** Responsabilité
- **Constat :** Mémoire persistante / mémoire de simulation non distinguées.
- **Correction :** GDB-002B précise désormais la frontière entre Mémoire du Monde (narrative, curatée) et mémoire de simulation (State/Event du Kernel), avec référence explicite à CORE-000C.

---

## GDB-003

### GDB-003-C01 --- ✅ Clos
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Cardinalités géographiques absentes.
- **Correction :** GDB-003A enrichi d'un tableau de cardinalités parent/enfant (Monde → Continent → Région → Zone → Lieu → Point d'intérêt) et de trois invariants de rattachement.

### GDB-003-C02 --- ✅ Clos
- **Priorité :** P1
- **Type :** Modèle de données
- **Constat :** Relation Location / Point of Interest absente.
- **Correction :** GDB-003F précise la relation : un Point d'intérêt appartient toujours à une Zone, parfois en plus à un Lieu (intégré ou isolé).

### GDB-003-C03 --- ✅ Clos
- **Priorité :** P2
- **Type :** Définition
- **Constat :** Statut documentaire des frontières absent.
- **Correction :** GDB-003H clarifie qu'une frontière est une qualification de Zone(s) contiguës, non un niveau supplémentaire de la hiérarchie.

---

## GDB-004

### GDB-004-C01 --- ✅ Clos
- **Priorité :** P1
- **Type :** Responsabilité
- **Constat :** Frontière Connaissance / Compétence absente.
- **Correction :** GDB-004G établit le critère de distinction (communication contre pratique) et ses conséquences sur la transmission ; GDB-004H y renvoie.

### GDB-004-C02 --- ✅ Clos
- **Priorité :** P2
- **Type :** Cycle de vie
- **Constat :** Cycle de vie des traits de personnalité absent.
- **Correction :** GDB-004D enrichi du cycle Formation → Stabilisation → Inflexion → Nouvelle stabilisation, avec invariant de causalité.

### GDB-004-C03 --- ✅ Clos
- **Priorité :** P2
- **Type :** Pipeline
- **Constat :** Cas d'échec de la transmission absents.
- **Correction :** GDB-004J enrichi de trois cas d'échec (absence de successeur, refus, transmission incomplète) et d'un invariant commun.

---

## GDB-005

### GDB-005-C01 --- ✅ Clos
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Invariants Ressource → Produit absents.
- **Correction :** GDB-005C enrichi de trois invariants (aucun produit sans ressource, conservation à chaque étape, traçabilité).

### GDB-005-C02 --- ✅ Clos
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Invariants du marché absents.
- **Correction :** GDB-005G enrichi de quatre invariants (localité de l'information, bornes de variation, pas d'arbitrage sans coût, mémoire du marché).

### GDB-005-C03 --- ✅ Clos
- **Priorité :** P1
- **Type :** Référence normative
- **Constat :** Valeur économique / CORE Value non reliées.
- **Correction :** GDB-005I distingue la Valeur économique (jugement contextuel) de CORE Value (conteneur de donnée typée), avec référence explicite à CORE-000C.

### GDB-005-C04 --- ✅ Clos
- **Priorité :** P2
- **Type :** Cycle de vie
- **Constat :** Cycle de vie des investissements absent.
- **Correction :** GDB-005J enrichi du cycle Engagement → Maturation → (Rendement | Stagnation | Échec) → Clôture ou Réinvestissement.

---

## GDB-006 → GDB-030

### Constat consolidé --- traité

Les 25 chapitres ont été relus intégralement (readme + documents clés) et corrigés
un par un. Le détail complet des corrections figure dans l'historique de chaque
document concerné ; résumé par chapitre :

| Chapitre | Correction principale |
|---|---|
| GDB-006 | Frontière Souvenir (joueur) / Mémoire du Monde (GDB-002B) --- GDB-006H |
| GDB-007 | Frontière systémique avec GDB-004H/GDB-001J (compétence, maîtrise) --- Readme |
| GDB-008 | Doublons « Le Temps » et « Mémoire du Monde » résolus avec GDB-001E/GDB-002B --- GDB-008A, GDB-008I |
| GDB-009 | Doublon « Les Lois » (→ GDB-018B) et « Les Conflits » (→ GDB-015H) résolus ; relation genre/espèce Institution/Organisation (→ GDB-020A) --- GDB-009F, G, I |
| GDB-010 | Doublon « Biomes » résolu (rattachement géographique vs écosystème) --- GDB-010F |
| GDB-011 | Doublon « Opportunités » résolu (cycle de vie vs déclenchement systémique) --- GDB-011E |
| GDB-012 | 3 doublons résolus avec GDB-005 (Métiers, Outils, Chaînes de Production) --- GDB-012A/D/F |
| GDB-013 | Référence normative ajoutée vers GDB-002B pour la notion de patrimoine --- GDB-013H |
| GDB-014 | 3 doublons résolus (Exploration, Découvertes avec GDB-006 ; Points d'Intérêt avec GDB-003F) --- GDB-014A/E/H |
| GDB-015 | 2 doublons résolus (Blessures avec GDB-022C ; Conflits avec GDB-009I) --- GDB-015E/H |
| GDB-016 | Cycle de vie complet d'un traité ajouté --- GDB-016C |
| GDB-017 | Frontière avec GDB-009B pour la communauté générique --- GDB-017H |
| GDB-018 | Doublon « Les Lois » résolu en retour (application judiciaire vs légitimité) --- GDB-018B |
| GDB-019 | Doublon « Les Marchés » résolu (typologie commerciale vs invariants) --- GDB-019E |
| GDB-020 | Relation genre/espèce Organisation/Institution --- GDB-020A |
| GDB-021 | Doublon « L'Apprentissage » résolu (institution éducative vs expérience joueur) --- GDB-021B |
| GDB-022 | Doublon « Les Blessures » résolu en retour (mécanisme médical vs contexte de combat) --- GDB-022C |
| GDB-023 | Chevauchement de chapitre entier avec GDB-029 clarifié (traduction en progrès jouable vs principe épistémique) ; tableau des documents corrigé (B/C/G ne correspondaient plus aux titres réels) --- Readme, GDB-023B/C/G (via Readme) |
| GDB-024 | Relation genre/espèce Source d'énergie/Ressource --- GDB-024A |
| GDB-025 | Frontière avec GDB-003G (véhicules vs réseaux géographiques) --- GDB-025A |
| GDB-026 / GDB-027 | Frontière canal (communication) / contenu (information) établie dans les deux sens --- GDB-026A, GDB-027A |
| GDB-028 | Doublon « Les Traditions » résolu en retour (institution culturelle vs angle générationnel) --- GDB-028C |
| GDB-029 | Chevauchement avec GDB-023 clarifié en retour --- Readme |
| GDB-030 | Frontière avec GDB-023 (déploiement durable vs invention) --- GDB-030A |

### GDB-CATALOG-C01 --- ✅ Clos
- **Priorité :** P2
- **Type :** Cohérence terminologique
- **Constat :** 19 titres de documents identiques répétés entre chapitres.
- **Correction :** les 19 paires ont chacune reçu une frontière explicite (l'un des deux documents fait autorité sur le mécanisme, l'autre sur une dimension complémentaire), avec renvois croisés `[réf: ...]` dans les deux sens et titres précisés lorsque nécessaire. Table détaillée dans `GDB/CATALOG.md`.

### GDB-CATALOG-C02 --- ⏳ Ouvert (portée non traitée entièrement)
- **Priorité :** P2
- **Type :** Méthodologie d'audit
- **Constat :** `GDB-CATALOG-C01` appariait les chapitres par **titre de
  document identique**. Ce repérage a un angle mort : deux documents
  peuvent traiter le même sujet sous des titres différents, sans jamais
  être rapprochés par une comparaison de titres. Trois occurrences de ce
  défaut, non couvertes par `GDB-CATALOG-C01`, ont été découvertes
  incidemment en régénérant `GDB-004C`, `GDB-004H` et `GDB-004J` pour
  atteindre la précision opérationnelle requise avant une future spec
  ENGINE (Relations/Compétences/Héritage) :
  1. `GDB-004H` (Les Compétences) / `GDB-007A` (Les Compétences du
     Joueur) --- même mécanique, titres différents, aucun renvoi croisé.
  2. `GDB-004H` / `GDB-007B` (La Maîtrise) --- recoupement partiel, même
     défaut.
  3. `GDB-004J` (La Transmission) / `GDB-008G` (L'Héritage) --- « ce qui
     peut être transmis » quasi identique entre les deux, aucun renvoi
     croisé.
- **Correction partielle déjà appliquée :** les trois paires ci-dessus
  ont chacune reçu une frontière explicite dans les deux sens
  (`GDB-004C` v1.1, `GDB-004H` v1.2, `GDB-004J` v1.2, `GDB-007A` v1.1,
  `GDB-007B` v1.1, `GDB-008G` v1.1) --- au passage, mise en conformité
  MASTER-004 des documents qui n'avaient encore ni `Maturité` ni
  `Bibliothèque` (`GDB-004C`, `GDB-007A`, `GDB-007B`, `GDB-008G`).
- **Ce qui reste ouvert :** ces trois paires ont été trouvées
  incidemment, pas par une recherche systématique. Un passage d'audit
  dédié, comparant les 30 chapitres de la GDB par **concept** plutôt que
  par titre (par exemple : chaque paire de documents dont l'ensemble des
  sections IMPACT/INTERACTIONS se recoupe significativement), reste à
  mener pour savoir si d'autres occurrences du même défaut existent
  ailleurs dans le dépôt.
- **Condition de clôture :** réalisation de ce passage d'audit dédié,
  qu'il trouve ou non de nouvelles occurrences --- sa seule exécution,
  pas son résultat, ferme ce constat.

---

# ACT

## ACT-001

### ACT-001-C01 --- ✅ Clos
- **Priorité :** P1
- **Type :** Référence normative
- **Constat :** Hiérarchie normative ACT / GDB non explicitée.
- **Correction :** en le corrigeant, découverte qu'ACT-001-I référençait encore STANDARDS (bibliothèque retirée, absorbée par MASTER via ADR-003) et n'incluait jamais CORE. Hiérarchie corrigée (MASTER → CORE → GDB → ACT → TECH → QA → CODE) dans ACT-001A et ACT-001I, CORE ajouté aux dépendances entrantes.

### ACT-001-C02 --- ✅ Clos
- **Priorité :** P1
- **Type :** Invariant
- **Constat :** Critères d'entrée d'une mécanique dans ACT absents.
- **Correction :** ACT-001G enrichi de quatre tests séquentiels (universalité, composition, responsabilité unique, non-duplication) déterminant si une mécanique candidate entre dans ACT.

### ACT-001-C03 --- ✅ Clos
- **Priorité :** P2
- **Type :** Cycle de vie
- **Constat :** Cycle de vie documentaire d'une mécanique absent.
- **Correction :** ACT-001G enrichi du cycle Proposée → Validée → Spécifiée → Implémentée → Testée → Stable, aligné sur les niveaux de maturité de MASTER-004, distinct du cycle de vie d'exécution (ACT-001-E).

---

## ACT-002

### ACT-002-C01 --- ✅ Clos
- **Priorité :** P1
- **Type :** Pipeline
- **Constat :** Pipeline d'exécution d'une action absent.
- **Correction :** ACT-002F enrichi d'un pipeline unifié intégrant Intent, Plan, Action Instance et Outcome --- jusqu'ici documentés séparément (G, H, I) sans jamais être reliés à la chaîne d'exécution de la section 3, alors que la GDB (GDB-002E) y faisait déjà référence comme si le lien existait.

### ACT-002-C02 --- ✅ Clos
- **Priorité :** P1
- **Type :** Responsabilité
- **Constat :** Frontière Action / Interaction absente.
- **Correction :** ACT-002C enrichi d'une définition précise : une Interaction est une Action dont la Cible est un Acteur capable de produire sa propre réponse dans le même événement causal (convaincre, négocier) ; ce n'est jamais un niveau supplémentaire du modèle.

### ACT-002-C03 --- ✅ Clos
- **Priorité :** P2
- **Type :** Invariant
- **Constat :** Conditions d'échec d'une action incomplètes.
- **Correction :** ACT-002F enrichi d'une taxonomie à trois catégories (invalidité interne, disparition, ressources) avec un invariant commun sur la production d'événements et la libération des ressources réservées.

---

# Constats de l'audit indépendant --- premier passage --- tous clos (9)

MASTER-C01, MASTER-C02, ADR-C01, GDB-C01, GDB-C02, ACT-C01, ACT-C02, ACT-C03, ACT-C04. Détail conservé dans l'historique des documents concernés (MASTER-001 à 007, ADR-003, GDB-001J, ACT/CATALOG.md, ACT/readme.md, ACT-002E/G/H).

---

# Constats de l'audit indépendant --- second passage (auto-vérification) --- tous clos (3)

MASTER-004-C03, GDB-C03, AUDIT-C01. Détail conservé dans l'historique de MASTER-004, GDB-001J et du présent document.

---

# Constats de l'audit indépendant --- troisième passage (bibliothèques restantes) --- tous clos (10)

> Ce passage a audité les 8 bibliothèques qui n'avaient jamais été lues (TECH, QA, UX, LORE, PROD, ART, AUDIO, MKT). Deux constats supplémentaires ont été découverts pendant l'analyse d'impact de la correction, conformément à MASTER-008 section 6.

### STUB-C01 --- P1 --- Bibliothèques vides au-delà de leur propre description --- ✅ Clos
- **Constat :** TECH, QA, UX, LORE, ART, AUDIO, MKT ne contenaient chacune qu'un readme se décrivant elle-même, sans aucun document numéroté malgré la convention annoncée.
- **Correction :** les 7 readme régénérés avec une section « État actuel » énonçant honnêtement qu'aucun document n'existe encore.

### STUB-C02 --- P2 --- Absence totale de métadonnées documentaires --- ✅ Clos
- **Correction :** en-tête MASTER-004 (Version, Statut, Type, Maturité, Bibliothèque) ajouté aux 7 readme, ainsi qu'à PROD/readme.md.

### STUB-C03 --- P3 --- Séparateur non conforme --- ✅ Clos
- **Correction :** « — » remplacés par « --- » dans les 7 readme et PROD/readme.md.

### PROD-C01 --- P1 --- Chevauchement non référencé entre FeuilleDeRoute.md et ADR-002 --- ✅ Clos
- **Correction :** section « Choix techniques (ADR-002) » supprimée de FeuilleDeRoute.md, remplacée par des renvois `[réf: ADR-002]`.

### PROD-C02 --- P2 --- Contenu technique hébergé hors de TECH --- ✅ Clos
- **Correction :** FeuilleDeRoute.md ne détaille plus les choix techniques, il y renvoie.

### PROD-C03 --- P1 --- Contradiction d'ordre de phases avec MASTER-005 --- ✅ Clos
- **Constat découvert pendant l'analyse d'impact de PROD-C01/C02 :** FeuilleDeRoute.md plaçait v0.4 *La profondeur* avant v0.5 *Le monde vivant*, alors que MASTER-005 (rang supérieur) place Phase 3 *Le monde vivant* avant Phase 4 *La profondeur*.
- **Correction :** v0.4 et v0.5 inversés dans FeuilleDeRoute.md pour suivre MASTER-005, décision validée par le porteur du projet.

### GLOBAL-C01 --- P2 --- Incohérence de casse des fichiers readme --- ✅ Clos
- **Correction :** `ACT/Readme.md` renommé en `ACT/readme.md` ; règle de casse ajoutée à MASTER-004 (v1.4) pour éviter toute nouvelle dérive.

### MASTER-003-C02 --- P2 --- Registre AUDIT non déclaré --- ✅ Clos
- **Correction :** MASTER-003 (v1.2) déclare désormais officiellement le registre AUDIT, distinct des bibliothèques et du registre ADR.

### GLOBAL-C02 --- P3 --- Nom de dossier et de fichier hors convention --- ✅ Clos
- **Correction :** contenu absorbé dans un nouveau document `MASTER-008`, dossier et fichier corrompus supprimés. Décision tracée par `ADR-004`.

### MASTER-C03 --- P2 --- Tableau des documents MASTER obsolète et erroné --- ✅ Clos
- **Constat découvert pendant l'analyse d'impact de la création de MASTER-008 :** `MASTER/readme.md` décrivait MASTER-007 comme « Gestion des dépendances documentaires » (faux --- il s'agit de « Standards de qualité ») et ne mentionnait pas MASTER-008.
- **Correction :** `MASTER/readme.md` régénéré (v1.1), tableau corrigé et complété, en-tête mis en conformité.

---

# Dette de migration MASTER-004 (suivi, distinct des constats d'incohérence)

> Chantier de mise en conformité progressive, non compté dans les statistiques de constats. Un document n'est mis en conformité qu'au moment de sa régénération pour un motif réel, jamais par un ajout mécanique isolé (MASTER-008, section 4).

| Bibliothèque | Documents totaux | `Maturité` présent | `Bibliothèque` présent |
|---|---|---|---|
| MASTER | 9 | 8 / 9 | 8 / 9 |
| CORE | 115 | 0 / 115 | 101 / 115 |
| GDB | 333 | 1 / 333 | 5 / 333 |
| ACT | 21 | 0 / 21 | 21 / 21 |
| TECH, QA, UX, LORE, ART, AUDIO, MKT | 1 chacune | 100 % | 100 % |
| PROD | 2 | 2 / 2 | 2 / 2 |

Les 8 bibliothèques auditées lors de ce troisième passage sont désormais entièrement conformes, chacune ne comptant qu'un seul document. CORE, GDB et ACT restent le gros de la dette --- attendue, puisqu'aucun constat réel ne les a encore fait régénérer document par document.

---

# Statistiques

## Backlog documentaire

Le décompte initial (90 constats, P1:52/P2:38) incluait un solde de 68 constats
jamais énumérés individuellement : ils correspondaient au bloc générique
« GDB-006 → GDB-030 » (52 - 15 = 37 P1 restants, 38 - 3 = 35 P2 restants, moins
GDB-CATALOG-C01 déjà compté à part). Ce bloc n'a jamais eu de détail
constat-par-constat comme GDB-001 à GDB-005 --- seulement l'affirmation qu'il
« correspond exactement » à ce qui précède.

Ce passage a traité ce bloc concrètement : les 25 chapitres ont été relus et
corrigés un par un (tableau ci-dessus), en ciblant précisément les catégories
que le constat générique annonçait --- pipelines, cycles de vie, frontières,
références normatives, invariants, chevauchements. Ce traitement ne produit pas
68 constats numérotés individuellement (ils n'ont jamais existé sous cette
forme), mais ferme le bloc générique dans son ensemble.

Les 22 constats explicitement numérotés du backlog original sont tous clos :
GDB-001-C01/C02, GDB-002-C01/C02/C03, GDB-003-C01/C02/C03, GDB-004-C01/C02/C03,
GDB-005-C01/C02/C03/C04, GDB-CATALOG-C01, ACT-001-C01/C02/C03, ACT-002-C01/C02/C03.

| Priorité | Nombre |
|-----------|--------|
| P0 | 0 |
| P1 | 0 |
| P2 | 0 |
| P3 | 0 |

**Total backlog ouvert : 0**

## Audit indépendant --- récapitulatif des trois passages

| Passage | Trouvés | Corrigés | Restants |
|---|---|---|---|
| 1er (bibliothèques principales) | 9 | 9 | 0 |
| 2e (auto-vérification) | 3 | 3 | 0 |
| 3e (bibliothèques restantes) | 10 | 10 | 0 |
| **Total** | **22** | **22** | **0** |

## Total général

**0 constat du backlog documentaire ouvert + 0 constat d'audit indépendant restant = 0 constat à traiter sur GDB et ACT.**

Le backlog documentaire initial du dépôt (GDB et ACT) est intégralement traité. Ce total ne compte pas `GDB-CATALOG-C02`, constat distinct ouvert lors de sessions de travail ultérieures (voir section ENGINE/GDB ci-dessous) --- même logique que pour `ENGINE-C06`, qui n'entre pas non plus dans ce décompte historique.

---

# État d'avancement

## Bibliothèques auditées

Toutes (MASTER, CORE, GDB, ACT, ENGINE, ADR, TECH, QA, UX, LORE, PROD, ART, AUDIO, MKT).

## Retiré (n'existera jamais sous cet identifiant)

- ACT-003 --- redondant avec ACT-001-E et ACT-002-F à I (voir ACT/CATALOG.md v1.2, section « Chapitre retiré »)

## Audités, non encore validés par l'équipe

- ACT-004 (v1.2)
- ACT-005 (v1.2)
- ACT-006-A (v1.1 ; taxonomie, périmètre restreint)
- ACT-007-A (v1.1 ; taxonomie, périmètre restreint)
- ACT-008-A (v1.0), ACT-009-A (v1.1), ACT-010-A (v1.0) --- taxonomie des
  verbes, composition d'Actions, taxonomie des événements ; ACT-001 à
  ACT-010 sont désormais tous créés (ACT-003 excepté, retiré)
- ENGINE-000 (v1.1), ENGINE-001 (v2.1), ENGINE-002 à ENGINE-005 (v1.0),
  CATALOG.md (v1.2) --- bibliothèque ENGINE, introduite par PROD-005
  (Feuille de Route v2.2) et documentée rétroactivement pour ses
  composants déjà codés (voir section dédiée ci-dessous)
- ENGINE-008-A (v1.0) --- Systems de population (Relations,
  Compétences, Héritage), deuxième document ENGINE rédigé avant tout
  code, traduisant GDB-004C/004H/004J en architecture concrète

---

# Relecture interne et audit formel systématiques (nouvelle pratique)

À partir de cette session, tout document généré ou régénéré fait l'objet,
avant d'être livré :

1. d'une **relecture interne rapide** --- cohérence des renvois croisés,
   citations vérifiées à l'endroit exact cité ;
2. puis d'un **audit formel** au sens de MASTER-008 --- lecture complète,
   conformité à l'en-tête MASTER-004, vérification systématique de
   chaque citation contre le contenu réel du document cité, constats
   numérotés et priorisés.

Objectif : réduire les allers-retours de correction. Cette pratique ne
remplace pas la validation d'équipe (cycle documentaire ACT-001-G,
section 14), qui reste une étape distincte, requise séparément, et que
ni la relecture ni l'audit ne peuvent accorder eux-mêmes.

## Constats trouvés sur ACT-004 et ACT-005 (relecture + audit formel)

- **ACT-005-C01 (P1, corrigé en v1.1)** --- section 6 (Rôle d'une Cible)
  attribuait à tort la désignation de la Cible principale à l'Intent
  d'origine, en citant ACT-002-H à l'appui d'une affirmation que cette
  section ne soutient pas explicitement. Corrigé : la Cible principale
  est désignée par l'Action Definition, pas par l'Intent.
- **ACT-004-C01 (P3, corrigé en v1.1)** --- renvoi générique vers « le
  futur ACT-005 » (section 8, Auto-ciblage), devenu imprécis depuis la
  création effective d'ACT-005. Précisé vers ACT-005 section 9.
- **ACT-004-C02 / ACT-005-C02 (P1, corrigés en v1.2)** --- champ
  obligatoire `Maturité` absent de l'en-tête des deux documents depuis
  leur création, en non-conformité avec MASTER-004 (obligatoire pour
  tout document créé après sa v1.2 ; les deux documents sont trop
  récents pour relever de la dette de migration qui couvre CORE et une
  partie de GDB/ACT). Valeur retenue : 2 (Spécification, MASTER-007),
  cohérente avec les sous-documents d'ACT-002 de même nature.
- **ACT-005-C03 (P2, corrigé en v1.2)** --- la citation ajoutée par la
  correction d'ACT-005-C01 (ci-dessus) était elle-même imprécise : elle
  attribuait à ACT-002-H, section Indépendance, le fait explicite qu'un
  Intent ne connaît pas de Cible, alors que cette section dit
  littéralement qu'un Intent ne connaît pas les *Actions*. La chaîne
  logique complète (Intent ignore les Actions --- une Cible est une
  propriété d'une Action --- donc un Intent ne peut pas porter de Cible)
  est désormais explicite plutôt que raccourcie.

Aucun des quatre constats n'a nécessité de revoir la structure ou les
invariants des documents --- uniquement des précisions de citation et
un ajout de champ d'en-tête obligatoire.

## Constats trouvés sur ACT-007 (et un oubli sur ACT-006)

- **ACT-007-C01 (P2, corrigé avant livraison)** --- section 4
  (Réversibilité) attribuait à tort à ACT-004-A, section 6, une
  affirmation sur l'irréversibilité de la mort qu'elle ne contient pas ;
  ACT-004-A section 5 utilise seulement la mort comme exemple d'état
  disqualifiant, sans se prononcer sur sa réversibilité. Reformulé pour
  ne plus sur-attribuer cette affirmation.
- **ACT-007-C02 (P3, corrigé avant livraison)** --- référence vague à
  ACT-001-E (« section sur l'interruption ») précisée (section 5,
  Interruptions).
- **ACT-CATALOG-C02 (P2, corrigé)** --- en traitant ACT-007, découverte
  que la sous-section descriptive `## ACT-006 --- Conditions` du
  catalogue était restée dans « Chapitres planifiés, non créés » depuis
  sa création (v1.3), alors que la structure générale du même catalogue
  la marquait déjà correctement « créé ». Même défaut que celui déjà
  corrigé une fois pour ACT-004 (voir Historique d'ACT/CATALOG.md,
  version 1.2) --- réapparu pour ACT-006 sans avoir été généralisé en
  vérification systématique. Corrigé dans ACT/CATALOG.md v1.4 : les deux
  vues (structure générale et sous-section descriptive) sont désormais
  revérifiées ensemble à chaque création de chapitre.

Les trois constats ci-dessus ont été trouvés et corrigés avant la
première livraison des documents concernés.

## Constats trouvés sur ENGINE (documentation rétroactive + audit formel)

Contexte : PROD-005 (Feuille de Route v2.2) introduit la bibliothèque
ENGINE et la règle « toute évolution importante du moteur doit d'abord
être décrite dans ENGINE avant d'être implémentée » (ENGINE-000,
section 3). Décision explicite du porteur de projet : cette règle
s'applique aussi rétroactivement aux composants déjà codés sans
spécification ENGINE préalable (Kernel, Scheduler, Systems,
Persistence).

- **ENGINE-C01 (P0, corrigé en v2.0)** --- divergence de fond entre
  ENGINE-001 (Statut : Proposition, décrivait une architecture
  Subscribe/Handler avec abonnement par type d'événement) et le code
  réellement implémenté (`World.Publish`/`World.Events`, une simple
  liste accumulée, sans abonnement ni distribution, utilisée par
  `AgingSystem` depuis la v0.2). Décision du porteur de projet : réviser
  ENGINE-001 pour refléter le mécanisme réel plutôt que de construire le
  Subscribe/Handler jamais requis par aucun besoin réel (MASTER-006).
  Document renommé « Journal d'événements du World », passé de Maturité
  2 à Maturité 3.
- **ENGINE-C02 (P1, corrigé)** --- ENGINE-000 (Principes) et le Readme
  de la bibliothèque utilisaient un champ d'en-tête `Famille` qui
  n'existe pas dans le format prescrit par MASTER-004 (le champ
  obligatoire s'appelle `Bibliothèque`), et n'avaient pas le champ
  obligatoire `Maturité`. Non-conformité pré-existante, propagée sans
  le vouloir dans les nouveaux documents ENGINE-002 à 005 avant d'être
  repérée et corrigée partout.
- **ENGINE-C03 (P2, corrigé en cours de rédaction)** --- une première
  version d'ENGINE-004 (Systems) affirmait qu'aucun test dédié
  n'existait pour `NeedsDecaySystem`. Vérification faite avant
  livraison : `NeedsDecaySystemTests.cs` existe et couvre 6 cas.
  Affirmation corrigée avant tout envoi.
- **ENGINE-C04 (P2, corrigé en cours de rédaction)** --- une première
  version d'ENGINE-003 (Scheduler) affirmait qu'aucun test n'exerçait
  directement `Scheduler.Register`/`Scheduler.Tick`. Vérification faite
  avant livraison : `SchedulerTests.cs` existe et couvre les trois
  invariants du document. Affirmation corrigée avant tout envoi.
- **ENGINE-C05 (P1, corrigé)** --- en vérifiant le moteur suite à la
  création d'ENGINE-002 à 005, découverte d'un dossier
  `Kernel/EventBus/` correspondant exactement à l'architecture
  Subscribe/Handler qu'ENGINE-001 v1.0 décrivait --- code jamais
  terminé (chaque méthode levait `NotImplementedException`), jamais
  référencé ailleurs dans le moteur. Ce squelette contredisait
  silencieusement ENGINE-001 v2.0, déjà révisé pour refléter le
  mécanisme réel (`World.Publish`/`Events`). Décision du porteur de
  projet : supprimer le dossier. ENGINE-001 passe en v2.1.

ENGINE-C03 et ENGINE-C04 n'ont jamais atteint l'utilisateur : trouvés et
corrigés pendant la phase d'audit formel elle-même, avant la première
livraison des documents --- exactement l'objectif de la pratique
décrite ci-dessus. ENGINE-C05 illustre l'utilité du contrôle inverse ---
vérifier le code à la lumière de la documentation, pas seulement l'autre
sens --- désormais recommandé après toute création ou révision d'un
document ENGINE touchant un composant déjà codé (voir Prochaine étape
recommandée).

### ENGINE-C06 --- ⏳ Ouvert (différé volontairement)
- **Priorité :** P2
- **Type :** Lacune architecturale
- **Origine :** proposition externe (« ChatGPT »), soumise sous
  l'identifiant `ENGINE-007 --- Simulation Loop`, statut auto-déclaré
  « Validé ». Non retenue telle quelle --- trois défauts de traçabilité :
  1. `ENGINE-007` est déjà réservé au Resource Manager (voir
     `ENGINE/CATALOG.md`, section « Chapitres planifiés, non créés ») ;
  2. elle recrée une séparation Scheduler / Simulation Loop déjà
     tranchée et consolidée dans `ENGINE-003` (« le code n'a jamais
     séparé les deux : `Scheduler.Tick` fait avancer le World *et*
     invoque les Systems »), sans fournir la justification explicite
     que le catalogue exige pour rouvrir cette consolidation ;
  3. un statut « Validé » ne peut pas s'auto-attribuer à un document
     anticipant du code non écrit --- seul précédent comparable,
     `ENGINE-006`, est entré au catalogue en `Proposition`, Maturité 2.
- **Constat :** au-delà du rejet de la proposition elle-même, elle
  pointe une lacune réelle et non encore adressée : aucun composant du
  moteur n'orchestre aujourd'hui le `Scheduler` (Systems) et le Pipeline
  d'Actions (`ENGINE-006`) au sein d'un même Tick. `Scheduler.Tick` n'a
  connaissance que des Systems. Le Pipeline existe bien en code
  (`Actions/`, dont `PipelineRunner`, 91/91 tests passants) --- **contrairement
  à une première version de ce constat qui affirmait à tort le
  contraire, corrigée avant clôture de la session** --- mais il reste
  câblé à la main pour l'unique Verbe de démonstration « Se reposer »
  (`PipelineRunner.ExecuterSeReposer`), invoqué manuellement, jamais par
  `Scheduler` ni par aucun autre point d'entrée automatique du Tick.
- **Décision :** ne pas rédiger de spécification ENGINE par
  anticipation (MASTER-006) --- généraliser `PipelineRunner` au-delà d'un
  Verbe unique, ou l'intégrer au Tick, sans qu'un besoin réel ne le
  démontre, serait anticiper (cf. le commentaire de `PipelineRunner.cs`
  lui-même sur ce point). Examiné explicitement par le porteur du projet
  au moment de valider `ENGINE-006` (v1.3, voir son Historique) : les
  deux limitations que ce constat décrit ne sont pas des écarts à
  corriger dans ce document ni dans `ENGINE-006` --- l'invocation
  automatique par Tick est un besoin de `MASTER-005` Phase 3 (habitants
  autonomes), pas de la Phase 1 en cours, où les Actions sont
  déclenchées par les choix du joueur ; elle pourrait même s'avérer la
  mauvaise architecture pour des Actions joueur. Trancher ce point avant
  la Phase 3 reviendrait à décider sans les données nécessaires. Constat
  consigné ici pour ne pas le perdre, à rouvrir explicitement à l'entrée
  en Phase 3. À cette occasion : choisir un identifiant réellement libre
  (pas `ENGINE-007`, toujours réservé au Resource Manager) et fournir la
  justification de réouverture de la consolidation `ENGINE-003`.
- **Condition de clôture :** entrée en Phase 3 de `MASTER-005` ---
  pas avant, et pas simplement à l'apparition d'un second Verbe (question
  de contenu GDB/VERBS, sans rapport avec ce constat d'architecture).

### ENGINE-C07 --- ✅ Clos
- **Priorité :** P2
- **Type :** Cohérence documentaire
- **Constat :** `ENGINE/README.md` affirmait que cette bibliothèque « ne
  contient aucun code source », alors que `ENGINE-006` et `ENGINE-008`
  contiennent des esquisses de code concrètes (types C#, signatures).
- **Correction :** Option A retenue par le porteur du projet. `ENGINE/README.md`
  v1.2 corrige la doctrine : ENGINE peut contenir des esquisses de code
  lorsqu'elles sont nécessaires pour exprimer un contrat avec précision.
  La section « Implémentation indépendante » est renommée et reformulée.
  La section 5 (Organisation) est mise à jour pour refléter la structure
  réelle de la bibliothèque.

## Non concerné (n'existe pas encore)

- ACT/PATTERNS
- ACT/VERBS

---

# Prochaine étape recommandée

GDB (001 à 030) et ACT (001 à 010) sont désormais intégralement traités : 0
constat ouvert (ACT-003 excepté, retiré). La dette de migration MASTER-004
(Maturité/Bibliothèque manquants sur CORE et une partie de GDB) reste le
principal chantier de fond, à traiter au fil des prochaines régénérations
plutôt que par une campagne dédiée (MASTER-008, section 4). TECH, QA, UX, LORE,
PROD, ART, AUDIO, MKT restent des bibliothèques à un seul document chacune :
leur prochaine étape naturelle est la rédaction de leurs premiers documents
numérotés, pas un nouvel audit.

Suite à ENGINE-C05 : toute création ou révision d'un document ENGINE portant
sur un composant déjà codé doit désormais s'accompagner d'une vérification
dans l'autre sens --- le code contredit-il la documentation, pas seulement
l'inverse (recherche de code mort, de scaffolding non terminé, ou de
mécanismes parallèles non référencés) --- avant de considérer le document
comme fiable à 100 %.

ENGINE-006 (Action Pipeline) est validé par le porteur du projet (v1.3, Statut
Validée, Maturité 4) --- premier document ENGINE à parcourir tout le cycle
Spécification → Implémentation → Tests → Validation (ENGINE-000, section 8).

ENGINE-C06 reste ouvert et différé volontairement : à rouvrir à l'entrée en
Phase 3 de MASTER-005 (habitants autonomes), moment où l'orchestration
automatique Scheduler / Pipeline d'Actions cessera d'être hors sujet pour la
Phase en cours --- pas avant, et pas simplement à l'apparition d'un second
Verbe (question de contenu GDB/VERBS, sans rapport avec ce constat).
