# AUDIT — Production autonome minimale

> Version : 1.0
> Statut : Clos
> Type : Audit de concordance ciblé
> Maturité : 4
> Bibliothèque : AUDIT
> Périmètre : GDB-004A, GDB-005, GDB-012, GDB-019, ACT, ENGINE-013

---

# 1. Objet

Déterminer si Chroniques possède suffisamment d'autorité documentaire pour ouvrir un premier comportement autonome de travail et une première transformation économique réelle sans intervention du joueur.

---

# 2. Constat initial

Les autorités existantes affirmaient déjà que :

- les habitants travaillent de manière autonome [réf: GDB-004A] ;
- les métiers créent de la valeur [réf: GDB-005A] ;
- les activités peuvent produire [réf: GDB-012B] ;
- une production mobilise des ressources et d'autres facteurs [réf: GDB-012E] ;
- les chaînes de production ne doivent pas créer des produits depuis rien [réf: GDB-005C] ;
- l'économie doit être vivante [réf: GDB-019A].

Mais ces principes ne suffisaient pas encore à une implémentation déterministe.

Il manquait notamment :

- une définition exécutable de l'activité productive disponible ;
- une opération de production avec quantités d'entrée et de sortie ;
- la règle de consommation des entrées ;
- une provenance obligatoire ;
- un arbitrage minimal entre entretien physiologique et activité productive.

Conclusion initiale :

```text
ENGINE productif autonome
→ interdit sans précision GDB
```

---

# 3. Corrections d'autorité

Le lot a corrigé uniquement les documents responsables :

```text
GDB-004A v1.1
→ activité productive courante
→ entretien actionnable avant travail

GDB-005C v1.2
→ opération de production
→ quantités entrée/sortie
→ consommation réelle
→ provenance

GDB-012B v1.1
→ activité productive exécutable
→ distinction activité / métier

GDB-012E v1.1
→ production exécutable
→ exigences propres à l'opération
→ frontière production / commerce
```

Aucun système de métier, carrière, salaire ou marché n'a été inventé.

---

# 4. Résultat ACT

Application des quatre tests d'ACT-008-A :

1. Paramétrage de Repos/Alimentation : impossible.
2. Composition de Verbes existants : insuffisante.
3. Pattern existant : aucun contrat entrée → sortie + provenance.
4. Nouveau Pattern : justifié.

Résultat :

```text
Transformation
↓
PAT-003 — Production
↓
VERB-003 — Produire une denrée
```

PAT-003 et VERB-003 restent Proposition / Maturité 2 tant que la validation moteur n'est pas confirmée.

---

# 5. Autorisation ENGINE

Après correction GDB/ACT :

```text
ENGINE-013 — Production autonome minimale
→ autorisé
```

Le périmètre autorisé est strict :

- une entrée matérielle ;
- une sortie alimentaire ;
- opération configurable ;
- stock réel ;
- provenance ;
- arbitrage entretien → production ;
- aucune économie commerciale.

---

# 6. Frontière GDB-019

GDB-019 définit correctement les principes de :

- économie ;
- ressources économiques ;
- offre et demande ;
- prix ;
- commerces ;
- entreprises.

Mais les documents actuels ne définissent pas encore de règles suffisamment précises pour calculer déterministement :

- un prix ;
- une offre agrégée ;
- une demande agrégée ;
- une transaction ;
- un salaire ;
- une décision de vente ou d'achat autonome.

Conclusion :

```text
production autonome minimale
→ autorisée

économie commerciale autonome
→ encore interdite avant précision GDB dédiée
```

---

# 7. État technique préparé

ENGINE-013 est spécifié et implémenté en attente de validation locale.

Couverture ajoutée :

```text
22 nouveaux tests
```

Base précédente :

```text
178 / 178
```

Total attendu :

```text
200 tests
```

Aucune validation M4 n'est enregistrée avant confirmation du build et de la suite complète.

---

# 8. Critère de clôture

L'audit est clos car :

- la lacune de spécification du premier socle productif a été identifiée ;
- les autorités compétentes ont été corrigées ;
- ACT possède une chaîne canonique proposée ;
- ENGINE-013 possède un périmètre autorisé clair ;
- la frontière avec le commerce est explicitement maintenue.

Le prochain audit économique devra repartir de GDB-019 uniquement lorsqu'un besoin concret de prix, marché ou transaction apparaîtra.

---

Fin du document
