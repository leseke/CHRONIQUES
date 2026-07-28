# AUDIT-GLOBALE.md

> Version : 2.2
> Statut : GDB et ACT (001-002) clos --- ACT-003 retiré, ACT-004 et ACT-005 créés en Proposition --- autres bibliothèques à approfondir
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
| ACT-004 | 🟡 Créé (Statut : Proposition) --- rédigé mais non encore audité ni validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| ACT-005 | 🟡 Créé (Statut : Proposition) --- rédigé mais non encore audité ni validé par l'équipe (cycle documentaire ACT-001-G, section 14) |
| ACT (006 → 010), PATTERNS, VERBS | ◻️ Non créés --- rien à auditer tant qu'ils n'existent pas (voir ACT/CATALOG.md) |
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

Le backlog documentaire initial du dépôt (GDB et ACT) est intégralement traité.

---

# État d'avancement

## Bibliothèques auditées

Toutes (MASTER, CORE, GDB, ACT, ADR, TECH, QA, UX, LORE, PROD, ART, AUDIO, MKT).

## Retiré (n'existera jamais sous cet identifiant)

- ACT-003 --- redondant avec ACT-001-E et ACT-002-F à I (voir ACT/CATALOG.md v1.2, section « Chapitre retiré »)

## Créé, non encore audité

- ACT-004 (Statut : Proposition)
- ACT-005 (Statut : Proposition)

## Non concerné (n'existe pas encore)

- ACT-006 → ACT-010
- ACT/PATTERNS
- ACT/VERBS

---

# Prochaine étape recommandée

GDB (001 à 030) et ACT (001 et 002) sont désormais intégralement traités : 0
constat ouvert. La dette de migration MASTER-004 (Maturité/Bibliothèque
manquants sur CORE et une partie de GDB/ACT, voir section dédiée) reste le
principal chantier de fond, à traiter au fil des prochaines régénérations
plutôt que par une campagne dédiée (MASTER-008, section 4). TECH, QA, UX, LORE,
PROD, ART, AUDIO, MKT restent des bibliothèques à un seul document chacune :
leur prochaine étape naturelle est la rédaction de leurs premiers documents
numérotés, pas un nouvel audit.
