# GDB-019D --- Les Échanges Commerciaux

> Version : 1.1
> Statut : Officiel
> Type : Économie & Commerce
> Maturité : 2
> Bibliothèque : GDB

---

# OBJECTIF

Définir la dimension commerciale des échanges dans Chroniques.

Les échanges commerciaux permettent la circulation des biens, des services et des ressources entre les différents acteurs économiques. Ils constituent un moteur de la prospérité, de la spécialisation et du développement des civilisations.

---

# PRINCIPE

Un échange commercial répond à un intérêt mutuel.

Chaque transaction repose sur une valeur reconnue par les parties concernées. Les échanges peuvent être locaux ou internationaux et évoluent selon l'offre, la demande, la confiance et les conditions du monde.

GDB-005F [réf: GDB-005F] fait autorité sur les invariants généraux d'un échange et sur le premier transfert volontaire exécutable. Le présent document décrit la dimension commerciale et les formes de transaction sans redéfinir ces invariants.

---

# LES FORMES D'ÉCHANGE

Les échanges commerciaux peuvent notamment prendre la forme :

- d'achats ;
- de ventes ;
- de trocs ;
- de contrats ;
- d'importations ;
- d'exportations ;
- de prestations de services.

Chaque forme répond à des besoins économiques spécifiques.

La présence d'une forme dans cette typologie n'autorise pas à inventer sa règle d'exécution. Achat, vente, troc bilatéral, prix et négociation nécessitent des contrats GDB suffisamment précis avant implémentation.

---

# FRONTIÈRE AVEC LE TRANSFERT VOLONTAIRE MINIMAL

GDB-005F peut autoriser un premier transfert volontaire de produit sans contrepartie monétaire ni prix.

Ce transfert démontre la circulation réelle d'une valeur entre habitants mais ne constitue pas encore un marché complet ni une vente.

```text
transfert volontaire de produit
≠
prix
≠
vente
≠
marché
```

Le moteur ne doit donc pas déduire un mécanisme commercial complet de l'existence de ce premier transfert.

---

# ÉVOLUTION

Les échanges évoluent grâce :

- aux innovations ;
- aux infrastructures ;
- aux routes commerciales ;
- aux relations diplomatiques ;
- aux générations.

Ils peuvent s'intensifier, ralentir ou être interrompus.

---

# IMPACT

Les échanges commerciaux influencent :

- les marchés ;
- les entreprises ;
- les ressources ;
- les technologies ;
- les histoires émergentes.

---

# RÈGLES DE CONCEPTION

Toute mécanique liée aux échanges commerciaux devra :

1. refléter les intérêts des acteurs économiques ;
2. produire des flux crédibles de biens et de services ;
3. réagir aux événements du monde ;
4. interagir avec les autres systèmes ;
5. renforcer l'immersion ;
6. respecter les invariants d'échange définis par GDB-005F ;
7. ne jamais inventer prix, taux de troc ou négociation en l'absence de règle dédiée.

---

# CRITÈRE DE VALIDATION

Cette mécanique fait-elle des échanges commerciaux un système vivant créant naturellement des interactions économiques plutôt qu'une simple fonction d'achat et de vente ?

Si la réponse est non, elle devra être repensée.

---

# HISTORIQUE

## Version 1.1

- frontière d'autorité ajoutée avec GDB-005F ;
- distinction explicite entre transfert volontaire minimal et commerce complet ;
- interdiction d'inférer automatiquement prix, vente, troc bilatéral ou négociation de la typologie commerciale ;
- en-tête mis en conformité avec MASTER-004.

## Version 1.0

- création du document.

---

Fin du document

Statut : Validé -- Référence officielle.
