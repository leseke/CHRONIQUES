# AUDIT — Concordance GDB-004D/E/F et autonomie enrichie

> Version : 1.0
> Statut : Clos
> Type : Audit de concordance ciblé
> Maturité : 4
> Bibliothèque : AUDIT
> Périmètre : GDB-004A/B/C/D/E/F/H, ACT-002-H, ENGINE autonomie existante

---

# 1. Objet

Vérifier les révisions de GDB-004D, GDB-004E et GDB-004F et les rendre concordantes avec l'arbitrage autonome déjà validé jusqu'à ENGINE-014, sans modifier le moteur.

---

# 2. Constat initial

Les modèles proposés pour Personnalité, Habitudes et Ambitions étaient globalement cohérents et Maturité 2, mais cinq écarts empêchaient une consommation ENGINE sans interprétation :

1. GDB-004A s'arrêtait à `entretien → échange → production → aucun Intent`, tandis que GDB-004E/F ajoutaient Habitudes et Ambitions après la production ;
2. la Force d'une Habitude pouvait être lue comme une priorité face aux autres familles alors que l'architecture actuelle utilise un ordre de sources ;
3. GDB-004B disait encore que l'arbitrage Habitudes/Ambitions restait à spécifier ;
4. « contexte similaire » pour former une Habitude n'était pas une règle déterministe ;
5. le Progrès d'une Ambition et certaines références aux Opportunités ne donnaient pas de frontière PNJ suffisamment stricte.

Une ambiguïté supplémentaire existait dans GDB-004D : la personnalité était décrite comme influence amont, mais pouvait aussi être lue comme modifiant la sensibilité d'un Déclencheur déjà formé.

---

# 3. Décision d'arbitrage

L'ordre de familles courant est désormais porté uniquement par GDB-004A :

```text
besoins physiologiques actionnables
↓
transfert volontaire exécutable
↓
activité productive exécutable
↓
Habitudes actives
↓
Ambitions candidates
↓
aucun Intent
```

La première famille qui produit un Intent exécutable gagne pour ce passage de décision.

Aucun score universel inter-familles n'est introduit.

---

# 4. Priorités internes

Les valeurs existantes restent locales à leur famille :

```text
Besoins
→ satisfaction / urgence

Habitudes
→ Force puis ancienneté

Ambitions
→ Intensité puis Progrès puis ancienneté
```

Force et Intensité ne peuvent pas dépasser une famille située plus haut dans GDB-004A.

Aucune fairness, quota, round-robin ou vieillissement de priorité inter-familles n'est implicite.

---

# 5. GDB-004D — Personnalité

Correction validée :

- modèle `Nom + Valeur 0..100 + Poids de référence` conservé ;
- Inflexions légère/profonde conservées ;
- personnalité confirmée comme influence amont ;
- modulation des Habitudes limitée au seuil de formation via mapping concret ;
- modulation des Ambitions limitée à l'Intensité via mapping concret ;
- aucune modification implicite du Déclencheur ou de la Force d'une Habitude existante ;
- aucun coefficient direct sur l'urgence des besoins ;
- aucune source directe d'Intent.

---

# 6. GDB-004E — Habitudes

Correction validée :

- modèle générique conservé ;
- ajout d'une **Signature de formation déterministe** ;
- suppression de toute similarité contextuelle implicite ;
- chaque type concret fournit Déclencheur et Signature ;
- Force limitée à l'arbitrage entre Habitudes ;
- objectif d'Intent requis comme actuellement traitable ;
- activation distincte de la réussite utilisée pour le renforcement.

Conséquence : le framework générique d'Habitudes peut être spécifié en ENGINE, mais aucun comportement concret ne doit être inventé sans définition concrète de Déclencheur/Signature/objectif.

---

# 7. GDB-004F — Ambitions

Correction validée :

- ajout d'un **Type d'Ambition** explicite ;
- chaque Type fournit sa règle de création, son évaluateur d'objectif et sa fonction de Progrès `0..100` ;
- aucune formule universelle de distance vers un objectif n'est autorisée ;
- Intensité limitée à l'arbitrage interne entre Ambitions ;
- GDB-002E reste réservé aux Opportunités joueur ;
- aucune Opportunité PNJ n'est inventée implicitement ;
- objectif d'Intent requis comme actuellement traitable.

Conséquence : le framework générique d'Ambitions peut être spécifié, mais aucun Type concret d'Ambition n'est autorisé par un simple exemple documentaire.

---

# 8. GDB-004B — Besoins

GDB-004B est synchronisé :

- Habitudes et Ambitions ne sont plus présentées comme des modificateurs implicites de l'urgence des besoins ;
- leur arbitrage inter-familles est délégué à GDB-004A ;
- GDB-002E n'est pas réutilisé pour les PNJ.

---

# 9. Concordance avec ACT et ENGINE

ACT-002-H reste respecté : Habitudes et Ambitions produisent des Intents, jamais directement des Actions.

L'architecture actuelle `CompositeAutonomousIntentSource` est compatible avec l'ordre de familles retenu : la première source non-null gagne.

Aucun changement du moteur existant n'est nécessaire pour conserver la validité d'ENGINE-014.

La validation locale **224 / 224** reste la référence technique courante ; cet audit n'ajoute ni ne modifie de test.

---

# 10. Frontière avant prochain ENGINE

Le modèle documentaire générique est désormais suffisamment précis pour ouvrir un audit ENGINE sur les Habitudes.

Cependant :

```text
modèle générique Habitude
≠
Habitude concrète déjà autorisée
```

et :

```text
modèle générique Ambition
≠
Type concret d'Ambition déjà autorisé
```

Le prochain ENGINE ne devra donc pas inventer un « horaire », un « loisir », une « ambition de carrière » ou toute autre règle concrète absente de GDB.

---

# 11. Verdict

```text
GDB-004A/B/D/E/F
→ CONCORDANTS

modèles génériques Personnalité/Habitudes/Ambitions
→ EXPLOITABLES POUR SPÉCIFICATION ENGINE

comportements concrets supplémentaires
→ TOUJOURS SOUMIS À UNE RÈGLE GDB/ACT EXPLICITE

ENGINE-014 / 224 tests
→ NON AFFECTÉS
```

Audit clos.

---

Fin du document
