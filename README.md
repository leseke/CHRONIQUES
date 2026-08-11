Chroniques

Chaque vie raconte une Chronique.

Présentation

Bienvenue dans le dépôt documentaire officiel de Chroniques.

Ce dépôt constitue la base de connaissances centrale du projet. Il regroupe les documents définissant la vision, les principes, les règles de simulation, les contrats d'Actions, l'architecture du moteur, la documentation technique, la validation, la production et les autres disciplines du projet.

Il est conçu pour être utilisé aussi bien par des développeurs que par des intelligences artificielles participant au développement.

Le code exécutable du moteur vit dans un dépôt séparé :

CHRONIQUES-ENGINE

Philosophie

Chroniques est développé selon une approche Documentation First.

Une règle ou une architecture structurante doit être définie dans sa bibliothèque d'autorité avant d'être implémentée, sauf lorsqu'un document ENGINE est explicitement rédigé rétroactivement pour décrire du code historique déjà existant.

Cette méthode vise à garantir :

une vision cohérente ;

une architecture évolutive ;

une documentation durable ;

une réduction des incohérences ;

une meilleure collaboration entre humains et IA ;

une traçabilité entre règle, architecture, code, tests et documentation technique.

La documentation constitue la source officielle de vérité conceptuelle et architecturale du projet.

Le code constitue la vérité de l'implémentation réellement exécutable.

TECH documente cette implémentation après validation.

Architecture du dépôt

CHRONIQUES/
│
├── MASTER/
├── CORE/
├── GDB/
├── ACT/
├── ENGINE/
├── TECH/
├── QA/
├── UX/
├── LORE/
├── PROD/
├── ART/
├── AUDIO/
├── MKT/
├── ADR/
├── AUDIT/
└── README.md

Chaque bibliothèque ou registre possède une responsabilité précise.

Hiérarchie de travail

Le workflow de référence est :

MASTER
↓
CORE
↓
GDB
↓
ACT
↓
ENGINE
↓
CHRONIQUES-ENGINE
↓
Tests
↓
TECH

Cette chaîne décrit le passage d'une règle à son implémentation documentée.

Toutes les fonctionnalités ne dépendent pas nécessairement de chaque bibliothèque intermédiaire, mais aucune couche aval ne doit contredire une autorité amont applicable.

MASTER

MASTER définit la gouvernance du projet.

Il décrit notamment :

les principes généraux ;

les standards documentaires ;

les niveaux de maturité ;

les méthodes de travail ;

la gestion des dépendances ;

les critères de qualité ;

les règles de cohérence.

MASTER évolue rarement et possède une autorité élevée sur l'organisation du projet.

CORE

CORE définit les primitives conceptuelles fondamentales utilisées par l'ensemble de Chroniques.

Il couvre notamment des notions comme :

Entity ;

Component ;

Value ;

State ;

Relation ;

Event ;

Time ;

Lifecycle.

CORE décrit les concepts fondamentaux indépendamment de leur implémentation concrète dans le moteur.

GDB

La bibliothèque GDB — Game Design Bible définit les règles de simulation et le fonctionnement du monde de Chroniques.

Elle couvre notamment :

le monde ;

les habitants ;

les besoins ;

les relations ;

les compétences ;

l'économie ;

la réputation ;

la transmission ;

les systèmes sociaux ;

les événements émergents.

Les documents GDB décrivent principalement ce que le monde simulé doit faire.

ACT

ACT définit les contrats génériques liés aux Actions.

Il couvre notamment :

Intent
Plan
Action
Outcome
Effects

ACT ne décide pas des règles métier particulières d'une relation, d'une compétence ou d'un héritage.

Il définit le langage commun permettant d'exprimer et de résoudre les Actions.

ENGINE

ENGINE décrit l'architecture attendue du moteur de simulation.

Il traduit les contrats conceptuels de MASTER, CORE, GDB et ACT en responsabilités techniques suffisamment précises pour guider CHRONIQUES-ENGINE.

ENGINE couvre actuellement notamment :

ENGINE-000  Principes d'architecture
ENGINE-001  Journal d'événements du World
ENGINE-002  Kernel
ENGINE-003  Scheduler et boucle de simulation
ENGINE-004  Systems
ENGINE-005  Persistence / Serialization
ENGINE-006  Action Pipeline
ENGINE-007  Resource Manager — réservé, non créé
ENGINE-008  Systems de population
ENGINE-009  Boucle de vie minimale

ENGINE peut contenir des esquisses de types ou de signatures lorsqu'elles sont nécessaires pour exprimer un contrat avec précision.

Ces esquisses restent des spécifications, pas du code à copier automatiquement dans le moteur.

CHRONIQUES-ENGINE

Le dépôt séparé :

CHRONIQUES-ENGINE

contient l'implémentation exécutable du moteur.

Le moteur est actuellement développé en C#/.NET autour d'une simulation déterministe.

À l'état documenté courant, il contient notamment :

Kernel ;

World / Entity ;

Components ;

Lifecycle ;

Scheduler ;

Persistence ;

Action Pipeline ;

Relations ;

Compétences ;

Héritage minimal ;

Effects de population ;

LifeSession / boucle de vie minimale.

Le dernier état validé du lot ENGINE-009 est :

dotnet build
→ succès

