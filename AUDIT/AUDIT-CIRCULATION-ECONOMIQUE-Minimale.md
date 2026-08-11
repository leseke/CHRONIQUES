# AUDIT — Circulation économique minimale

> Version : 1.1
> Statut : Clos
> Type : Audit de concordance ciblé
> Maturité : 4
> Bibliothèque : AUDIT
> Périmètre : GDB-004A, GDB-005E/F/G/H/I, GDB-019C/D/E/G/H, ACT, ENGINE-014

---

# 1. Objet

Déterminer quel mécanisme économique peut succéder à ENGINE-013 sans inventer une formule de prix, une monnaie ou une mécanique commerciale absente des autorités GDB.

---

# 2. Constat initial

Les autorités existantes définissaient déjà :

- les habitants comme capables d'échanger [réf: GDB-004A] ;
- l'échange comme transfert volontaire de valeur [réf: GDB-005F] ;
- les dons comme forme d'échange [réf: GDB-005F] ;
- les marchés comme sensibles à l'offre/demande et à une information locale [réf: GDB-005G] ;
- la monnaie comme outil de confiance et de circulation [réf: GDB-005H] ;
- la Valeur économique comme contextuelle et non réductible à un nombre absolu [réf: GDB-005I] ;
- les prix comme dynamiques et influencés par de nombreux facteurs [réf: GDB-019G].

Mais aucun document ne fournissait encore :

- une formule déterministe de prix ;
- un mécanisme d'émission/circulation monétaire exécutable ;
- un taux de troc ;
- une règle de négociation ;
- une décision autonome d'achat/vente suffisamment précise.

---

# 3. Conclusion sur les prix et la monnaie

```text
prix / monnaie / vente / marché exécutable
→ NON AUTORISÉS à ce stade
```

Implémenter l'un de ces mécanismes obligerait ENGINE à inventer des coefficients, des fonctions ou des règles de décision métier.

GDB-005G impose en outre localité de l'information, bornes de variation et absence d'arbitrage gratuit ; ces invariants ne suffisent pas à définir une fonction de prix.

GDB-005I interdit de traiter la Valeur économique comme un simple nombre universel.

---

# 4. Sous-capacité autorisable

Une sous-capacité plus petite est cohérente avec les principes : le transfert volontaire d'une denrée entre deux habitants.

Elle nécessite uniquement :

```text
produit existant
+
donneur
+
destinataire
+
opportunité volontaire
+
deux stocks distincts compatibles
+
quantité positive
↓
transfert conservatif
```

Cette capacité crée une circulation économique réelle sans prétendre constituer un commerce complet.

---

# 5. Corrections d'autorité réalisées

Pour rendre le contrat exécutable sans invention, les documents suivants ont été précisés :

- `GDB-005E v1.3` : identité stable de produit, conservation lors d'un transfert et invariant `stock source ≠ stock destination` ;
- `GDB-005F v1.2` : opportunité volontaire explicite, transfert minimal entre parties et exigence de deux stocks distincts ;
- `GDB-004A v1.2` : ordre autonome minimal `entretien → échange volontaire → production` ;
- `GDB-019D v1.1` : GDB-005F devient l'autorité sur les invariants d'échange et le transfert minimal reste distinct du commerce complet.

---

# 6. ACT

Les quatre tests d'ACT-008-A concluent :

1. **Paramétrage** : aucun Verbe existant ne déplace un produit intact entre deux stocks distincts.
2. **Composition** : Repos, Manger et Produire une denrée ne reproduisent pas un transfert conservatif sans détourner leurs Effects.
3. **Pattern existant** : PAT-001 à PAT-003 ont des contrats incompatibles.
4. **Nouveau Pattern** : un nouveau Pattern est justifié.

Chaîne ouverte :

```text
Échange
↓
PAT-004 Transfert
↓
VERB-004 Donner une denrée
```

PAT-004 v1.1 et VERB-004 v1.1 restent Proposition / Maturité 2 jusqu'à validation moteur.

---

# 7. ENGINE

ENGINE-014 v1.1 peut démontrer :

```text
production par A
↓
stock alimentaire de A
↓
transfert volontaire A → B
↓
stock alimentaire distinct de B
↓
consommation par B
```

Le lot ne nécessite aucune modification du `PipelineRunner` : le quatrième Verbe est raccordé par les compositeurs et interfaces existants.

La couverture pré-validation comprend 23 nouveaux tests pour un total attendu de 224 tests.

---

# 8. Frontière maintenue

Restent explicitement hors périmètre :

- monnaie ;
- prix ;
- achat ;
- vente ;
- troc réciproque ;
- salaire ;
- taxe ;
- marché ;
- offre/demande calculée ;
- négociation ;
- entreprise.

Ces sujets ne pourront être ouverts qu'après une nouvelle précision GDB donnant un contrat exécutable sans coefficient inventé.

---

# 9. Verdict

```text
Circulation volontaire d'une denrée
→ AUTORISÉE

Économie commerciale avec prix/monnaie
→ TOUJOURS BLOQUÉE
```

L'audit ciblé est clos.

---

# HISTORIQUE

## Version 1.1

- synchronisation avec GDB-005E v1.3 / GDB-005F v1.2 ;
- ajout explicite de l'invariant de stocks source/destination distincts ;
- synchronisation avec PAT-004 v1.1, VERB-004 v1.1 et ENGINE-014 v1.1 ;
- couverture pré-validation enregistrée à 23 nouveaux tests, soit 224 attendus.

## Version 1.0

- audit initial de la frontière entre circulation volontaire et économie commerciale.

---

Fin du document
