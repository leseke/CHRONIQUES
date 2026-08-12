# GDB-004

> Version : 1.2
> Statut : Officiel
> Type : Série
> Maturité : 1
> Bibliothèque : GDB

---

> Les habitants qui donnent vie au monde de Chroniques.

---

# Présentation

La série **GDB-004** définit les principes qui régissent les habitants : besoins, relations, personnalité, Habitudes, Ambitions, connaissances, compétences, réputation et transmission.

Elle constitue la référence officielle concernant la population du monde.

---

# Documents

| Document | Sujet | État courant |
|---|---|---|
| GDB-004A | Les Habitants du Monde | v1.3 / M2 |
| GDB-004B | Les Besoins des Habitants | v1.3 / M2 |
| GDB-004C | Les Relations Sociales | v1.1 / M2 |
| GDB-004D | Les Personnalités | v1.3 / M2 |
| GDB-004E | Les Habitudes | v1.2 / M2 |
| GDB-004F | Les Ambitions | v1.2 / M2 |
| GDB-004G | Les Connaissances | Officiel |
| GDB-004H | Les Compétences | v1.2 / M2 |
| GDB-004I | La Réputation | Officiel |
| GDB-004J | La Transmission | Officiel |

---

# Arbitrage autonome courant

GDB-004A fait autorité sur l'ordre des familles :

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

Les priorités internes restent locales à chaque famille :

- besoins : satisfaction/urgence selon GDB-004B ;
- Habitudes : Force puis ancienneté selon GDB-004E ;
- Ambitions : Intensité, Progrès puis ancienneté selon GDB-004F.

Aucun score universel inter-familles n'est défini.

---

# Personnalité, Habitudes et Ambitions

## Personnalité

GDB-004D définit des Traits `Nom + Valeur + Poids de référence` et leur cycle d'Inflexion. La personnalité agit en amont, via des mappings concrets vers la formation des Habitudes ou l'Intensité des Ambitions. Elle n'est pas une source directe d'Intent.

## Habitudes

GDB-004E définit un modèle générique incluant Déclencheur déterministe, Signature de formation, Force et Ticks de suivi. Un type concret d'Habitude doit fournir ses règles contextuelles ; le moteur générique ne devine jamais une similarité de contexte.

## Ambitions

GDB-004F définit un modèle générique incluant Type, Objectif, Intensité, Progrès, Intent et Tick de création. Chaque Type concret doit fournir son évaluateur déterministe d'objectif/progrès et ses conditions de création.

---

# Frontières

- GDB-002E reste consacré aux Opportunités joueur et n'est pas recyclé implicitement pour les PNJ.
- Les exemples d'Habitudes ou d'Ambitions ne deviennent jamais des règles concrètes par leur seule présence dans la documentation.
- Les constantes numériques restent des paramètres d'équilibrage lorsque la forme du modèle est déjà fixée.
- Les systèmes techniques restent du ressort d'ENGINE après validation des contrats GDB applicables.

---

# Principes

Les habitants doivent être :

- autonomes ;
- cohérents ;
- persistants ;
- évolutifs ;
- crédibles ;
- déterministes à état et configuration identiques.

---

# HISTORIQUE

## Version 1.2

- synchronisation de GDB-004A/B/D/E/F après leur montée en précision ;
- ordre des familles autonomes fixé dans GDB-004A ;
- Personnalité séparée de l'arbitrage direct ;
- Signature de formation déterministe ajoutée aux Habitudes ;
- Type et évaluateur déterministe ajoutés aux Ambitions ;
- frontière GDB-002E / Opportunités PNJ clarifiée.

## Version 1.1

- en-tête mis en conformité avec MASTER-004 ;
- enrichissements précédents de GDB-004D/G/H/J.

## Version 1.0

- création du document.

---

Fin du document