dotnet test
→ 134 / 134 tests réussis
→ 0 échec

Le test d'intégration de référence démontre l'assemblage minimal :

Action joueur
↓
évolution temporelle
↓
vieillissement
↓
mort
↓
héritage
↓
continuité avec l'héritier

Cette validation prouve la continuité architecturale minimale de v0.3, sans prétendre à elle seule représenter toute la richesse finale d'une vie jouable.

TECH

TECH documente l'implémentation réellement obtenue et validée.

TECH n'est pas l'autorité sur les règles métier et ne remplace pas ENGINE.

La distinction est :

ENGINE
→ comportement et architecture attendus

CHRONIQUES-ENGINE
→ implémentation réelle

TECH
→ documentation de cette implémentation après validation

La bibliothèque TECH est active.

Ses documents numérotés actuels sont :

TECH-001 — Systems de population

Documente l'implémentation d'ENGINE-008 :

RelationComponent / RelationSystem ;

SkillComponent / SkillSystem ;

HeritageSystem ;

Effects de population ;

PopulationEffectApplicator.

TECH-002 — Boucle de vie minimale

Documente l'implémentation d'ENGINE-009 :

LifeSession / LifeSessionState ;

orchestration du Scheduler ;

détection de la mort via Lifecycle ;

lecture observable de la transmission ;

continuité du contrôle avec l'héritier ;

tests QA et intégration v0.3.

QA

QA regroupe les documents consacrés à la validation du projet.

Cette bibliothèque peut notamment documenter :

stratégies de tests ;

campagnes de validation ;

critères de sortie ;

non-régressions ;

scénarios de contrôle.

Les tests exécutables restent dans le dépôt moteur lorsque leur nature l'exige.

UX

UX documente l'expérience utilisateur et les interactions avec les interfaces de Chroniques.

LORE

LORE documente les éléments de monde et de fiction qui ne relèvent pas directement des règles systémiques de la GDB.

PROD

PROD documente la production et la feuille de route.

Il décrit notamment :

les phases ;

les versions cibles ;

les priorités de développement ;

l'ordre de construction des grands ensembles.

ART

ART regroupe les règles et documents relatifs à la direction artistique et aux assets visuels.

AUDIO

AUDIO regroupe les règles et documents relatifs au son, à la musique et au design audio.

MKT

MKT regroupe la documentation liée au marketing et à la communication du projet lorsque ces sujets deviennent nécessaires.

ADR

ADR constitue le registre des Architecture Decision Records.

Un ADR conserve la trace d'une décision structurante, de son contexte et de sa justification.

ADR complète les bibliothèques d'autorité mais ne les remplace pas.

AUDIT

AUDIT conserve les contrôles de cohérence et les constats documentaires transverses.

Il permet notamment de suivre :

les divergences ;

les dettes documentaires ;

les corrections ;

les vérifications de concordance entre documentation et code.

Principe de responsabilité unique

Chaque information officielle doit posséder une source d'autorité identifiable.

Une règle ne doit pas être redéfinie dans plusieurs bibliothèques.

Lorsqu'un document dépend d'un autre, il doit privilégier la référence et la traçabilité plutôt qu'une duplication normative.

Exemple :

GDB-004C
↓
ENGINE-008
↓
RelationSystem.cs
↓
RelationSystemTests.cs
↓
TECH-001

Autre chaîne désormais validée :

PROD v0.3
↓
ENGINE-009
↓
LifeSession.cs
↓
LifeSessionTests.cs
↓
TECH-002

Chaque niveau possède ici un rôle différent.

Ordre de lecture recommandé

Pour comprendre l'ensemble du projet :

README.md ;

MASTER/ ;

CORE/ ;

GDB/ ;

ACT/ ;

ENGINE/ ;

TECH/ ;

PROD/ selon le besoin ;

CHRONIQUES-ENGINE pour l'implémentation.

Pour travailler sur une fonctionnalité particulière, il est préférable de suivre directement sa chaîne de traçabilité plutôt que de lire tout le dépôt.

Validation

Une fonctionnalité structurante suit idéalement :

Spécification
↓
Implémentation
↓
Build
↓
Tests
↓
Validation
↓
TECH

Une fonctionnalité n'est pas considérée comme implémentée uniquement parce qu'un document la décrit.

Inversement, du code historique peut nécessiter une documentation ENGINE rétroactive lorsque le projet découvre qu'une infrastructure existe sans contrat architectural explicite.

Toute exception doit être documentée.

Évolution du projet

La structure du dépôt est conçue pour rester stable tandis que son contenu gagne progressivement en profondeur.

Toute évolution importante doit préserver :

la cohérence globale ;

la modularité ;

le déterminisme du moteur lorsque applicable ;

la non-redondance ;

la traçabilité ;

la maintenabilité ;

la séparation entre règles, architecture et implémentation.

Objectif

Construire une base documentaire suffisamment claire, structurée et durable pour accompagner le développement de Chroniques sur plusieurs années.

Cette base doit permettre à tout nouveau contributeur — humain ou IA — de comprendre rapidement :

ce qui fait autorité ;

où se trouve une règle ;

comment elle est traduite dans le moteur ;

comment son implémentation est validée ;

quelles parties restent encore à construire.

Version : 1.2
Statut : Officiel
Bibliothèque racine : CHRONIQUES
