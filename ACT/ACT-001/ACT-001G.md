# ACT-001-G — Périmètre de la bibliothèque ACT

> Version : 1.0
>
> Statut : Fondation
>
> Type : Contrat d'architecture
>
> Bibliothèque : ACT
>
> Dépendances :
> - MASTER
> - GDB
>
> Utilisé par :
> - TECH
> - QA
> - UX
> - Documentation

---

# 1. Objectif

Définir précisément le périmètre fonctionnel de la bibliothèque ACT.

Ce document établit les responsabilités exclusives d'ACT et les limites avec les autres bibliothèques.

Il constitue le contrat architectural garantissant une séparation claire des responsabilités.

---

# 2. Mission

ACT répond exclusivement à la question :

> **Que peut entreprendre un acteur ?**

Toutes les réponses à cette question appartiennent à ACT.

---

# 3. Responsabilités d'ACT

ACT est responsable de :

- la définition des actions ;
- la définition des verbes ;
- les patterns d'action ;
- les conditions d'exécution ;
- les effets produits ;
- les conséquences ;
- les événements générés ;
- les interactions entre actions ;
- les règles de composition ;
- le cycle de vie des actions ;
- les contrats liés au gameplay.

---

# 4. Ce qui appartient à GDB

Les éléments suivants ne relèvent jamais d'ACT :

- les êtres vivants ;
- les objets ;
- les bâtiments ;
- les véhicules ;
- les métiers ;
- les ressources ;
- les institutions ;
- les organisations ;
- les territoires ;
- les lois ;
- les technologies ;
- les données du monde.

ACT utilise ces éléments sans les définir.

---

# 5. Ce qui appartient à TECH

Les éléments suivants relèvent exclusivement de TECH :

- les algorithmes ;
- les structures de données ;
- les API ;
- les bases de données ;
- les moteurs physiques ;
- les systèmes réseau ;
- les sauvegardes ;
- les performances ;
- le code source ;
- les implémentations.

ACT décrit les règles, TECH les implémente.

---

# 6. Ce qui appartient à LORE

LORE documente :

- les événements historiques ;
- les personnages historiques ;
- les chronologies ;
- les récits ;
- les traditions ;
- les légendes.

ACT décrit les possibilités, LORE décrit ce qui s'est réellement produit.

---

# 7. Ce qui appartient à QA

QA définit :

- les scénarios de test ;
- les plans de validation ;
- les cas limites ;
- les campagnes de vérification.

ACT fournit les règles à tester.

---

# 8. Ce qui appartient à UX

UX définit :

- la représentation des actions ;
- les interactions utilisateur ;
- les retours visuels ;
- les flux d'interface.

ACT reste indépendant de toute interface.

---

# 9. Dépendances autorisées

Les dépendances sont unidirectionnelles.

```
MASTER
    │
    ▼
GDB
    │
    ▼
ACT
    │
    ▼
TECH
```

Une bibliothèque ne peut jamais dépendre d'une couche inférieure.

---

# 10. Dépendances interdites

Exemples interdits :

- GDB dépend d'ACT
- GDB dépend de TECH
- MASTER dépend de TECH
- ACT dépend du code
- ACT dépend de l'interface

Ces dépendances créeraient des cycles architecturaux.

---

# 11. Règles de conception

Avant de créer un document, la question suivante doit être posée :

> « Quelle responsabilité ce document couvre-t-il ? »

Si la réponse est :

« Ce qui existe »

→ GDB

« Ce que l'on peut faire »

→ ACT

« Comment cela est implémenté »

→ TECH

---

# 12. Critères de validation

Le périmètre est respecté si :

✓ aucune responsabilité n'est dupliquée ;

✓ aucune bibliothèque ne décrit le même concept ;

✓ chaque document possède une responsabilité unique ;

✓ les dépendances restent acycliques.

---

# 13. Contrat TECH

Les développeurs doivent considérer ACT comme la référence officielle du gameplay.

Toute implémentation qui introduit une mécanique absente d'ACT constitue un écart d'architecture.

---

# 14. Contrat Documentation

Toute nouvelle documentation doit être classée dans la bibliothèque correspondant à sa responsabilité.

En cas de doute, le document doit être revu avant intégration.

---

# 15. Historique

Version 1.0

Création du contrat officiel de périmètre de la bibliothèque ACT.
