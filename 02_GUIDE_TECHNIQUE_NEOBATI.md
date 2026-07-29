# 02_GUIDE_TECHNIQUE_NEOBATI

## Projet professionnel – NeoBati

**Version :** 1.0

---

# 1. Présentation du document

## 1.1 Objectif

Ce document constitue le guide technique de référence du projet **NeoBati**.

Contrairement aux documents de contexte, qui décrivent l'architecture fonctionnelle de la base Airtable et des interfaces, ce guide définit les conventions techniques, les bonnes pratiques et les règles de développement à respecter pour faire évoluer le projet de manière cohérente.

Il a pour objectif de garantir une architecture homogène, maintenable et évolutive, quel que soit le développeur ou l'outil utilisé.

Les recommandations présentées dans ce document concernent principalement :

- la conception et l'évolution de la base Airtable ;
- le développement des scénarios Make ;
- l'utilisation de l'intelligence artificielle ;
- les conventions de nommage ;
- les règles de modélisation ;
- les bonnes pratiques de maintenance et d'évolution.

Ce guide a vocation à servir de référence technique tout au long du cycle de vie du projet.

---

## 1.2 Positionnement dans la documentation

La documentation de NeoBati est organisée en plusieurs documents complémentaires.

Chaque document possède un rôle bien défini.

| Document | Objectif |
|-----------|----------|
| **00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md** | Présenter l'architecture fonctionnelle de la base Airtable, les tables, les relations et les principales règles métier. |
| **01_CONTEXTE_INTERFACES_NEOBATI.md** | Décrire les interfaces Airtable, les formulaires et les parcours utilisateurs. |
| **02_GUIDE_TECHNIQUE_NEOBATI.md** | Définir les conventions techniques, les bonnes pratiques de développement et les règles d'évolution du projet. |

Ensemble, ces documents constituent la documentation de référence du projet NeoBati.

## 1.3 Ordre de lecture recommandé

Pour comprendre le projet NeoBati, les documents doivent être consultés dans l'ordre suivant :

1. README_NEOBATI.md
   Vue d'ensemble du projet.

2. 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md
   Architecture fonctionnelle des données.

3. 01_CONTEXTE_INTERFACES_NEOBATI.md
   Interfaces, formulaires et parcours utilisateurs.

4. 02_GUIDE_TECHNIQUE_NEOBATI.md
   Conventions techniques, architecture et bonnes pratiques.

---

# 2. Principes d'architecture technique

## 2.1 Philosophie générale

Le projet NeoBati repose sur une architecture modulaire dans laquelle chaque composant possède une responsabilité clairement définie.

La conception privilégie une séparation nette entre :

- le stockage des données ;
- la logique métier ;
- les interfaces utilisateurs ;
- les automatisations ;
- les traitements réalisés par l'intelligence artificielle.

Cette approche permet de limiter les dépendances entre les différents composants du système et facilite les évolutions futures.

Chaque fonctionnalité doit être implémentée dans l'outil le plus adapté à son rôle.

---

## 2.2 Architecture du système

L'architecture technique de NeoBati s'appuie principalement sur trois composants.

### Airtable

Airtable constitue le référentiel central du système d'information.

Il est responsable de :

- stocker les données métier ;
- gérer les relations entre les entités ;
- effectuer les calculs simples (formules, rollups, lookups) ;
- fournir les interfaces utilisées par les collaborateurs.

Airtable ne doit pas être utilisé pour implémenter des traitements métier complexes ou des intégrations avec des services externes.

---

### Make

Make est utilisé comme moteur d'automatisation.

Il est responsable de :

- orchestrer les processus métier ;
- synchroniser les données entre plusieurs services ;
- envoyer des notifications ;
- créer des documents ou dossiers ;
- appeler des services externes ;
- exécuter les traitements nécessitant plusieurs étapes.

La logique métier complexe doit être centralisée dans les scénarios Make plutôt que répartie entre plusieurs automatisations Airtable.

---

### Intelligence artificielle

Les modèles d'intelligence artificielle sont utilisés uniquement lorsque leur valeur ajoutée est réelle.

Ils peuvent notamment intervenir pour :

- analyser un texte ;
- générer un résumé ;
- classer automatiquement une information ;
- produire un contenu structuré ;
- assister les utilisateurs dans certaines tâches.

L'intelligence artificielle ne doit jamais être utilisée pour réaliser des traitements déterministes pouvant être effectués par Airtable ou Make.

---

## 2.3 Séparation des responsabilités

Afin de garantir une architecture cohérente, chaque technologie possède un périmètre d'utilisation clairement défini.

| Composant | Responsabilités principales |
|------------|-----------------------------|
| **Airtable** | Stockage des données, relations, calculs simples, interfaces utilisateurs et formulaires. |
| **Make** | Automatisations, orchestration des processus, intégrations externes et notifications. |
| **IA** | Analyse, génération de contenu, classification et aide à la décision. |

Toute nouvelle fonctionnalité devra respecter cette répartition des responsabilités.

Avant de développer une automatisation, il convient toujours de déterminer quel composant est le plus approprié pour implémenter la logique souhaitée.

Cette approche permet de limiter la complexité du système, de faciliter sa maintenance et de garantir une meilleure évolutivité.

## 2.4 Principes directeurs

Les décisions techniques prises dans NeoBati reposent sur les principes suivants :

• simplicité avant complexité ;

• fonctionnalités natives avant automatisations ;

• automatisations avant intelligence artificielle ;

• une donnée = un référentiel ;

• une responsabilité = un composant ;

• documenter toute évolution.

# 3. Bonnes pratiques Airtable

Les recommandations présentées dans ce chapitre définissent les principes de conception à respecter pour toute évolution de la base Airtable NeoBati.

Elles visent à garantir une base de données cohérente, performante et facilement maintenable dans le temps.

---

## 3.1 Modélisation des données

La base Airtable doit être conçue selon les principes de la modélisation relationnelle.

Chaque table représente une entité métier clairement identifiée et possède une responsabilité unique.

Les données doivent être organisées de manière à limiter les duplications, faciliter les relations entre les différentes entités et permettre l'évolution future du système.

Les principales règles de modélisation sont les suivantes :

- Une table représente une seule entité métier.
- Chaque enregistrement représente une seule occurrence de cette entité.
- Une information ne doit être stockée qu'une seule fois lorsque cela est possible.
- Les relations entre les tables doivent être privilégiées aux duplications de données.
- Les champs calculés doivent être utilisés lorsque les valeurs peuvent être déduites automatiquement.

---

## 3.2 Conception des tables

Chaque nouvelle table intégrée au projet doit répondre à un besoin métier clairement identifié.

Avant de créer une nouvelle table, il convient de vérifier que l'information ne peut pas être intégrée à une table existante ou obtenue au moyen d'une relation.

Chaque table doit notamment définir :

- son objectif ;
- son niveau de granularité (1 ligne = 1 entité métier) ;
- ses relations avec les autres tables ;
- les informations réellement stockées ;
- les informations calculées automatiquement.

Cette démarche permet de conserver une architecture simple et cohérente.

---

## 3.3 Relations entre les tables

Les relations constituent le principal mécanisme de navigation entre les données.

Elles doivent être privilégiées chaque fois que plusieurs entités partagent une information commune.

Les principales conventions sont les suivantes :

- privilégier les relations aux duplications de données ;
- utiliser des relations explicites plutôt que des champs texte ;
- conserver un seul référentiel pour chaque type d'information ;
- utiliser une table de liaison lorsqu'une relation plusieurs-à-plusieurs est nécessaire.

Cette approche facilite les recherches, les calculs et les automatisations.

---

## 3.4 Champs calculés

Les champs Formula, Lookup et Rollup doivent être utilisés dès lors qu'une information peut être obtenue automatiquement à partir des données existantes.

Les champs calculés présentent plusieurs avantages :

- suppression des mises à jour manuelles ;
- diminution des risques d'erreur ;
- cohérence des indicateurs ;
- simplification des automatisations.

À l'inverse, un champ calculé ne doit jamais être modifié manuellement ni par une automatisation.

Si une valeur est dérivée d'autres informations présentes dans la base, elle doit être calculée plutôt que saisie.

---

## 3.5 Interfaces

Les interfaces Airtable constituent l'environnement de travail des utilisateurs.

Les utilisateurs ne doivent, dans la mesure du possible, pas accéder directement aux tables de la base.

Les interfaces doivent :

- afficher uniquement les informations utiles au profil concerné ;
- limiter les possibilités de modification aux données nécessaires ;
- simplifier les parcours utilisateurs ;
- réduire les risques d'erreurs de saisie.

Les tableaux de bord doivent privilégier les indicateurs synthétiques avant les données détaillées.

---

## 3.5bis Vues par rôle

En complément des interfaces (section 3.5), qui constituent le point d'accès des utilisateurs finaux, chaque table dispose d'une organisation de vues Airtable natives dédiée aux besoins de conception, de maintenance et de vérification directe des données par le développeur du projet — répondant ainsi à l'exigence du cahier des charges portant sur les « vues adaptées par rôle » et les « vues filtrées » du livrable Étape 1, en complément des interfaces et des formulaires.

**Convention retenue.** Les vues de chaque table sont organisées en dossiers nommés par rôle métier (Direction, Administratif, Chargé d'affaires, Chefs de chantier, Artisans), reprenant la terminologie des interfaces documentées en 01_CONTEXTE_INTERFACES_NEOBATI.md. Un dossier distinct, « Automatisation », regroupe les vues techniques créées pour porter la logique d'éligibilité d'un scénario Make (ex. « Devis à relancer », « AUT-CHA-004 - Chantiers à notifier (retard) », « Factures à relancer »), afin de ne jamais mélanger les vues de pilotage métier et les vues de support technique.

**Distinction avec les interfaces.** Ces vues ne sont pas consultées par les utilisateurs de l'entreprise NeoBati, qui accèdent exclusivement aux données via les interfaces et les formulaires (cf. 01_). Elles servent au créateur/éditeur de la base pour concevoir, vérifier et faire évoluer le système. Les deux niveaux sont complémentaires et non redondants : l'interface répond au besoin utilisateur final, la vue répond au besoin de modélisation et de maintenance du système.

**Exception assumée — table Demande de devis.** Cette table n'est consultée que par un seul rôle (Chargé d'affaires, cf. 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md, section 3.2). L'absence de dossier de vues par rôle est un choix assumé : une organisation par rôle n'a d'intérêt que lorsque plusieurs profils consomment une même table avec des besoins de lecture distincts, ce qui n'est pas le cas ici.

**Point à compléter — table Rapport terrain.** Cette table est consultée par deux rôles aux besoins distincts (Artisan : déposer un compte rendu ; Chef de chantier : consulter et valider, cf. 00_, section 3.6), sans qu'aucune vue par rôle n'existe à ce jour. Cet écart est identifié et non corrigé à ce stade, l'accès aux données de cette table se faisant exclusivement par l'interface pour l'ensemble des utilisateurs concernés.

---

## 3.6 Formulaires

Les formulaires doivent être utilisés chaque fois qu'un utilisateur doit créer un nouvel enregistrement sans accéder directement à la table concernée.

Ils permettent notamment :

- de simplifier la saisie ;
- de limiter les erreurs ;
- de masquer les champs calculés ;
- de contrôler les informations obligatoires.

Chaque formulaire doit être conçu autour d'un objectif métier unique.

---

## 3.7 Performances Airtable

La conception de la base doit également tenir compte des performances.

Les recommandations suivantes sont retenues.

| Bonne pratique | Justification |
|----------------|---------------|
| Limiter les formules inutilement complexes | Réduire les temps de calcul et améliorer la réactivité de la base. |
| Éviter les relations redondantes | Simplifier le modèle de données et limiter les incohérences. |
| Privilégier les calculs natifs d'Airtable | Éviter des automatisations Make inutiles. |
| Limiter les champs calculés lorsque plusieurs calculs peuvent être regroupés | Améliorer la lisibilité et les performances. |
| Utiliser les vues principalement pour l'administration | Les interfaces constituent le point d'entrée des utilisateurs. |
| Supprimer les champs et vues devenus inutiles | Alléger la base et faciliter sa maintenance. |

Ces recommandations contribuent à maintenir une base fluide et facilement évolutive.

---

## 3.8 Pièges techniques identifiés

Cette section recense les comportements Airtable non documentés officiellement par l'éditeur, découverts en pratique lors du développement du projet. Elle a vocation à s'enrichir au fil des évolutions.

**Rollup vide et comparaisons.** Un champ Rollup dont la source de cumul ne contient aucun enregistrement lié ne renvoie pas nécessairement un blanc exploitable par `BLANK()` dans une formule : selon la fonction d'agrégation utilisée (ex. `MAX(values)`), le résultat peut être coercé à une valeur numérique (souvent 0, interprétée comme une date proche de l'epoch dans une comparaison de dates). Toute formule qui doit détecter l'absence de données sous-jacentes à un Rollup doit tester directement le champ de lien source (ex. `ETAPES_Chantier != BLANK()`), jamais le résultat du Rollup lui-même. Ce cas a été découvert sur les champs `EnRetard` et `JoursRetardChantier` de la table Chantier (domaine Gestion commerciale, AUT-COM-004), qui affichaient respectivement "Oui" et NaN pour un chantier sans Étape liée.

### Décisions retenues

Pour NeoBati, les principes suivants sont retenus :

- Les interfaces constituent le point d'entrée principal des utilisateurs.
- Les tables sont considérées comme la couche de stockage des données.
- Les vues sont principalement utilisées pour l'administration et certains traitements internes.
- Les calculs simples sont réalisés directement dans Airtable.
- Les traitements métier complexes sont délégués à Make.

# 4. Bonnes pratiques Make

Les scénarios Make constituent le moteur d'automatisation de NeoBati.

Ils assurent l'orchestration des différents processus métier, la communication avec les services externes et les traitements dépassant les capacités natives d'Airtable.

Chaque scénario doit être conçu afin d'être facilement compréhensible, maintenable et évolutif.

---

## 4.1 Organisation des scénarios

Chaque scénario Make doit répondre à une responsabilité unique.

Il est recommandé de privilégier plusieurs scénarios spécialisés plutôt qu'un scénario unique regroupant l'ensemble des traitements du projet.

Cette approche facilite :

- la maintenance ;
- les évolutions futures ;
- le débogage ;
- la réutilisation des scénarios.

Chaque scénario doit être autonome et limiter autant que possible ses dépendances avec les autres scénarios.

---

## 4.2 Déclencheurs

Chaque scénario doit posséder un déclencheur clairement identifié.

Selon le besoin métier, plusieurs types de déclencheurs peuvent être utilisés :

- Webhook ;
- Airtable (nouvel enregistrement ou modification) ;
- Déclenchement planifié ;
- API externe.

Le choix du déclencheur doit toujours privilégier la simplicité et limiter les exécutions inutiles.

---

## 4.3 Organisation des traitements

Les traitements réalisés dans Make doivent suivre une structure logique et reproductible.

Dans la mesure du possible, chaque scénario doit être organisé selon les étapes suivantes :

1. Déclenchement.
2. Validation des données reçues.
3. Traitement métier.
4. Écriture des données.
5. Notifications éventuelles.
6. Journalisation.

Cette organisation facilite la lecture des scénarios et réduit les risques d'erreurs.

---

## 4.4 Gestion des erreurs

Chaque scénario doit prévoir un mécanisme de gestion des erreurs.

Les principaux objectifs sont :

- empêcher l'interruption complète d'un processus ;
- identifier rapidement l'origine d'une erreur ;
- faciliter la reprise du traitement.

Selon le contexte, plusieurs stratégies peuvent être mises en œuvre :

- arrêt contrôlé du scénario ;
- nouvelle tentative d'exécution ;
- création d'un journal d'erreur ;
- notification d'un administrateur.

Les erreurs ne doivent jamais être ignorées silencieusement.

---

## 4.5 Journalisation

Les scénarios importants doivent conserver une trace des traitements réalisés.

La journalisation peut notamment enregistrer :

- la date d'exécution ;
- le scénario concerné ;
- l'enregistrement traité ;
- le résultat du traitement ;
- les éventuelles erreurs rencontrées.

Cette pratique facilite le diagnostic des incidents et le suivi des automatisations.

---

## 4.6 Maintenance

Les scénarios doivent être conçus afin de pouvoir évoluer facilement.

| Bonne pratique | Objectif |
|----------------|----------|
| Utiliser des noms explicites pour les modules | Faciliter la lecture du scénario. |
| Limiter les embranchements inutiles | Réduire la complexité du scénario. |
| Regrouper les traitements similaires | Favoriser la réutilisation et limiter les duplications. |
| Documenter les scénarios complexes | Faciliter la maintenance future. |
| Supprimer les modules devenus inutiles | Conserver une architecture claire. |

Une architecture simple est généralement plus robuste qu'un scénario unique très complexe.

---

## 4.7 Pièges techniques identifiés

Cette section recense les comportements Make/Airtable non documentés officiellement, découverts en pratique lors du développement du projet. Elle a vocation à s'enrichir au fil des évolutions.

**Recherches sans résultat et modules en aval.** Un module Search Records qui ne trouve aucun enregistrement ne bloque pas automatiquement l'exécution du scénario : il peut laisser passer un bundle vide vers les modules suivants, provoquant l'envoi d'une notification aux variables vierges puis une erreur sur un module d'écriture faute d'identifiant valide. Tout scénario connectant directement un Search Records à des modules de traitement en aval (sans Iterator ni Aggregator intermédiaire) doit systématiquement être suivi d'un filtre de garde (`ID → Exists`) avant ces modules. Cette bonne pratique a été identifiée lors du développement d'AUT-COM-003 (domaine Gestion commerciale).

**Mapping direct d'un champ lié comme input variable de script.** Lorsqu'un champ lié (ex. `CLIENT_Chantier`) est mappé directement comme input variable dans un script d'automatisation Airtable, la valeur reçue par le script est le champ primaire de l'enregistrement lié — pas le Record ID technique, et pas nécessairement le champ que l'on souhaite afficher. Sur ce projet, le champ primaire de la table Client concatène un identifiant et le nom (ex. "5-Atelier Bois & Design"), ce qui a nécessité la création d'un champ Lookup dédié (`Nom_CLIENT_Chantier`) pour obtenir le nom du client isolément. Ce comportement n'est pas un bug : il reflète simplement le champ primaire configuré sur la table liée. Point de vigilance identifié lors du développement d'AUT-CHA-002 (domaine Gestion des chantiers).

**Suppression des guillemets dans l'éditeur de formule Make.** Au-delà du cas déjà connu des guillemets doubles adjacents à une puce de variable, certaines formules Make fonctionnent correctement sans aucun guillemet autour de chaînes littérales simples (espace, ponctuation), alors que l'ajout de guillemets — doubles ou simples — provoque une mauvaise interprétation de la formule. Comportement observé lors du développement de l'enrichissement IA d'AUT-COM-003 sur une formule `replace()` imbriquée. À tester au cas par cas avant de figer une formule contenant des chaînes littérales.

**Formulaire d'interface et table de jonction porteuse d'attributs.** Un formulaire Airtable (qu'il s'agisse d'un formulaire d'interface ou d'un formulaire classique) ne peut créer, via un champ de liaison, que des enregistrements déjà existants dans la table liée : il ne permet jamais de créer plusieurs enregistrements de jonction en une seule soumission lorsque chacun porte un attribut propre saisi par l'utilisateur (ex. une quantité). C'est le cas de `Quantité Matériel`, table de jonction entre `Étape` et `Matériel` porteuse du champ `Quantité`. Le formulaire de création d'une étape ne peut donc pas inclure la saisie du matériel nécessaire à cette étape.

Solution retenue : séquencer la saisie en deux temps. Le formulaire de création d'étape ne gère que les champs propres à l'étape (nom, description, planning, artisan) et redirige, après soumission, vers la fiche de l'étape créée. Sur cette fiche, l'élément de liste liée affichant `Quantité Matériel` (filtré sur l'étape courante) est configuré avec l'option d'interface **Ajouter des entrées par le biais d'un formulaire**, qui ouvre un formulaire de création dédié à la table `Quantité Matériel`. Ce formulaire pré-remplit et verrouille automatiquement le lien vers l'étape parente, expose uniquement les champs de saisie utile (matériel, quantité, notes) et masque les champs Formula/Lookup (`QuantiteMaterielID`, `Unite_MATERIEL`, `CoutUnitaire_MATERIEL`, `CoutMateriel`). Le champ de liaison vers le référentiel `Matériel` conserve son comportement de recherche/sélection standard, sans option de création à la volée, ce qui protège l'intégrité du référentiel.

Ce pattern est généralisable à toute table de jonction porteuse d'attribut dans le projet (aucune autre identifiée à ce jour) : ne jamais tenter de la peupler depuis le formulaire de création de l'enregistrement parent, toujours passer par un élément de liste liée avec formulaire d'ajout sur la fiche de détail. Piège identifié lors du développement de l'interface chef de chantier, section « Nouveaux chantiers (à préparer) ».

### Décisions retenues

Pour NeoBati, les principes suivants sont retenus :

- Un scénario Make répond à une seule responsabilité métier.
- Les traitements sont découpés en scénarios spécialisés plutôt qu'en un scénario monolithique.
- Tous les scénarios critiques doivent intégrer une gestion des erreurs.
- Les traitements doivent suivre une structure commune : déclenchement, validation, traitement, écriture, notification, journalisation.
- Les intégrations avec des services externes (Google Drive, Gmail, LLMs, etc.) sont réalisées exclusivement par Make.
- Les automatisations natives d'Airtable sont réservées aux traitements simples lorsqu'elles permettent d'éviter la création d'un scénario Make.

# 5. Guide de décision technique

Ce chapitre définit la méthode à suivre avant d'ajouter une nouvelle fonctionnalité au projet NeoBati.

L'objectif est de choisir systématiquement la solution la plus simple, la plus robuste et la plus facile à maintenir.

Avant toute évolution du système, il est recommandé de suivre les étapes de décision décrites ci-dessous.

| Si le besoin est... | Utiliser... | Pourquoi ? |
|---------------------|-------------|------------|
| Calcul d'une valeur | Formula | Plus simple et plus performant. |
| Agrégation de données | Rollup | Calcul natif d'Airtable. |
| Consultation d'une donnée liée | Lookup | Évite les duplications. |
| Création d'un enregistrement | Formulaire Airtable | Simplifie la saisie. |
| Mise à jour simple d'un enregistrement | Automatisation Airtable | Suffisant pour les traitements simples. |
| Orchestration de plusieurs actions | Make | Gère les processus complexes. |
| Interaction avec un service externe | Make | Centralise les échanges. |
| Analyse ou génération de texte | LLM | Traitement non déterministe. |

---

## 5.1 Faut-il créer une automatisation ?

Toutes les nouvelles fonctionnalités ne nécessitent pas une automatisation.

Avant de développer un scénario Make ou une automatisation Airtable, il convient de vérifier si le besoin peut être satisfait directement par la structure de la base.

Le principe retenu est le suivant :

```
Le besoin peut-il être résolu
avec un champ Formula,
Lookup ou Rollup ?

            │
      ┌─────┴─────┐
      │           │
     Oui         Non
      │           │
      ▼           ▼
 Utiliser     Étudier une
 Airtable    automatisation
```

Une automatisation ne doit être développée que lorsqu'une solution native Airtable ne permet pas de répondre au besoin.

---

## 5.2 Airtable ou Make ?

Lorsqu'une automatisation est nécessaire, il convient ensuite de déterminer quel outil est le plus adapté.

Les règles suivantes doivent être privilégiées.

| Besoin | Solution recommandée |
|---------|----------------------|
| Calcul simple | Airtable |
| Formula | Airtable |
| Lookup | Airtable |
| Rollup | Airtable |
| Mise à jour d'un enregistrement | Airtable ou Make selon le contexte |
| Notification interne simple | Airtable |
| Notification externe (email, Slack, etc.) | Make |
| Génération de document | Make |
| Connexion à un service externe | Make |
| Orchestration de plusieurs actions | Make |

Le principe général est le suivant :

- Airtable gère les données.
- Make gère les processus.

---

## 5.3 Make ou Intelligence Artificielle ?

L'utilisation d'un modèle d'intelligence artificielle doit toujours être justifiée par un besoin réel.

Avant d'utiliser un LLM, il convient de se poser la question suivante.

```
Le traitement est-il
déterministe ?

            │
      ┌─────┴─────┐
      │           │
     Oui         Non
      │           │
      ▼           ▼
Make        Intelligence
               artificielle
```

Un traitement est considéré comme déterministe lorsque le résultat attendu est toujours identique pour une même entrée.

Exemples :

**Traitements déterministes**

- calcul d'un montant ;
- mise à jour d'un statut ;
- création d'un dossier ;
- renommage d'un fichier ;
- envoi d'un email standard.

Ces traitements doivent être réalisés sans IA.

**Traitements non déterministes**

- résumé d'un rapport ;
- classification d'un texte ;
- génération d'un email personnalisé ;
- extraction d'informations depuis un texte libre ;
- analyse d'une demande client.

Ces traitements peuvent être confiés à un modèle d'intelligence artificielle.

---

## 5.4 Quand créer une nouvelle table ?

Avant d'ajouter une nouvelle table à la base, plusieurs questions doivent être étudiées.

```
La nouvelle information
représente-t-elle
une entité métier ?

            │
      ┌─────┴─────┐
      │           │
     Oui         Non
      │           │
      ▼           ▼
Créer      Ajouter un champ
une table   dans une table
```

Une nouvelle table est justifiée lorsqu'elle représente une entité indépendante possédant :

- son propre cycle de vie ;
- ses propres relations ;
- ses propres informations.

À l'inverse, une simple caractéristique d'une entité existante doit rester un champ.

---

## 5.5 Quand créer une relation ?

Une relation doit être créée dès lors qu'une même information est utilisée dans plusieurs tables.

Les relations doivent être privilégiées aux duplications de données.

Lorsque plusieurs occurrences peuvent être associées de part et d'autre de la relation, une table de liaison doit être créée.

---

## 5.6 Quand créer un formulaire ?

Les formulaires sont privilégiés lorsque l'utilisateur doit uniquement créer un nouvel enregistrement.

Ils permettent :

- de simplifier la saisie ;
- de masquer les champs techniques ;
- de limiter les erreurs ;
- de sécuriser les créations.

Les utilisateurs ne doivent pas accéder directement aux tables lorsque cette consultation n'est pas nécessaire.

---

## 5.7 Quand créer une interface ?

Une interface est créée lorsqu'un utilisateur doit :

- consulter plusieurs informations provenant de différentes tables ;
- suivre des indicateurs ;
- réaliser plusieurs actions sur un même processus métier ;
- travailler quotidiennement dans Airtable.

Les interfaces constituent le point d'entrée principal des utilisateurs.

Les tables restent réservées à l'administration et à la maintenance de la base.

### Décisions retenues

Pour NeoBati, les principes suivants sont retenus :

- Toujours privilégier la solution la plus simple répondant au besoin.
- Utiliser Airtable avant Make lorsqu'une fonctionnalité native est suffisante.
- Utiliser Make uniquement lorsqu'une orchestration ou une intégration externe est nécessaire.
- Utiliser un modèle d'intelligence artificielle uniquement lorsqu'un traitement non déterministe apporte une réelle valeur ajoutée.
- Éviter la multiplication des automatisations lorsque plusieurs besoins peuvent être couverts par une même logique métier.
- Concevoir chaque évolution de manière à préserver la simplicité, la maintenabilité et l'évolutivité du système.

# 6. Conventions de nommage

Les conventions de nommage définissent les règles à respecter pour nommer les différents éléments du projet NeoBati.

Leur objectif est de garantir une architecture homogène, de faciliter la maintenance du projet et d'améliorer la compréhension des données par les développeurs comme par les outils d'automatisation.

Les conventions présentées dans ce chapitre devront être respectées pour toute évolution future du projet.

---

## 6.1 Tables Airtable

Les noms des tables doivent représenter directement l'entité métier concernée.

Les règles suivantes sont retenues :

- utiliser un nom au singulier ;
- utiliser un vocabulaire métier explicite ;
- éviter les abréviations ;
- éviter les préfixes techniques.

### Exemples

| Correct | À éviter |
|----------|-----------|
| Client | tbl_Client |
| Chantier | Chantiers |
| Facture | FACT |
| Rapport terrain | RapportTerrain |

---

## 6.2 Champs

Les champs doivent être nommés de manière explicite afin d'être compréhensibles sans documentation complémentaire.

Les principales règles sont :

- utiliser des noms courts mais explicites ;
- éviter les abréviations ;
- utiliser une majuscule au début de chaque mot ;
- conserver une terminologie homogène dans toute la base.

### Exemples

| Correct | À éviter |
|----------|-----------|
| Date de début | DateDeb |
| Montant HT | MHT |
| Coût total | CoutTot |
| Pourcentage d'avancement | Avancement |

---

## 6.3 Champs de relation

Les champs de relation suivent une convention spécifique.

Le nom du champ est composé du nom de la table liée suivi du nom de la table d'origine.

Exemple :

```
CLIENT_Devis
```

Ce nom indique que le champ établit une relation avec la table **Client** depuis la table **Devis**.

Cette convention est utilisée dans l'ensemble de la base NeoBati afin de faciliter l'identification des relations.

---

## 6.4 Champs calculés

Les champs calculés doivent permettre d'identifier rapidement leur rôle.

Lorsque cela est pertinent, un suffixe explicite peut être utilisé.

Exemples :

- DateEcheance_fx
- PaiementRecu
- PourcentageFacturation
- MargeBrute

Les noms doivent rester orientés métier plutôt que technique.

---

## 6.5 Interfaces

Les interfaces doivent être nommées selon le profil utilisateur auquel elles sont destinées.

Structure recommandée :

```
Profil — Fonction
```

Exemples :

- Direction — Pilotage global
- Administratif — Facturation & documents
- Chargé d'affaires — Devis & suivi commercial
- Chefs de chantier — Planning & avancement
- Artisans — Mobile terrain

---

## 6.6 Pages d'interface

Les pages doivent décrire directement leur fonction.

Exemples :

- Tableau de bord
- Pipeline devis
- Planning des étapes
- Documents chantiers
- Chantiers à facturer

Les intitulés doivent être compréhensibles par les utilisateurs finaux.

---

## 6.7 Formulaires

Les formulaires doivent être nommés à l'aide d'un verbe d'action.

Structure recommandée :

```
Verbe + Objet
```

Exemples :

- Créer un devis
- Créer une facture
- Ajouter un document
- Créer un client
- Créer un rapport terrain

---

## 6.8 Scénarios Make

Les scénarios Make doivent suivre une nomenclature homogène.

Structure recommandée :

```
[Domaine] — [Action principale]
```

Exemples :

- Devis — Créer un chantier
- Chantier — Générer les étapes
- Facture — Envoyer une relance
- Rapport terrain — Notifier le chef de chantier

Cette convention facilite la recherche et la maintenance des scénarios.

---

## 6.9 Variables et données Make

Les variables créées dans Make doivent porter un nom explicite.

Les noms doivent :

- décrire clairement leur contenu ;
- rester cohérents avec les noms utilisés dans Airtable ;
- éviter les abréviations.

Exemples :

- clientId
- chantierId
- factureId
- montantHT
- dateEcheance

---

## 6.10 Documents

Les documents générés automatiquement doivent respecter une convention commune.

Structure recommandée :

```
[Type]_[Référence]_[Date]
```

Exemples :

- Devis_DEV-001_2026-07-15.pdf
- Facture_FAC-012_2026-08-01.pdf
- RapportTerrain_CHA-004_2026-09-10.pdf

Cette convention facilite le classement et les recherches, y compris via la recherche native d'Airtable sur le nom des pièces jointes.

### Décisions retenues

Pour NeoBati, les conventions suivantes sont retenues :

- Les noms privilégient toujours le vocabulaire métier plutôt que le vocabulaire technique.
- Les conventions de nommage sont identiques dans Airtable, Make et les documents générés.
- Les relations entre les tables utilisent systématiquement le format `TABLELIÉE_TableOrigine`.
- Les scénarios Make sont organisés par domaine métier et non par outil ou par service externe.
- Les noms doivent rester suffisamment explicites pour être compris sans consulter la documentation.

# 7. Règles de modélisation

Les règles présentées dans ce chapitre définissent les principes à respecter lors de toute évolution du modèle de données de NeoBati.

Elles ont pour objectif de garantir la cohérence de la base, de limiter les redondances et de faciliter les futures automatisations.

---

## 7.1 Une table représente une entité métier

Chaque table doit représenter une seule entité métier clairement identifiable.

Une table ne doit jamais regrouper plusieurs concepts différents.

### Exemples

| Table | Entité représentée |
|--------|--------------------|
| Client | Un client |
| Devis | Un devis |
| Chantier | Un chantier |
| Étape | Une étape |
| Facture | Une facture |

Si une nouvelle information possède son propre cycle de vie, ses propres relations et ses propres attributs, elle doit généralement être modélisée sous la forme d'une nouvelle table.

---

## 7.2 Granularité des enregistrements

Chaque enregistrement doit représenter une seule occurrence de l'entité.

Quelques exemples :

- une ligne de la table **Client** représente un client ;
- une ligne de la table **Devis** représente un devis ;
- une ligne de la table **Étape** représente une étape ;
- une ligne de la table **Quantité Matériel** représente l'utilisation d'un matériel sur une étape.

Cette règle garantit une structure homogène et facilite les traitements automatiques.

---

## 7.3 Relations entre les entités

Les relations doivent être privilégiées aux duplications de données.

Lorsqu'une information est utilisée dans plusieurs tables, celle-ci doit être stockée une seule fois puis référencée grâce à une relation.

Les relations permettent notamment :

- d'éviter les incohérences ;
- de simplifier les mises à jour ;
- de faciliter les calculs ;
- de garantir l'intégrité des données.

---

## 7.4 Relations plusieurs-à-plusieurs

Les relations de type plusieurs-à-plusieurs doivent être modélisées au moyen d'une table de liaison.

Cette table contient les informations propres à la relation.

Exemple :

```
Matériel
      │
      │
Quantité Matériel
      │
      │
Étape
```

La table **Quantité Matériel** ne représente pas un matériel ni une étape, mais l'utilisation d'un matériel pour une étape donnée.

Cette approche permet d'ajouter des informations spécifiques à cette relation, comme la quantité utilisée ou le coût calculé.

---

## 7.5 Données calculées

Les informations pouvant être déduites automatiquement ne doivent pas être saisies manuellement.

Il convient de privilégier :

- les champs Formula ;
- les champs Lookup ;
- les champs Rollup.

Les automatisations Make ne doivent pas recalculer des valeurs déjà produites par Airtable.

---

## 7.6 Éviter la duplication des données

Une même information ne doit être stockée qu'une seule fois lorsque cela est possible.

Avant d'ajouter un nouveau champ, il convient de vérifier si l'information existe déjà dans une autre table et si elle peut être récupérée au moyen d'une relation.

La duplication volontaire reste possible lorsqu'elle répond à un besoin métier clairement identifié (par exemple la conservation d'un état historique).

---

## 7.7 Responsabilité des données

Chaque donnée possède un propriétaire unique.

Par exemple :

| Information | Table responsable |
|--------------|------------------|
| Coordonnées d'un client | Client |
| Informations d'un devis | Devis |
| Planning d'un chantier | Chantier |
| Coût unitaire d'un matériau | Matériel |
| Quantité utilisée | Quantité Matériel |

Les autres tables doivent récupérer ces informations par relation plutôt que les stocker une seconde fois.

---

## 7.8 Évolutivité

Toute évolution de la base doit préserver la simplicité du modèle de données.

Avant de modifier la structure, il convient de vérifier :

- si une nouvelle table est réellement nécessaire ;
- si une relation permet déjà de répondre au besoin ;
- si un champ calculé suffit ;
- si la modification reste cohérente avec l'architecture existante.

L'objectif est de maintenir un modèle de données stable, compréhensible et évolutif.

### Décisions retenues

Pour NeoBati, les principes suivants sont retenus :

- Une table représente une seule entité métier.
- Une information possède un seul référentiel dans la base.
- Les relations sont privilégiées aux duplications de données.
- Les relations plusieurs-à-plusieurs sont systématiquement modélisées à l'aide d'une table de liaison.
- Les données calculées restent calculées et ne sont jamais mises à jour manuellement.
- Toute évolution du modèle de données doit préserver la simplicité de l'architecture existante.

# 8. Architecture des automatisations

Les automatisations constituent la couche d'orchestration du système d'information NeoBati.

Leur rôle est de relier les différents composants de l'application, d'automatiser les processus métier et d'assurer la communication entre Airtable et les services externes.

L'objectif est de construire une architecture modulaire dans laquelle chaque automatisation possède une responsabilité clairement définie.

---

## 8.1 Principes généraux

Les automatisations doivent respecter les principes suivants :

- une automatisation répond à un seul processus métier ;
- chaque scénario possède une responsabilité clairement définie ;
- les traitements sont découplés autant que possible ;
- les données restent stockées dans Airtable ;
- Make orchestre les traitements sans devenir le référentiel des données.

Les scénarios doivent privilégier la simplicité plutôt que la centralisation excessive de la logique métier.

---

## 8.2 Découpage par domaine métier

Les scénarios Make doivent être organisés selon les principaux processus métier de NeoBati.

Les domaines identifiés sont les suivants.

### Commercial

Ce domaine regroupe les automatisations liées :

- aux demandes de devis ;
- aux devis ;
- aux relances commerciales ;
- aux notifications du chargé d'affaires.

---

### Chantiers

Ce domaine concerne notamment :

- la création d'un chantier ;
- la planification ;
- les notifications aux chefs de chantier ;
- la mise à jour automatique de l'avancement.

La création des étapes elles-mêmes (tâches, matériel, durées) reste manuelle et relève du jugement du chef de chantier ; ce domaine n'automatise que le suivi et les notifications qui en découlent.

---

### Terrain

Les scénarios de ce domaine concernent :

- les rapports terrain ;
- les documents ajoutés par les artisans ;
- les mises à jour d'avancement.

---

### Facturation

Les automatisations liées :

- à la création des factures ;
- aux relances de paiement ;
- aux notifications administratives.

---

### Documents

Ce domaine avait initialement prévu l'organisation documentaire via Google Drive (création de dossiers, classement automatique). Ces automatisations ont été abandonnées — le besoin de stockage et de consultation documentaire est entièrement couvert nativement par la table Document chantier dans Airtable (cf. section 9.4).

---

### Intelligence artificielle

Les scénarios faisant intervenir un modèle d'intelligence artificielle.

Par exemple :

- résumé automatique d'un rapport terrain ;
- analyse d'une demande de devis ;
- génération d'un email personnalisé.

Chaque domaine doit pouvoir évoluer indépendamment des autres.

---

## 8.3 Architecture des flux

L'architecture générale repose sur le principe suivant.

```
Utilisateur

        │

        ▼

Interface Airtable

        │

        ▼

Base Airtable

        │

        ▼

Automatisation Make

        │

 ┌──────┴──────┐

 ▼             ▼

Gmail          IA

        │

        ▼

Retour dans Airtable
```

Les données transitent toujours par Airtable, qui reste le référentiel unique du projet.

---

## 8.4 Utilisation des services externes

Les services externes ne doivent jamais modifier directement la base Airtable.

Toutes les interactions passent par Make.

Les principaux services prévus sont :

| Service | Utilisation prévue |
|----------|--------------------|
| Gmail | Notifications et emails |
| LLMs | Traitements IA |
| Airtable | Référentiel métier |

Cette architecture facilite les évolutions futures et limite les dépendances entre les différents services.

---

## 8.5 Utilisation de l'intelligence artificielle

Les modèles d'intelligence artificielle ne doivent être utilisés que lorsque leur apport est significatif.

Ils interviennent principalement pour :

- analyser des textes ;
- générer du contenu ;
- classer des informations ;
- résumer des rapports.

L'IA ne doit jamais remplacer des traitements déterministes pouvant être réalisés directement par Airtable ou Make.

Les réponses produites par l'IA doivent être structurées afin de pouvoir être exploitées automatiquement par les scénarios Make.

Lorsque cela est possible, le format JSON est privilégié.

---

## 8.6 Évolutivité

Les nouvelles automatisations doivent pouvoir être ajoutées sans remettre en cause l'architecture existante.

Avant de créer un nouveau scénario, il convient de vérifier :

- si un scénario existant peut être réutilisé ;
- si la logique métier appartient réellement au domaine concerné ;
- si une automatisation native Airtable est suffisante.

L'objectif est de limiter le nombre de scénarios tout en conservant une responsabilité claire pour chacun.

### Décisions retenues

Pour NeoBati, les principes suivants sont retenus :

- Airtable constitue le référentiel unique des données.
- Make orchestre les processus métier et les échanges avec les services externes.
- Les scénarios sont organisés par domaine métier et non par technologie.
- Les traitements IA sont isolés des traitements déterministes.
- Les données reviennent systématiquement dans Airtable après un traitement externe.
- Les automatisations sont conçues pour être indépendantes, réutilisables et facilement maintenables.

# 9. Cartographie des automatisations

Ce chapitre présente l'architecture cible des automatisations de NeoBati.

Les automatisations sont organisées par domaine métier afin de refléter l'organisation fonctionnelle du système plutôt que la structure technique des scénarios Make.

Chaque domaine regroupe un ensemble de processus poursuivant un même objectif métier.

Cette organisation facilite :

- la compréhension de l'architecture globale ;
- la maintenance des scénarios ;
- les évolutions futures du projet ;
- la répartition des responsabilités.

Les automatisations décrites dans ce chapitre constituent la feuille de route technique du projet.

Leur implémentation sera réalisée progressivement.

Les statuts suivants sont utilisés :

- Prévue
- En cours de développement
- Implémentée
- À améliorer

---

## 9.1 Vue d'ensemble

| Domaine métier | Objectif |
|----------------|----------|
| Gestion commerciale | Transformer une demande de devis en chantier. |
| Gestion des chantiers | Piloter la réalisation opérationnelle des travaux. |
| Gestion documentaire | Organiser automatiquement les documents du projet. |
| Gestion de la facturation | Automatiser le suivi administratif et financier. |
| Assistance intelligente | Utiliser l'IA pour assister les collaborateurs dans certaines tâches. |

---

## 9.2 Domaine métier — Gestion commerciale

### Objectif

Automatiser le traitement des demandes commerciales depuis leur réception jusqu'à la création d'un chantier.

### Automatisations prévues

| Référence | Processus automatisé | Déclencheur | Statut |
|------------|----------------------|-------------|---------|
| AUT-COM-001 | Création automatique d'un client si inexistant | Nouvelle demande de devis (webhook) | Implémentée |
| AUT-COM-002 | Notification du chargé d'affaires | Nouvelle demande de devis (webhook) | Implémentée|
| AUT-COM-003 | Relance automatique des devis | Exécution planifiée (jours ouvrés, 10h) | Implémentée |
| AUT-COM-004 | Création automatique d'un chantier après acceptation d'un devis | Devis accepté (webhook)| Implémentée |

### AUT-COM-001 — Détail d'implémentation

**Déclenchement.** Le déclencheur documenté initialement ("Nouvelle demande de devis") s'appuie en pratique sur un mécanisme en deux temps, car aucune action native "Envoyer une requête Web" n'est disponible dans les automatisations Airtable de ce plan. Une automatisation Airtable native ("Quand un enregistrement est créé" sur la table Demande de devis) déclenche une action "Exécuter le script", dont le code JavaScript envoie un webhook POST vers Make via `fetch()`. L'URL du webhook est stockée dans un code secret Airtable (`MAKE_WEBHOOK_URL`), non en clair dans le script. Ce choix s'écarte du principe de simplicité "no-code" habituellement privilégié, mais reste justifié : c'est la seule option native disponible pour ce besoin sur ce plan Airtable.

**Architecture du scénario Make.** Le scénario recherche un client existant par e-mail normalisé (`LOWER(TRIM(...))`) avant toute création, afin d'éviter les doublons. Deux branches distinctes gèrent respectivement l'absence et la présence d'un client correspondant :

- **Client non trouvé** : création d'un nouvel enregistrement Client (statut "Prospect"), avec liaison à la Demande de devis réalisée via le champ symétrique `DEMANDEDEVIS_Client` (relation bidirectionnelle Airtable), sans module d'écriture séparé sur la table Demande de devis.
- **Client trouvé** : mise à jour directe du champ `CLIENT_Demande` sur la Demande de devis avec l'ID du client trouvé. Une alerte est envoyée si plusieurs clients correspondent au même e-mail (doublon existant), sans fusion automatique.

**Gestion des erreurs.** Chaque module Airtable (recherche, création, mises à jour) dispose d'une route d'erreur dédiée : notification par e-mail suivie de la directive **Commit**, qui arrête l'exécution du cycle en cours sans traiter les modules suivants. La directive Skip a été testée puis écartée : elle ignore l'enregistrement en erreur mais laisse le scénario se poursuivre avec des données invalides, ce qui n'est pas acceptable ici.

**Coexistence avec le bouton manuel "Créer le client".** Le bouton manuel de l'interface Chargé d'affaires (automatisation Airtable native, sans recherche de doublon) est conservé en filet de sécurité temporaire. Un usage de ce bouton sur une Demande de devis déjà traitée par AUT-COM-001 peut créer un client en double, car ce bouton ne fait aucune vérification par e-mail contrairement à l'automatisation. Ce risque est accepté pour l'instant ; la suppression du bouton est une évolution envisagée à terme.

**Point technique confirmé.** La valeur par défaut du champ Chargé d'affaires (table Client) s'applique correctement même lors d'une création via l'API Airtable (donc via Make), ce qui n'était pas garanti a priori.

### AUT-COM-002 — Détail d'implémentation

**Besoin métier.** Informer automatiquement le chargé d'affaires dès qu'une nouvelle demande de devis est enregistrée, afin de réduire le délai de prise en charge commerciale.

**Choix d'architecture.** Un scénario Make totalement autonome, indépendant d'AUT-COM-001, conformément au principe de responsabilité unique retenu au chapitre 4.1. Ce découpage a été confirmé pertinent après vérification qu'il n'existe qu'un seul chargé d'affaires dans l'entreprise à ce stade du projet : la notification ne dépend donc d'aucune donnée produite par la recherche ou la création du client (AUT-COM-001), et ne nécessite aucune dépendance entre les deux scénarios.

**Déclenchement.** Une seconde automatisation Airtable native, indépendante de celle d'AUT-COM-001, sur le même événement ("Quand un enregistrement est créé" sur Demande de devis). Un script dédié envoie un webhook POST vers un second scénario Make, via un code secret distinct (`MAKE_WEBHOOK_URL_COM002`).

**Architecture du scénario Make.** Volontairement minimale : Webhook → Gmail, sans traitement intermédiaire. Le corps de l'e-mail est structuré en deux sections HTML : informations du demandeur (nom, e-mail, téléphone, adresse, type) et informations sur le projet (description, type de chantier, adresse du chantier, budget estimé, date de démarrage souhaitée). Le destinataire est une adresse fixe, l'entreprise ne comptant qu'un seul chargé d'affaires.

**Pièces jointes — fonctionnalité abandonnée.** L'envoi des documents joints à la demande (photos, plans) en pièces jointes de l'e-mail a été envisagé, conçu et partiellement implémenté, mais abandonné après un comportement non résolu du module Make Array aggregator lors de l'agrégation de contenus binaires (fichiers téléchargés) : le module produisait systématiquement un bundle de sortie par fichier au lieu d'un bundle unique regroupant l'ensemble des pièces jointes, provoquant l'envoi d'un e-mail séparé par document plutôt qu'un e-mail unique. Cause non confirmée avec certitude (suspicion d'un problème spécifique à l'agrégation de buffers binaires volumineux dans Make), non documentée officiellement par l'éditeur. Cette limitation pourra être réexaminée ultérieurement si le besoin redevient prioritaire, par exemple via un encodage base64 des fichiers directement dans le script Airtable plutôt que par téléchargement côté Make.

**Gestion des erreurs.** Aucun error handler mis en place : le scénario ne réalise aucune écriture ni lecture Airtable, un échec d'envoi Gmail est jugé non bloquant pour l'intégrité des données du projet, cohérent avec la politique retenue sur les autres notifications du domaine commercial.

**Point de vigilance.** AUT-COM-001 et AUT-COM-002 sont désormais deux automatisations Airtable natives indépendantes, déclenchées sur le même événement ("nouvel enregistrement créé" dans Demande de devis). Un test en conditions réelles confirme qu'elles s'exécutent sans se bloquer mutuellement, mais Airtable ne garantit pas d'ordre d'exécution entre deux automatisations natives déclenchées sur le même événement. Ce n'est pas un problème actuellement, les deux scénarios étant totalement indépendants l'un de l'autre. Si une future automatisation venait à se greffer sur ce même événement avec une dépendance d'ordre vis-à-vis de l'une des deux existantes, l'architecture actuelle devrait être revue.

**Statut : Implémentée.**

### AUT-COM-003 — Détail d'implémentation

**Besoin métier.** Relancer automatiquement les clients dont le devis reste sans réponse au-delà d'un délai défini, jusqu'à un plafond de 3 relances, et faire basculer automatiquement au statut "Expiré" tout devis dont la date de validité est dépassée sans réponse — sans intervention manuelle du chargé d'affaires pour ces tâches répétitives.

**Choix d'architecture.** Un seul scénario Make à deux branches (Router après le déclencheur), plutôt que deux scénarios séparés : la relance et la gestion de l'expiration relèvent d'un même processus métier plus large ("gestion quotidienne du cycle de vie des devis en attente"), et réutilisent un même déclencheur planifié quotidien plutôt que d'en dupliquer un second pour un besoin très proche.

**Déclencheur.** Module Schedule, jours ouvrés (lundi-vendredi), 10h00, fuseau Europe/Paris.

**Logique d'éligibilité déportée dans Airtable.** Deux vues filtrées portent l'intégralité de la logique métier, plutôt que de dupliquer des formules dans Make :
- Vue "Devis à relancer", pilotée par le champ formule `ARelancer` : statut Envoyé ou En attente, ancienneté suffisante depuis l'envoi ou la dernière relance (5 puis 15 jours), plafond de 3 relances (`NombreRelances < 3`), et date de validité non dépassée.
- Vue "AUT-COM-003 - Devis expirés à traiter" : statut Envoyé ou En attente, date de validité antérieure à aujourd'hui.

Un champ formule complémentaire, `JoursRestantsValidite`, calcule le nombre de jours restants avant expiration et alimente le contenu de l'e-mail de relance.

**Route 1 — Relance.** Recherche des devis de la vue "À relancer" (sans formule dupliquée côté Make), rédaction assistée par IA du corps du message (voir ci-dessous), envoi d'un e-mail personnalisé au client (coordonnées récupérées via deux champs Lookup sur la table Devis, `NomClient_CLIENT` et `EmailClient_CLIENT`, plutôt que par une recherche Make supplémentaire), incrémentation de `NombreRelances` et mise à jour de `DateDerniereRelance`. Si le compteur atteint 3 après incrémentation, une notification est envoyée au chargé d'affaires pour signaler qu'une action manuelle est recommandée.

**Rédaction assistée par IA du corps de la relance.** Conformément à l'exigence du cahier des charges ("rédaction assistée des relances clients"), un module OpenAI (Create a Chat Completion, modèle `gpt-4.1-mini-2025-04-14`, daté plutôt qu'un alias "(system)" pour garantir un comportement stable dans le temps) est inséré entre le filtre de garde initial et l'envoi Gmail, uniquement sur la Route 1.

Choix du modèle : les familles de raisonnement (o1/o3/o4-mini, GPT-5.x y compris les variantes mini/nano) ont été écartées après un premier test infructueux avec `gpt-5-mini` — ce modèle consomme des tokens de raisonnement internes prélevés sur le même budget que `Max Output Tokens`, ce qui a produit une réponse vide avec une limite de 300 tokens. `gpt-4.1-mini` ne raisonne pas en interne : tous les tokens de sortie servent au texte visible, avec un coût stable et prévisible — cohérent avec la recommandation du cahier des charges de maîtriser le coût d'exécution des scénarios.

Le module ne génère que le corps rédactionnel du message, jamais l'e-mail complet : l'objet, la formule d'ouverture, le rappel du délai de validité (`JoursRestantsValidite`) et la signature restent gérés par un template Gmail fixe. Ce découpage respecte le principe retenu au chapitre 5.3 (les données factuelles — dates, montants — restent des traitements déterministes, non confiés à l'IA) et limite le risque d'hallucination.

Le prompt système impose : l'absence de toute date, délai ou montant dans le texte généré (ajoutés séparément par le template) ; l'absence de promesse commerciale non fournie ; un texte de 3 à 5 phrases sans objet ni formule de politesse ; et surtout une différenciation explicite du registre selon `NombreRelances` (0 : ton de découverte, 1 : rappel avec proposition d'échange, 2 : signal explicite de dernière sollicitation avant clôture du dossier). Une première version du prompt ne portait qu'une consigne qualitative unique ("adapte le ton progressivement"), sans effet observable sur les trois paliers testés ; le passage à une instruction dédiée par valeur de `NombreRelances` a résolu ce point.

Le message utilisateur transmet uniquement `NomClient_CLIENT`, `NombreRelances` et `JoursRestantsValidite` (ce dernier à titre de contexte, sans consigne de le citer) — aucun nouveau champ Lookup n'a été nécessaire sur Devis.

**Mise en forme du corps généré.** Le texte produit par le modèle est restitué comme un bloc continu, sans retour à la ligne exploitable en HTML. Une première tentative a consisté à demander au modèle d'insérer lui-même un saut de ligne entre chaque phrase : le résultat n'était pas fiable (environ 3 exécutions sur 4), une consigne de mise en forme n'étant pas restituée avec la même constance qu'une consigne de fond par un LLM. La mise en forme a donc été déplacée côté Make, comme traitement déterministe : la formule `replace(replace(35.Result; newline; " "); ". "; ".<br>")` neutralise d'abord tout saut de ligne résiduel, puis insère systématiquement un `<br>` après chaque point suivi d'un espace. Le prompt système a été simplifié en conséquence (retrait de la consigne de mise en forme), l'IA restant responsable du seul contenu.

**Point technique — guillemets dans les formules Make.** Contrairement à la convention initialement documentée en section 4.7 (contournement par guillemets simples), la formule ci-dessus fonctionne sans aucun guillemet (ni double, ni simple) autour des chaînes littérales `" "`, `". "` et `".<br>"` : les ajouter provoque une mauvaise interprétation de la formule sur cette instance Make. À vérifier au cas par cas selon le contexte du champ, cette précision complète (sans la remplacer) le piège déjà documenté sur la suppression des guillemets doubles adjacents à une puce de variable.

**Filtre de garde IA.** Un filtre `35.Result → Exists` est positionné entre le module OpenAI et l'envoi Gmail, pour éviter l'envoi d'un e-mail au corps vide si le module réussit techniquement sans produire de contenu — même logique que le filtre de garde sur les Search Records (section 4.7).

**Route 2 — Expiration.** Recherche des devis de la vue "Devis expirés à traiter", passage du statut à "Expiré" (aucun autre champ modifié), puis notification au chargé d'affaires.

**Protection contre les recherches sans résultat.** Chaque module Airtable Search Records est suivi d'un filtre de garde (`ID → Exists`) avant tout module de traitement en aval, conformément au piège technique documenté en section 4.7.

**Gestion des erreurs.** Chaque module Airtable (deux Search Records, deux Update a Record) et le module OpenAI de rédaction disposent chacun d'une route d'erreur dédiée : notification par e-mail suivie de la directive Commit, cohérente avec la politique retenue sur AUT-COM-001. Un échec du module IA (quota, timeout, clé invalide) n'interrompt donc pas silencieusement le scénario : le devis concerné n'est pas relancé ce jour-là, mais reste éligible au cycle suivant tant qu'il figure dans la vue "À relancer" — cohérent avec le point de vigilance déjà accepté sur le plafond de relance.

**Point de vigilance non traité.** Aucune limite n'est imposée au nombre de cycles de relance au-delà du plafond de 3 : un devis qui atteint ce plafond reste en statut Envoyé ou En attente indéfiniment (sauf expiration), avec une notification unique au chargé d'affaires. Aucun mécanisme n'empêche qu'il soit à nouveau proposé à la relance si son statut ou ses dates étaient modifiés manuellement par la suite — comportement jugé acceptable, la vigilance reposant sur l'intervention humaine signalée par la notification.

**Historisation de la relance (ajout).** Après l'envoi confirmé de l'e-mail de relance, un module Airtable Create a Record crée un enregistrement dans la table `Interaction client` (cf. 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md, section 3.12) : type « Relance devis », client et devis concernés, contenu du message envoyé, date, numéro de relance. Ce module est indépendant de la mise à jour de `NombreRelances`/`DateDerniereRelance` sur Devis, qui continue de piloter l'éligibilité aux relances (`ARelancer`) sans dépendre de cet ajout. Une route d'erreur dédiée (e-mail de notification + Commit) couvre ce module, selon la convention retenue sur l'ensemble du scénario ; un échec de cette écriture n'affecte pas la relance déjà envoyée au client.

**Statut : Implémentée.**

### AUT-COM-004 — Détail d'implémentation

**Besoin métier.** Créer automatiquement un enregistrement Chantier dès qu'un Devis passe au statut "Accepté", en reprenant les informations pertinentes du devis (client, description, adresse, montant HT), sans jamais créer de doublon si le statut du devis repasse plusieurs fois par "Accepté" (annulation puis nouvelle acceptation, par exemple).

**Déclenchement.** Une automatisation Airtable native ("Quand un enregistrement correspond aux conditions", table Devis, condition `Statut = Accepté`) déclenche une action "Exécuter le script", qui envoie un webhook POST vers Make via `fetch()`, selon le même mécanisme que AUT-COM-001/002 (aucune action native "Envoyer une requête Web" disponible sur ce plan Airtable). L'URL du webhook est stockée dans un code secret dédié (`MAKE_WEBHOOK_URL_COM004`), récupérée via `input.secret()` plutôt que codée en clair — une première tentative sans cet appel a échoué (`TypeError: Invalid URL`), le script tentait littéralement d'ouvrir une connexion vers le nom du secret au lieu de sa valeur. Le script transmet uniquement l'identifiant du Devis déclencheur (`devisId`) ; l'ensemble des autres données est récupéré côté Make au moment de l'exécution, afin de garantir des données à jour plutôt que figées au moment du déclenchement.

**Choix d'architecture — garde anti-doublon.** L'architecture initialement envisagée reposait sur un Search Records sur la table Chantier, filtré par le champ lié `DEVIS_Chantier`. Cette approche a été abandonnée en cours de construction : une formule Airtable de type `ARRAYJOIN({DEVIS_Chantier}) = "{{devisId}}"` ne peut pas fonctionner, car `ARRAYJOIN` sur un champ lié renvoie le texte affiché de l'enregistrement lié (son champ primaire, par exemple "DEV-010"), jamais son Record ID — alors que `devisId` transmis par le webhook est bien un Record ID. Airtable ne permet pas d'extraire l'ID d'un enregistrement lié dans une formule sans passer par un champ Formula `RECORD_ID()` créé sur la table source, ce qui aurait ajouté un champ technique supplémentaire pour un besoin qui pouvait être résolu plus simplement.

L'architecture retenue exploite la relation symétrique déjà confirmée entre Devis et Chantier (`CHANTIER_Devis` / `DEVIS_Chantier`) : si le champ `CHANTIER_Devis` du Devis déclencheur est vide, aucun Chantier n'existe encore pour ce Devis. Cette vérification se fait directement sur le Devis, sans interroger la table Chantier.

**Architecture du scénario Make.** Webhook → Airtable Get a Record (Devis) → filtre de garde → Airtable Create a Record (Chantier).

- **Get a Record** sur Devis, Record ID = `{{devisId}}`. Récupère en un seul point : Client, Type de chantier, nom du client (via un champ Lookup ajouté sur Devis pour ce besoin), Montant HT, et `CHANTIER_Devis`.
- **Filtre de garde** : continue uniquement si `CHANTIER_Devis` est vide (n'existe pas). Si un Chantier est déjà lié, le scénario s'arrête à cet endroit sans notification — ce cas correspond à un ré-enclenchement normal du déclencheur (statut repassé à Accepté), pas à une anomalie.
- **Create a Record** sur Chantier :

| Champ Chantier | Source | Nature de l'écriture |
|---|---|---|
| `DEVIS_Chantier` | Record ID du Devis | Écrit par Make (lien symétrique — `CHANTIER_Devis` se remplit automatiquement côté Devis, aucun module d'écriture séparé) |
| `CLIENT_Chantier` | Client (Devis) | Écrit par Make |
| `Budget` | Montant HT (Devis) | Écrit par Make |
| `Nom` | Type de chantier + nom du client (Devis, via Lookup) | Écrit par Make, champ texte simple resté éditable ensuite |
| `Description` | — | Non mappé : champ Lookup, calculé automatiquement dès l'écriture de `DEVIS_Chantier` |
| `AdresseChantier` | — | Non mappé : champ Lookup, calculé automatiquement |
| `StatutChantier` | — | Non mappé : champ Formula, non éditable par Make |
| `DateDemarrage_fx` | — | Non mappé : champ Rollup (`MIN` des dates de début prévues des Étapes liées), reste vide tant qu'aucune Étape n'a été créée manuellement pour ce chantier |

**Convention retenue — champ Nom.** Contrairement à `Description` et `AdresseChantier`, le champ `Nom` de la table Chantier est un champ texte simple, volontairement laissé éditable après la création automatique : l'usage constaté sur les chantiers existants montre que le nom du client y est souvent reformulé ou raccourci à la main (ex. "Cabinet Loire Architecture" devient "Loire" dans le nom du chantier "Bureaux Loire"). Une Formula stricte aurait figé ce champ et empêché cet ajustement éditorial. Make initialise donc `Nom` avec une concaténation simple (Type de chantier + nom du client) au moment de la création, sans empêcher une correction manuelle ultérieure par le chargé d'affaires. Un champ IA natif Airtable (AI field) a été envisagé pour générer ce nom à partir de la description du projet, puis écarté : le besoin est un traitement déterministe (une étiquette d'identification, pas une synthèse), et un champ IA introduirait une non-homogénéité entre chantiers ainsi qu'un coût récurrent sans valeur ajoutée réelle, contrairement au principe retenu au chapitre 5.3. Cette convention n'était pas documentée avant AUT-COM-004 et devra être ajoutée au chapitre 6 lors d'une prochaine mise à jour de ce guide.

**Gestion des erreurs.** Les deux modules Airtable (Get a Record, Create a Record) disposent chacun d'une route d'erreur dédiée : notification par e-mail suivie de la directive **Commit**, cohérente avec la politique retenue depuis AUT-COM-001.

**Point de vigilance — champs calculés (résolu).** `StatutChantier` (Formula) et `DateDemarrage_fx` (Rollup sur les Étapes) sont des champs calculés non éditables par Make : toute tentative d'écriture échouerait. Cette contrainte, découverte au moment de configurer le Create Record d'AUT-COM-004, a depuis été documentée dans 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md (table Chantier, rubrique Planning, « Remarque technique »), qui signale explicitement les quatre champs calculés à partir des Étapes (`StatutChantier`, `DateDemarrage_fx`, `DateFinEstimee_fx`, `DateFinReelle`). Une prochaine automatisation ne devrait donc plus reproduire l'hypothèse erronée d'un champ éditable.

**Intégration avec le reste du système.** La création d'un Chantier par AUT-COM-004 déclenche AUT-CHA-002 (notification du chef de chantier), seule automatisation réagissant à cet événement — AUT-DOC-001, envisagée initialement sur le même déclencheur, a été abandonnée (cf. section 9.4). AUT-COM-004 se limite strictement à la création du Chantier et de son lien vers le Devis ; la création des étapes (manuelle, cf. section 9.3) reste hors de son périmètre, conformément au principe de responsabilité unique retenu au chapitre 8.1. Les champs calculés dépendant des Étapes (`DateDemarrage_fx`, `StatutChantier`, etc.) ne se peupleront qu'une fois les étapes créées manuellement par le chef de chantier, généralement à la suite de la notification d'AUT-CHA-002.

**Statut : Implémentée.**

---

## 9.3 Domaine métier — Gestion des chantiers

### Objectif

Automatiser les processus liés au suivi opérationnel des chantiers.

### Automatisations prévues

| Référence | Processus automatisé | Déclencheur | Statut |
|------------|----------------------|-------------|---------|
| AUT-CHA-001 | Génération automatique des étapes d'un chantier | Nouveau chantier | Abandonnée |
| AUT-CHA-002 | Notification du chef de chantier | Nouveau chantier | Implémentée |
| AUT-CHA-003 | Mise à jour automatique de l'avancement du chantier | Modification des étapes | Abandonnée |
| AUT-CHA-004 | Notification en cas de retard important | Contrôle planifié | Implémentée |
| AUT-CHA-005 | Notification étape en retard (chef de chantier + artisan) | Contrôle planifié | Implémentée |
| AUT-CHA-006 | Notification changement de statut d'une étape (En cours / Terminée) | Modification du statut d'une étape | Implémentée |
| AUT-CHA-007 | Alerte dépassement budgétaire | Modification du coût total d'un chantier | Implémentée |
| AUT-CHA-008 | Notification de démarrage du chantier (chef de chantier, artisans, Direction) | Chantier prêt à démarrer | Implémentée |

**Note sur AUT-CHA-001.** Cette automatisation a été abandonnée après analyse : la définition des étapes d'un chantier (tâches, matériel nécessaire, durées) est un traitement non déterministe et fortement dépendant du contexte réel de chaque chantier, qui relève du jugement métier du chef de chantier. Une génération automatique produirait des étapes génériques nécessitant une reprise manuelle complète, ce qui va à l'encontre du principe retenu au chapitre 5.3 (un traitement non déterministe n'est confié à une automatisation ou une IA que si elle apporte une réelle valeur ajoutée). La création des étapes reste donc entièrement manuelle, via la table Étape ou un formulaire dédié dans l'interface Chef de chantier.

**Note sur AUT-CHA-003.** Cette automatisation a été abandonnée après vérification que le pourcentage d'avancement du chantier (`Avancement(%)`, champ Formule) est déjà entièrement calculé nativement, à partir de deux champs eux-mêmes automatiques : `NbrEtapesTotales` (champ Quantité, comptage des Étapes liées via `ETAPES_Chantier`) et `NbrEtapesTerminee` (champ Cumul, `SUM(values)` sur le champ Formule `EstTerminée` des Étapes liées). Ces trois champs se recalculent instantanément à chaque création, suppression ou changement de statut d'une Étape, sans nécessiter de déclencheur externe. Une automatisation Make serait redondante avec ce mécanisme natif, introduirait une latence et un point de défaillance évitables, et ne pourrait de toute façon pas écrire directement sur `Avancement(%)`, ce champ étant une Formule non éditable.

**Note sur AUT-CHA-005.** Cette automatisation ne figurait pas dans le plan initial des 18 automatisations, mais elle s'inscrit dans l'exigence du cahier des charges sur les "notifications internes ... retard détecté", qui ne précise pas de granularité (chantier ou étape). Elle a été ajoutée en cours de développement, à l'initiative du porteur du projet, en complément d'AUT-CHA-004 qui couvre le retard au niveau du chantier.

**Note sur AUT-CHA-008.** Cette automatisation n'était identifiée ni dans le plan initial des 18 automatisations, ni dans la feuille de route de mise en conformité établie lors de l'audit (section 9.7). Elle a été ajoutée après la clôture de cet audit, à l'initiative du porteur du projet, sur le même raisonnement que celui ayant justifié l'ajout d'AUT-CHA-005 : le cahier des charges demande des "scénarios automatisés (jalons, notifications...)" sans lister exhaustivement chaque jalon attendu. Le démarrage effectif d'un chantier — matérialisé par la case `PretADemarrer` — constitue un jalon de même nature que le retard (AUT-CHA-004/005) ou le changement de statut d'une étape (AUT-CHA-006), déjà couverts par des notifications. Contrairement à ces dernières, la difficulté propre à AUT-CHA-008 est de notifier un nombre variable de destinataires (les artisans affectés aux étapes du chantier) plutôt qu'un destinataire unique par rôle — cf. détail d'implémentation pour l'architecture retenue.

### AUT-CHA-002 — Détail d'implémentation

**Besoin métier.** Informer le ou les chefs de chantier dès qu'un nouveau Chantier est créé, afin qu'un chef de chantier se désigne responsable et prenne en charge la préparation (étapes, artisans, matériel).

**Déclenchement.** Une automatisation Airtable native, indépendante d'AUT-COM-004 ("Quand un enregistrement est créé", table Chantier), déclenche une action "Exécuter le script". Ce découpage respecte le principe de responsabilité unique déjà retenu sur AUT-COM-001/002 : AUT-COM-004 se limite à la création du Chantier, la notification est un processus distinct qui réagit au même événement plutôt que d'être chaînée dans le même scénario.

**Saisies du script.** Six input variables, chacune mappée directement sur un champ du Chantier déclencheur (sans lecture supplémentaire dans le script) :
- `recordId` (Record ID)
- `nomChantier` (Nom)
- `nomClient` (`Nom_CLIENT_Chantier`, champ Lookup — cf. section 4.7 sur le mapping des champs liés)
- `description` (Description du projet)
- `adresse` (Adresse du chantier)
- `budget` (Budget du chantier)

Le script se contente de relayer ces valeurs vers Make via un webhook POST, sans requête supplémentaire vers la base (`base.getTable()` / `selectRecordAsync()` volontairement écartés ici, ces champs n'étant pas de type Attachment — cf. section 4.7 sur ce point).

**Déclenchement du webhook.** L'URL est stockée dans un secret dédié (`MAKE_WEBHOOK_URL_CHA002`), récupérée via `input.secret()`, cohérent avec la politique retenue depuis AUT-COM-001.

**Architecture du scénario Make.** Volontairement minimale, comme AUT-COM-002 : Webhook → Gmail, sans module Airtable, sans traitement intermédiaire.

**Destinataire — limitation assumée.** Le champ `ChefChantierResponsable` (table Chantier) est vide à la création : aucune automatisation ne désigne un chef de chantier. Le destinataire de l'e-mail est actuellement une adresse fixe (unique chef de chantier configuré à ce stade du développement), avec un texte explicite invitant le destinataire à se désigner responsable sur la fiche Chantier. Ce comportement est un placeholder assumé : à terme, avec plusieurs chefs de chantier réels, la diffusion devra se faire vers l'ensemble des chefs de chantier plutôt qu'une adresse unique — non implémenté à ce stade, cf. remarque de conception de la table Chantier en 00_.

**Corps de l'e-mail.** Nom du chantier, client, description, adresse, budget (omis si vide, sans erreur), suivi d'un lien générique vers la page "Nouveaux chantiers (à préparer)" de l'interface Chef de chantier.

**Gestion des erreurs.** Aucun error handler : le scénario ne lit ni n'écrit dans Airtable, un échec Gmail est non bloquant, cohérent avec la politique retenue sur AUT-COM-002.

**Intégration avec le reste du système.** Comme documenté en 9.2, la création d'un Chantier par AUT-COM-004 ne déclenche désormais qu'AUT-CHA-002 (celle-ci) — AUT-DOC-001, envisagée initialement sur le même événement, a été abandonnée (cf. section 9.4).

**Statut : Implémentée.**

### AUT-CHA-004 — Détail d'implémentation

**Besoin métier.** Notifier une seule fois le chef de chantier responsable d'un chantier passant en retard.

**Historique de conception.** La première version de cette automatisation reposait sur un champ `ANotifierRetard` (Formule) déclenchant une notification au jour 1 de retard puis tous les 5 jours, avec un Schedule quotidien (7j/7) pour éviter qu'un jour exact de rappel tombant un week-end ne soit définitivement manqué. Cette logique a été abandonnée au profit du pattern retenu sur AUT-CHA-005 (champ de suivi explicite `NotifieRetard`), pour deux raisons : une notification unique répond suffisamment au besoin réel, et le champ de suivi explicite rend le système plus simple et plus inspectable qu'une cadence pilotée par formule. Le champ `ANotifierRetard` a été supprimé, n'étant utilisé nulle part ailleurs dans le projet.

**Champ Airtable créé — `NotifieRetard`** (Checkbox, table Chantier). Coché automatiquement par Make une fois la notification envoyée ; garantit qu'un chantier n'est notifié qu'une seule fois.

**Vue support.** "AUT-CHA-004 - Chantiers à notifier (retard)", filtrée sur : `EnRetard = "Oui"` ET `NotifieRetard` non coché ET `ChefChantierResponsable` non vide. Un chantier en retard sans chef de chantier assigné n'est volontairement pas remonté : aucun destinataire de repli n'a été retenu (le chargé d'affaires a été explicitement écarté comme destinataire de cette notification).

**Déclencheur.** Module Schedule, jours ouvrés (lundi-vendredi), 09h00, Europe/Paris. Le passage en quotidien retenu dans la première version n'a plus lieu d'être : avec `NotifieRetard` explicite, un chantier non encore notifié reste dans la vue jusqu'à son traitement, quel que soit le jour — plus aucun risque de notification définitivement manquée.

**Modules.** Airtable Search Records (vue ci-dessus) → filtre de garde `ID → Exists` (section 4.7) → Gmail Send an Email (notification) → Airtable Update Record (coche `NotifieRetard`).

**Ordre critique Gmail → Update Record.** La notification doit impérativement s'exécuter avant la mise à jour de `NotifieRetard`, pour éviter qu'un échec d'envoi ne laisse un chantier marqué comme notifié sans qu'aucun e-mail n'ait été envoyé.

**Variables importantes.** `Nom`, `DateFinEstimee_fx`, `JoursRetardChantier`, `ChefChantierResponsable:Email`, `ChefChantierResponsable:Name`.

**Destinataire.** `ChefChantierResponsable:Email`, résolu dynamiquement par chantier.

**Corps de l'e-mail.** Nom du chantier, date de fin estimée, nombre de jours de retard, suivi d'un lien vers la page "Liste des chantiers" de l'interface.

**Écritures Airtable.** `NotifieRetard = true` sur le chantier traité, une fois la notification envoyée avec succès. Vérifié en test : la mise à jour ne touche que ce champ, `ChefChantierResponsable` et tous les autres champs du chantier restent inchangés.

**Gestion des erreurs.** Error handler attaché au module Update Record, directive `Commit` (section 4.7). Si l'écriture échoue, `NotifieRetard` reste décoché et le chantier sera retraité à l'exécution suivante. Aucun error handler sur le module Gmail, cohérent avec la politique retenue sur les autres notifications du projet.

**Intégration avec le reste du système.** Indépendant d'AUT-CHA-005 malgré un pattern identique (déclencheur, champ de suivi, ordre des modules) — table, destinataire et contenu distincts, aucune mutualisation pertinente. Aucune automatisation existante n'écrit sur `EnRetard`, `NotifieRetard` ou `ChefChantierResponsable`.

**Statut : Implémentée.**

### AUT-CHA-005 — Détail d'implémentation

**Besoin métier.** Notifier une seule fois, par étape, le chef de chantier et l'artisan affecté dès qu'une étape passe en retard — distinct d'AUT-CHA-004, qui porte sur le retard au niveau du Chantier avec une cadence de rappel répétée.

**Champ Airtable créé — `NotifieRetard`** (Checkbox, table Étape). Coché automatiquement par Make une fois la notification envoyée ; garantit qu'une étape n'est notifiée qu'une seule fois, indépendamment de toute mémorisation côté Make.

**Rejet du module Watch Records.** Une première version du scénario utilisait un module Watch Records (déclencheur `Créé le`). Ce mécanisme a été abandonné après analyse : Watch Records ne remonte que les enregistrements dont le champ surveillé progresse dans le temps en corrélation avec leur entrée dans la vue. Or la date de création d'une étape (`Créé le`) et son passage en retard (`EnRetard`) sont deux événements totalement décorrélés — une étape ancienne peut basculer en retard bien après que Make ait mémorisé une valeur de `Créé le` plus récente, et serait alors silencieusement ignorée. Le pattern Schedule + Search Records + champ de suivi explicite (`NotifieRetard`), déjà éprouvé sur AUT-CHA-004, a été retenu à la place : la logique "une seule fois" devient inspectable directement dans Airtable plutôt que dépendante d'un état caché dans Make.

**Champs Recherche créés sur Étape :**
- `ArtisanResponsable` : Recherche sur le champ `Collaborateur` de la table Artisan, via le lien `ARTISANT_Etape`.
- `ChefChantierResponsable_CHANTIER_Etape` : Recherche sur le champ `ChefChantierResponsable` de la table Chantier, via le lien `CHANTIER_Etape`.

Ces deux champs exposent nom et e-mail exploitables directement dans Make, `Collaborateur` et `ChefChantierResponsable` étant tous deux des champs Utilisateur/Collaborator natifs.

**Vue support.** "AUT-CHA-005 : Notification étape en retard", filtrée sur : `EnRetard = "Oui"` ET `NotifieRetard` non coché, combiné à `ArtisanResponsable` non vide ET `ChefChantierResponsable_CHANTIER_Etape` non vide. Un e-mail unique à deux destinataires obligatoires a été retenu par choix : si un seul des deux rôles est assigné, l'étape n'est pas remontée et personne n'est notifié — limitation assumée, cohérente avec le traitement déjà appliqué aux chantiers sans chef assigné en AUT-CHA-004.

**Déclencheur.** Module Schedule, jours ouvrés (lundi-vendredi), 09h00, Europe/Paris.

**Modules.** Airtable Search Records (vue ci-dessus) → filtre de garde `ID → Exists` (section 4.7) → Tools Set multiple variables (mise en forme des e-mails artisan/chef) → Gmail Send an Email (notification) → Airtable Update Record (coche `NotifieRetard`).

**Ordre critique Gmail → Update Record.** La notification doit impérativement s'exécuter avant la mise à jour de `NotifieRetard` : si l'ordre était inversé, un échec d'envoi laisserait l'étape marquée comme notifiée sans qu'aucun e-mail n'ait été envoyé, la rendant définitivement ignorée par la vue.

**Variables importantes.** `EtapeID`, `DateFinPrevu`, `ChantierID_CHANTIER_Etape`, `ArtisanResponsable:Email`, `ChefChantierResponsable_CHANTIER_Etape:Email`.

**Destinataires.** Deux adresses sur le même e-mail (`ArtisanResponsable:Email` et `ChefChantierResponsable_CHANTIER_Etape:Email`), résolues dynamiquement par étape.

**Corps de l'e-mail.** Identifiant de l'étape (`EtapeID`, qui inclut déjà le nom lisible), identifiant du chantier (`ChantierID_CHANTIER_Etape`), date de fin prévue. Aucun lien vers l'interface, par choix — les deux destinataires n'ayant pas la même interface de destination naturelle (fiche Chantier pour le chef, page "Mes étapes" pour l'artisan), l'information brute a été jugée suffisante.

**Écritures Airtable.** `NotifieRetard = true` sur l'étape traitée, une fois la notification envoyée avec succès.

**Gestion des erreurs.** Error handler attaché au module Update Record, directive `Commit` (standard du projet, section 4.7). Si l'écriture échoue, `NotifieRetard` reste décoché et l'étape sera retraitée à l'exécution suivante. Aucun error handler sur le module Gmail : cohérent avec la politique retenue sur les autres notifications du projet.

**Intégration avec le reste du système.** Indépendant d'AUT-CHA-004 (déclencheur Schedule similaire, mais table, mécanique et destinataires distincts — aucune mutualisation pertinente). Aucune automatisation existante n'écrit sur `EnRetard`, `NotifieRetard`, `ArtisanResponsable` ou `ChefChantierResponsable_CHANTIER_Etape`.

**Statut : Implémentée.**

### AUT-CHA-006 — Détail d'implémentation

**Besoin métier.** Notifier les bonnes personnes à chaque changement de statut d'une Étape : le passage à "En cours" informe l'artisan affecté et le chef de chantier que l'intervention démarre ; le passage à "Terminée" informe l'artisan de l'étape suivante et le chef de chantier que le relais peut être pris.

**Redéfinition du périmètre.** La feuille de route (section 9.7) associait initialement à cette référence le signalement d'un problème bloquant sur un rapport terrain. Ce volet a été retiré du périmètre après cadrage : il s'agit d'un déclencheur distinct (création d'un Rapport terrain, et non modification d'une Étape), qui sera couvert par AUT-IA-001 (résumé automatique d'un rapport terrain, domaine Assistance intelligente, section 9.6) plutôt que dupliqué ici. AUT-CHA-006 se limite désormais au changement de statut d'Étape.

**Champ Airtable créé — `ArtisanResponsable_Etape_successeur`** (table Étape, Lookup). Expose l'e-mail de l'artisan affecté à l'étape suivante, via le lien auto-référentiel `Étape suivante`. Ce champ est un Lookup pointant vers `ArtisanResponsable`, qui est lui-même un champ Recherche (créé pour AUT-CHA-005) — un Lookup de Lookup, cas non rencontré jusqu'ici dans le projet. Confirmé fonctionnel en test : Airtable résout correctement la valeur finale (adresse e-mail) sans étape intermédiaire nécessaire côté Make.

**Règle métier justifiant l'absence de garde sur la route "En cours".** Contrairement à AUT-CHA-005 (qui exclut les étapes sans artisan ou sans chef de chantier assigné), la route "En cours" ne comporte aucune vérification de présence de `artisanResponsableEmail`. C'est un choix assumé : le champ `Statut` est modifié manuellement depuis l'interface Artisan, et seul l'artisan affecté à une étape peut faire passer celle-ci à "En cours" — `artisanResponsableEmail` est donc structurellement toujours renseigné à ce stade. Cette hypothèse ne doit pas être reproduite telle quelle pour une future automatisation sans revérifier que ce mécanisme d'affectation préalable reste inchangé.

**Déclenchement.** Une automatisation Airtable native, "Quand un enregistrement est mis à jour", table Étape, champ surveillé restreint à `Statut`. Une action "Exécuter le script" relaie les valeurs vers Make via un webhook POST, secret dédié `MAKE_WEBHOOK_URL_CHA006`, cohérent avec la politique retenue depuis AUT-COM-001.

**Saisies du script.** Sept input variables, mappées directement sur les champs de l'Étape déclencheuse : `recordId`, `nomEtape`, `statut`, `nomChantier`, `chefChantierEmail` (`ChefChantierResponsable_CHANTIER_Etape`), `artisanResponsableEmail` (`ArtisanResponsable`), `artisanEtapeSuivanteEmail` (`ArtisanResponsable_Etape_successeur`).

**Architecture du scénario Make.** Un seul déclencheur Webhook, deux niveaux de Router :
- Router 1 (Répartition selon Statut) : route "Statut = En cours" et route "Statut = Terminée". Toute autre valeur de `Statut` ne correspond à aucune route ; le scénario s'arrête silencieusement sans erreur, comportement voulu.
- Router 2 (Présence artisan étape suivante), en aval de la route "Terminée" uniquement : route "Si artisanEtapeSuivanteEmail existe" et route "Si artisanEtapeSuivanteEmail n'existe pas".

Ce choix reprend le pattern validé sur AUT-COM-003 : un déclencheur unique et un seul scénario pour un même processus métier ("suivre la progression d'une étape"), plutôt que deux automatisations Airtable natives dupliquant le même événement racine.

**Modules Gmail (3 au total).**
- "Notification étape en cours - CDC et artisan respo" : destinataires `chefChantierEmail` + `artisanResponsableEmail`.
- "Notification étape terminée - CDC et artisan suiva" : destinataires `chefChantierEmail` + `artisanEtapeSuivanteEmail`.
- "Notification étape terminée - CDC" : destinataire `chefChantierEmail` uniquement, utilisée quand l'étape terminée est la dernière du chantier (`Étape suivante` vide).

**Corps des e-mails.** Nom de l'étape, nom du chantier, statut atteint, et une phrase adaptée au contexte (invitation à démarrer / relais possible / dernière étape du chantier). Aucun lien vers l'interface : contrairement à AUT-CHA-002/004, aucune page de l'interface Chef de chantier ne correspond au suivi d'une étape individuelle dans `01_` — point à revoir si une telle page est ajoutée ultérieurement.

**Écritures Airtable.** Aucune — scénario de lecture et notification uniquement, comme AUT-CHA-002/004/005.

**Gestion des erreurs.** Route d'erreur sur le module Airtable du script (e-mail + directive Commit, politique standard depuis AUT-COM-001). Aucun error handler sur les modules Gmail, cohérent avec les autres notifications du projet.

**Intégration avec le reste du système.** `Statut` (table Étape) n'est écrit par aucune autre automatisation — modifié uniquement depuis l'interface Artisan et Chef de chantier. Aucun conflit avec AUT-CHA-004/005, qui portent sur le retard et non sur un changement d'état volontaire. Le champ `ArtisanResponsable_Etape_successeur` n'est consommé que par cette automatisation.

**Statut : Implémentée.**

### AUT-CHA-007 — Détail d'implémentation

**Besoin métier.** Alerter la direction et le chef de chantier responsable dès qu'un chantier dépasse son budget prévisionnel, afin de permettre une intervention avant que l'écart ne se creuse davantage — exigence explicite du cahier des charges ("détection conditionnelle : retard, dépassement budgétaire... et déclenchement d'alertes").

**Donnée déjà existante.** L'écart budgétaire était déjà calculé nativement avant cette automatisation, via le champ Formule `EcartBudget` (table Chantier) : `Budget - CoutTotalChantier`. Un résultat négatif signifie un dépassement, conformément à la formule de référence du cahier des charges (`Écart budget = Devis initial – Coût total réel`). Seule l'alerte manquait — cohérent avec le principe retenu depuis AUT-CHA-003 : ne jamais dupliquer un calcul déjà natif.

**Choix d'architecture — déclencheur événementiel plutôt que Schedule.** Contrairement à AUT-CHA-004/005 (Schedule + Search Records + champ de suivi), AUT-CHA-007 repose sur un déclencheur Airtable natif "Quand un enregistrement correspond aux conditions" (`EcartBudget < 0`). Ce choix a été validé après clarification du besoin réel : une notification est attendue à chaque nouveau franchissement du seuil vers le négatif, y compris si un chantier redevient positif puis renégatif par la suite — et non une seule notification pour la durée de vie du chantier. Le comportement natif de ce type de déclencheur (ne se réactive que sur la transition non-conforme → conforme) correspond exactement à ce besoin, sans nécessiter de champ de suivi ni de logique de garde supplémentaire.

**Condition de déclenchement composée.** `EcartBudget < 0` ET `ChefChantierResponsable` non vide. Un chantier en dépassement sans chef de chantier assigné n'est volontairement pas remonté — même limitation assumée que sur AUT-CHA-004 (aucun destinataire de repli retenu), cohérente avec le fait que `ChefChantierResponsable` reste un champ à affectation manuelle.

**Déclenchement.** Automatisation Airtable native, table Chantier, condition ci-dessus. Action "Exécuter le script" relaie les valeurs vers Make via un webhook POST, secret dédié `MAKE_WEBHOOK_URL_CHA007`, cohérent avec la politique retenue depuis AUT-COM-001.

**Saisies du script.** Sept input variables, mappées directement sur les champs du Chantier déclencheur : `recordId`, `nomChantier`, `nomClient` (`Nom_CLIENT_Chantier`), `ecartBudget` (`EcartBudget`), `budgetChantier` (`Budget`), `coutTotalChantier` (`CoutTotalChantier`), `chefChantierEmail` (`ChefChantierResponsable`).

**Architecture du scénario Make.** Volontairement minimale, comme AUT-CHA-002 : Webhook → Gmail, sans Router (un seul cas métier, condition déjà filtrée en amont côté Airtable), sans module Airtable en écriture.

**Destinataires.** Deux adresses sur le même e-mail : une adresse fixe pour la Direction (l'entreprise ne comptant qu'un seul dirigeant, même limitation assumée que pour le chargé d'affaires sur AUT-COM-002) et `chefChantierEmail`, résolue dynamiquement par chantier.

**Corps de l'e-mail.** Nom du chantier, client, budget initial, coût total réel, montant du dépassement (valeur absolue de `ecartBudget` via la fonction Make `abs()`, pour l'affichage plutôt que le nombre négatif brut).

**Écritures Airtable.** Aucune — scénario de lecture et notification uniquement.

**Gestion des erreurs.** Route d'erreur sur le module Airtable du script (e-mail + directive Commit, politique standard depuis AUT-COM-001). Aucun error handler sur le module Gmail, cohérent avec les autres notifications du projet.

**Intégration avec le reste du système.** `EcartBudget` (champ Formule, non éditable) n'est écrit par aucune automatisation. Indépendant d'AUT-CHA-004/005 (déclencheur natif événementiel, pas de Schedule ni de champ de suivi partagé). Aucun conflit avec AUT-CHA-006, qui porte sur `Statut` (table Étape) et non sur les champs financiers du Chantier.

**Statut : Implémentée.**

### AUT-CHA-008 — Détail d'implémentation

**Besoin métier.** Notifier le chef de chantier, l'ensemble des artisans affectés aux étapes du chantier et la Direction lorsque le chef de chantier coche `PretADemarrer`, indiquant que la préparation (étapes, artisans, matériel) est terminée et que le chantier est prêt à démarrer.

**Choix d'architecture — notifier un nombre variable de destinataires.** Contrairement aux notifications précédentes du domaine (un artisan unique par étape sur AUT-CHA-005/006), cette automatisation doit adresser potentiellement plusieurs artisans, un par étape du chantier, avec des doublons possibles si un artisan intervient sur plusieurs étapes. Deux options ont été comparées : agréger nativement la liste dans Airtable et l'exploiter en un seul e-mail (retenue), ou éclater la liste côté Make avec un Iterator pour envoyer un e-mail personnalisé par artisan. La seconde a été écartée : le besoin exprimé est une notification générique ("le chantier est prêt à démarrer"), sans contenu différencié par artisan, ce qui rend l'Iterator une complexité Make non justifiée au regard du principe retenu au chapitre 5.3.

**Champs Airtable créés :**
- `EmailArtisan_ARTISAN_Etape` (table Étape, Recherche) : expose le champ `Adresse e-mail` de l'Artisan lié via `ARTISANT_Etape`. Nécessaire car le champ existant `ArtisanResponsable` expose `Collaborateur` (type Utilisateur), qui ne peut pas être converti en adresse e-mail par une formule d'agrégation — seul le nom d'affichage en résulte.
- `ArtisansEmails_ETAPES_Chantier` (table Chantier, Cumul) : agrège `EmailArtisan_ARTISAN_Etape` via `ETAPES_Chantier`, formule `ARRAYJOIN(ARRAYCOMPACT(ARRAYUNIQUE(values)), ", ")` — déduplique les artisans intervenant sur plusieurs étapes et élimine les valeurs vides des étapes sans artisan assigné, avant même que Make n'ait à traiter la donnée.

**Déclenchement.** Automatisation Airtable native, "Quand un enregistrement correspond aux conditions", table Chantier : `PretADemarrer = coché` ET `ChefChantierResponsable` non vide. Déclencheur transitionnel, sur le modèle d'AUT-CHA-007 : se réactive uniquement sur le passage non-coché → coché, sans nécessiter de champ de suivi `NotifieXXX` dédié.

**Garde `ChefChantierResponsable` non vide.** Même limitation assumée que sur AUT-CHA-004/007 : un chantier prêt à démarrer sans chef de chantier assigné n'est pas remonté, aucun destinataire de repli retenu.

**Saisies du script.** Six input variables, mappées directement sur le Chantier déclencheur : `recordId`, `chantierID` (`ChantierID`), `nomClient` (`Nom_CLIENT_Chantier`), `adresse` (Adresse du chantier), `chefChantierEmail` (`ChefChantierResponsable`, résolu directement en e-mail par le mapping des Saisies), `artisansEmails` (`ArtisansEmails_ETAPES_Chantier`).

**Déclenchement du webhook.** URL stockée dans un secret dédié (`MAKE_WEBHOOK_URL_CHA008`), récupérée via `input.secret()`, cohérent avec la politique retenue depuis AUT-COM-001.

**Architecture du scénario Make.** Volontairement minimale : Webhook → Gmail, sans module Airtable, sans traitement intermédiaire — même architecture qu'AUT-CHA-002/FAC-001/FAC-005.

**Destinataires.** To : `chefChantierEmail` et l'adresse fixe de la Direction (même adresse que sur AUT-CHA-007 et la route "blocage" d'AUT-IA-001) — choix assumé de placer la Direction en destinataire principal plutôt qu'en copie, la notification de démarrage étant jugée suffisamment importante pour ne pas être reléguée en CC. CC : `artisansEmails`, résolu dynamiquement via la formule Make `split(artisansEmails, ", ")` appliquée en mode Map, plutôt que des slots de destinataires individuels — nécessaire puisque `artisansEmails` contient un nombre variable d'adresses concaténées en une seule chaîne, incompatible avec le format "une adresse par slot" attendu par les champs de destinataires classiques du module Gmail.

**Point de vigilance résolu en test — champ CC vide.** Un chantier sans aucune étape affectée à un artisan produit un `artisansEmails` vide ; `split("", ", ")` produit alors un tableau vide plutôt qu'un tableau contenant une chaîne vide, ce qui n'entrave pas l'envoi. Confirmé fonctionnel en test.

**Corps de l'e-mail.** Nom du chantier, client (en gras), adresse du chantier (en gras), suivi d'un lien vers la fiche du chantier dans l'interface Airtable (construit à partir de `recordId`).

**Écritures Airtable.** Aucune — scénario de lecture et notification uniquement, cohérent avec AUT-CHA-002/004/005/007.

**Gestion des erreurs.** Route d'erreur sur le module Airtable du script (e-mail + directive Commit, politique standard depuis AUT-COM-001). Aucun error handler sur le module Gmail, cohérent avec le reste du projet.

**Intégration avec le reste du système.** Aucune automatisation existante n'écrit sur `PretADemarrer`, `ArtisansEmails_ETAPES_Chantier` ou `EmailArtisan_ARTISAN_Etape`. Indépendant d'AUT-CHA-002 (déclencheur distinct : création du Chantier, et non passage à `PretADemarrer`).

**Statut : Implémentée.**

---

## 9.4 Domaine métier — Gestion documentaire

### Objectif

Centraliser et organiser automatiquement les documents liés aux chantiers.

### Automatisations prévues

| Référence | Processus automatisé | Déclencheur | Statut |
|------------|----------------------|-------------|---------|
| AUT-DOC-001 | Création automatique du dossier Google Drive d'un chantier | Nouveau chantier | Abandonnée |
| AUT-DOC-002 | Classement automatique des documents | Nouveau document | Abandonnée |
| AUT-DOC-003 | Renommage automatique des fichiers | Nouveau document | Abandonnée |

**Note sur le domaine Documents.** Les trois automatisations prévues initialement (AUT-DOC-001, 002, 003) ont été abandonnées après confrontation avec le texte exact du cahier des charges. Celui-ci ne demande que le "stockage et consultation des documents et photos liés aux chantiers" — une exigence de données, sans mention de Google Drive, de classement ou de renommage automatique. Ce domaine, tel que planifié initialement, découlait d'un choix technique (Google Drive comme solution de stockage, cf. README_NEOBATI.md) posé avant vérification que le besoin réel était déjà satisfait nativement :

- Le stockage et la consultation sont entièrement couverts par la table **Document chantier** (cf. 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md, section 3.11), avec pièces jointes natives Airtable.
- Le classement documentaire est déjà assuré nativement par les champs `Type`, `Catégorie` et `VisibleClient` de cette même table, sans automatisation.
- Créer un dossier Google Drive parallèle introduirait une seconde source de stockage documentaire à synchroniser, contraire aux principes retenus au chapitre 8 (8.1 : "les données restent stockées dans Airtable" ; 8.4 : "les services externes ne doivent jamais modifier directement la base Airtable").

Cette décision pourra être réexaminée si un besoin réel et non couvert apparaît ultérieurement (par exemple des volumes de fichiers dépassant les quotas de stockage Airtable, ou un besoin de consultation par des tiers sans accès à la base).

---

## 9.5 Domaine métier — Gestion de la facturation

### Objectif

Automatiser le suivi administratif et financier des chantiers.

### Automatisations prévues

| Référence | Processus automatisé | Déclencheur | Statut |
|------------|----------------------|-------------|---------|
| AUT-FAC-001 | Notification de facture d'acompte à établir | Nouveau chantier | Implémentée |
| AUT-FAC-002 | Relance automatique des factures impayées (IA) + notification interne à la première échéance dépassée | Quotidien (jours ouvrés, 10h00) | Implémentée |
| AUT-FAC-003 | Notification des échéances à venir | Exécution planifiée | Abandonnée |
| AUT-FAC-005 | Notification de facture de solde à établir | Chantier terminé | Implémentée |

**Note sur AUT-FAC-003.** Cette automatisation a été abandonnée après vérification du cahier des charges : celui-ci demande des relances pour les factures impayées et une détection du retard et des acomptes non reçus — exigences déjà intégralement couvertes par AUT-FAC-002 (relance client après échéance + alerte interne à la première échéance dépassée, cf. 9.5). Aucune exigence n'évoque de notification préventive avant échéance, ni vers le client ni en interne. Ajouter ce périmètre créerait une sollicitation redondante sans besoin métier démontré.

### AUT-FAC-001 — Détail d'implémentation

**Redéfinition du périmètre.** Le besoin initial ("Création automatique d'une facture") a été abandonné après cadrage (cf. section 9.7) : le formulaire "Créer une facture", accessible depuis la page "Chantiers à facturer", et les champs Lookup/Formula déjà natifs (Chantier, Client, TTC) couvrent intégralement ce besoin. Décider quand et pour quel montant émettre une facture reste un jugement métier de l'assistante de direction, non déductible d'une règle déterministe — un constat de même nature que celui ayant justifié l'abandon d'AUT-CHA-001.

Un besoin réel a néanmoins été identifié lors du cadrage : notifier l'assistante de direction à la création d'un chantier, pour l'inviter à établir une facture d'acompte. AUT-FAC-001 a été redéfinie sur ce périmètre.

**Besoin métier.** Informer l'assistante de direction dès qu'un chantier est créé, avec un montant d'acompte suggéré, afin de réduire le délai d'émission de la facture d'acompte.

**Champ Airtable créé — `MontantAcompteSuggere`** (Formula, table Chantier) : `{MontantHTDevis} * 0.3`. Le taux (30%) est ainsi lisible et modifiable directement dans le schéma plutôt qu'enfoui dans un scénario Make, conformément au principe retenu depuis le début du projet (Airtable avant Make lorsqu'une fonctionnalité native suffit, cf. chapitre 5.3 et 7.5).

**Déclenchement.** Une seconde automatisation Airtable native sur "Chantier créé", indépendante de celle d'AUT-CHA-002 — même schéma que la coexistence AUT-COM-001/AUT-COM-002 sur un déclencheur commun, conformément au principe de responsabilité unique (chapitre 8.1). Un script dédié envoie un webhook POST vers un scénario Make distinct, via un secret dédié (`MAKE_WEBHOOK_URL_FAC001`).

**Saisies du script.** Cinq input variables, mappées directement sur des champs du Chantier déclencheur :
- `recordId` (Record ID)
- `ChantierID` (champ composite lisible, ex. "CHANT-7-Aménagement bureaux Atelier Bois & Design")
- `nomClient` (`Nom_CLIENT_Chantier`, champ Lookup)
- `montantHTDevis` (`MontantHTDevis`, Lookup vers le Devis d'origine)
- `montantAcompteSuggere` (`MontantAcompteSuggere`, Formula)

Le Record ID est conservé dans le payload (`recordID`) bien que non affiché dans l'e-mail, pour rester disponible en cas de besoin futur (ex. écriture d'un indicateur "acompte notifié" sur le Chantier) — l'identifiant lisible `ChantierID`, distinct du Record ID, est celui utilisé pour l'affichage.

**Architecture du scénario Make.** Volontairement minimale, sur le modèle d'AUT-CHA-002 et AUT-COM-002 : Webhook → Gmail, sans module Airtable, sans traitement intermédiaire.

**Destinataire — limitation assumée.** Adresse fixe, l'entreprise ne comptant qu'une seule assistante de direction à ce stade, cohérent avec le traitement retenu pour le chargé d'affaires unique (AUT-COM-002) et le chef de chantier unique (AUT-CHA-002).

**Corps de l'e-mail.** Nom du chantier (identifiant lisible), client, montant HT du devis, montant d'acompte suggéré (30% du HT), suivi d'un lien vers la page "Chantiers à facturer" et d'un rappel explicite que le montant reste une suggestion ajustable à la création de la facture.

**Gestion des erreurs.** Aucun error handler : le scénario ne lit ni n'écrit dans Airtable, un échec Gmail est non bloquant, cohérent avec la politique retenue sur AUT-CHA-002 et AUT-COM-002.

**Intégration avec le reste du système.** Deux automatisations Airtable natives coexistent désormais sur l'événement "Chantier créé" (AUT-CHA-002 et AUT-FAC-001), chacune indépendante, sans conflit — schéma déjà validé pour AUT-COM-001/002. Aucune écriture Airtable n'est réalisée par cette automatisation ; aucun risque d'interférence avec les champs déjà exploités par les autres automatisations du domaine Chantiers.

**Statut : Implémentée.**

### AUT-FAC-002 — Détail d'implémentation

**Besoin métier.** Relancer automatiquement les clients dont une facture reste impayée au-delà de l'échéance, jusqu'à ce que le règlement soit intégral, avec un e-mail rédigé par IA dont le registre se durcit progressivement selon le nombre de relances déjà effectuées — sans plafond de relance, contrairement à AUT-COM-003, une facture impayée ayant un impact direct et continu sur la trésorerie.

**Choix d'architecture.** Un scénario Make à route unique, sans Router : contrairement à AUT-COM-003 (relance + expiration), AUT-FAC-002 n'a qu'un seul processus métier, aucun équivalent "expiration" n'existant pour une facture.

**Prérequis — fiabilisation du champ `Statut`.** Le champ `Statut` de la table Facture était initialement une Sélection unique manuelle, alors que 00_ affirmait à tort qu'il était calculé automatiquement selon l'échéance. Ce point a été corrigé en amont de la construction de l'automatisation : `Statut` est désormais un champ Formule, s'appuyant sur les champs déjà calculés `StatutPaiement` et `JoursRetardFac` plutôt que de dupliquer leur logique :

```
IF(
  {Annulee}, "Annulée",
  IF(
    {JoursRetardFac} > 0,
    IF({StatutPaiement} = "Partiellement payée", "En retard : partiellement payée", "En retard : impayée"),
    IF({StatutPaiement} = "Payée", "Payée",
      IF({StatutPaiement} = "Partiellement payée", "Partiellement payée", "Émise")
    )
  )
)
```

Un champ `Annulee` (Case à cocher) a été créé en complément : l'annulation d'une facture est une décision humaine non déductible des données (même constat que celui ayant justifié l'abandon d'AUT-CHA-001), et reste donc la seule entrée manuelle de ce dispositif, isolée dans un champ minimal plutôt que dispersée dans une sélection libre. L'état "Créé" de l'ancien champ a été retiré : une facture est toujours émise le jour même de sa création (`DateEmission` est systématiquement renseignée dès la création via le formulaire), rendant cet état sans cas d'usage réel.

**Champs Airtable créés ou modifiés sur la table Facture, préalables à AUT-FAC-002 :**
- `NombreRelances` (Number, défaut 0) — compteur, sans plafond, pilote uniquement le palier de ton du message IA.
- `Statut` (converti de Sélection unique vers Formule, cf. ci-dessus).
- `Annulee` (Case à cocher, nouveau).
- `ResteAEncaisserTTC` (Formule : `{ResteAEncaisserHT} * (1 + {TVA})`) — utilisé dans l'e-mail de relance client, un client réglant un montant TTC et non HT.

**Champ d'éligibilité — `FacARelancer`** (Formule) :

```
AND(
  {Statut} != "Annulée",
  {ResteAEncaisserHT} > 0,
  OR(
    AND({DateDerniereRelance} = BLANK(), TODAY() > {DateEcheance}),
    AND({DateDerniereRelance} != BLANK(), DATETIME_DIFF(TODAY(), {DateDerniereRelance}, 'days') >= 15)
  )
)
```

Relance dès le jour du dépassement d'échéance, puis tous les 15 jours, sans limite de nombre tant que `ResteAEncaisserHT > 0`. Une vue "Factures à relancer", filtrée sur `FacARelancer = true`, porte l'intégralité de la logique d'éligibilité — aucune formule dupliquée côté Make (7.5).

**Déclencheur.** Module Schedule, jours ouvrés (lundi-vendredi), 10h00, Europe/Paris — même fenêtre quotidienne que les autres cycles de relance du système (AUT-COM-003).

**Modules Make, dans l'ordre :**
1. Schedule.
2. Airtable — Search Records (table Facture, vue "Factures à relancer", limite portée à 30).
3. Filtre de garde `ID → Exists` (pattern 4.7).
4. OpenAI — Create a Chat Completion, `gpt-4.1-mini-2025-04-14`, rédaction du corps uniquement, différenciation de ton par instruction dédiée selon `NombreRelances` (0 / 1 / 2 et plus — au-delà de 2, le registre reste stable, aucune escalade supplémentaire dans le texte, contrairement à AUT-COM-003 où le palier maximal annonçait une clôture de dossier inapplicable ici en l'absence de plafond).
5. Filtre de garde `Result → Exists` (pattern AUT-COM-003).
6. Mise en forme HTML du corps généré : `replace(replace(Result; newline; " "); ". "; ".<br>")`, sans aucun guillemet (piège déjà documenté en 4.7/AUT-COM-003).
7. Gmail — envoi au client (destinataire et nom via les champs Lookup `Email_CLIENT_Facture` et `Nom_CLIENT_Facture`), corps intégrant `ResteAEncaisserTTC` et `JoursRetardFac` en clair, hors texte généré par le modèle.
8. Airtable — Update a Record : incrémente `NombreRelances`, met à jour `DateDerniereRelance` à la date du jour.
9. Filtre `NombreRelances = 5` (valeur après incrémentation, égalité stricte pour ne déclencher l'alerte qu'une seule fois dans le cycle de vie de la facture).
10. Gmail — alerte interne au collaborateur désigné (champ `Collaborateur`, par défaut l'assistante de direction), mentionnant `ResteAEncaisserTTC`.

**Enrichissement — notification interne à la première échéance dépassée.** Le besoin initialement prévu sous AUT-FAC-004 ("alerte acomptes non reçus") a été réexaminé et absorbé dans AUT-FAC-002 plutôt que construit comme automatisation distincte : `NombreRelances = 0` combiné à la présence dans la vue "Factures à relancer" identifie exactement le moment où une facture bascule pour la première fois en retard, avant toute relance — signal déjà disponible sans nouveau champ. Le périmètre a également été élargi à l'ensemble des factures (Acompte et Solde), et non aux seules factures d'acompte, une facture de solde impayée méritant le même signalement.

Un Router a été ajouté juste après le module de recherche (en aval du filtre de garde `ID → Exists`, qui protège ainsi les deux routes simultanément) :
- **Route 1** (inchangée) : rédaction IA → envoi au client → mise à jour du compteur → alerte à 5 relances.
- **Route 2** (nouvelle) : filtre `NombreRelances = 0` → Gmail, alerte interne au collaborateur désigné, signalant l'échéance dépassée avec le type de facture et le reste à encaisser TTC. Notification templatée, sans module IA, une information factuelle interne n'apportant aucune valeur à une rédaction générée (5.3).

Les deux e-mails (relance client et alerte interne) sont envoyés dans la même exécution, sans interférence entre les deux routes.

**Rédaction assistée par IA.** Même architecture qu'AUT-COM-003 : le modèle ne génère que le corps rédactionnel, jamais les montants ni les dates (ajoutés séparément par le template, principe du chapitre 5.3). Le prompt système interdit explicitement toute formulation à portée juridique (mise en demeure, poursuites, pénalités) à tous les paliers, y compris au registre le plus ferme — contrainte ajoutée spécifiquement pour cette automatisation après validation explicite, l'enjeu financier d'une facture étant distinct de celui d'un devis sans réponse.

**Gestion des erreurs.** Chaque module Airtable (Search Records, Update Record) et le module OpenAI disposent d'une route d'erreur dédiée — notification + Commit, cohérent avec la politique du projet. Un échec du module IA laisse la facture éligible au cycle suivant.

**Nommage des modules et error handlers — complément.** Les modules ont été explicitement nommés (Déclenchement quotidien, Récupération des factures à relancer, Rédaction du message de relance, Envoi de la relance au client, Mise à jour du compteur de relance, Alerte interne — 5 relances atteintes), conformément au principe retenu en 6.10 privilégiant le vocabulaire métier.

**Bug corrigé en cours de construction.** Le mapping de `DateDerniereRelance` avait été omis dans une première version du module Update a Record — seul `NombreRelances` était mis à jour. Conséquence : la condition `{DateDerniereRelance} = BLANK()` de `FacARelancer` restait indéfiniment vraie après le premier dépassement d'échéance, provoquant une relance quotidienne au lieu d'un cycle de 15 jours. Corrigé par l'ajout du mapping `DateDerniereRelance = now`.

**Point de vigilance — absence de plafond.** Contrairement à AUT-COM-003, aucune limite n'arrête le cycle de relance : celui-ci se poursuit indéfiniment tant que `ResteAEncaisserHT > 0`. L'alerte à 5 relances est un signalement ponctuel et non bloquant, comportement demandé explicitement plutôt qu'un oubli.

**Point de vigilance — limite du Search Records.** La limite est fixée à 30 factures traitées par exécution. Au-delà, les factures excédentaires seraient reportées silencieusement au cycle suivant, sans erreur levée. Seuil jugé large au regard du volume actuel de l'entreprise, à réévaluer si l'activité croît significativement.

**Historisation de la relance (ajout).** Après l'envoi confirmé de l'e-mail de relance au client (Route 1 uniquement), un module Airtable Create a Record crée un enregistrement dans la table `Interaction client` (cf. 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md, section 3.12) : type « Relance facture », client et facture concernés, contenu du message envoyé, date, numéro de relance. La Route 2 (alerte interne à l'assistante à `NombreRelances = 0`) n'écrit pas dans cette table, cette notification ne constituant pas une interaction avec le client. Une route d'erreur dédiée (e-mail de notification + Commit) couvre ce module, selon la convention retenue sur l'ensemble du scénario.

**Statut : Implémentée.**

### AUT-FAC-005 — Détail d'implémentation

**Besoin métier.** Notifier l'assistante de direction, symétriquement à AUT-FAC-001, lorsqu'un chantier se termine et qu'un solde reste à facturer, avec le montant restant suggéré.

**Déclenchement — différence architecturale avec AUT-FAC-001.** Contrairement à AUT-FAC-001 (déclenché à la création du Chantier, événement unique et sans ambiguïté), AUT-FAC-005 repose sur une transition d'état : `StatutChantier = "Terminé"`. L'automatisation Airtable native utilisée est donc de type "Lorsqu'une entrée correspond aux conditions" (et non "Quand un enregistrement est créé"), avec une double condition :

```
StatutChantier = "Terminé"
ResteAFactureHT > 0
```

Le second critère (`ResteAFactureHT`, champ Formule : `MontantHTDevis - {MontantFactureHT}`) évite de notifier un chantier déjà entièrement soldé, et réduit le risque de notification répétée : une fois la facture de solde émise, `ResteAFactureHT` retombe à 0 et la condition cesse d'être vraie.

**Point de vigilance.** `StatutChantier` étant un champ Formule dérivé des Étapes liées, une réouverture d'étape après clôture puis reclôture pourrait théoriquement provoquer une seconde transition vers "Terminé" et donc une seconde notification. Cas jugé rare, non traité par un garde-fou supplémentaire à ce stade — à surveiller en usage réel.

**Script de déclenchement.** Quatre input variables mappées sur le Chantier déclencheur : `recordId`, `ChantierID`, `nomClient` (Lookup), `resteAFactureHT`. Envoi via webhook POST, secret dédié `MAKE_WEBHOOK_URL_FAC005`.

**Scénario Make.** "Facture — Notifier solde à établir" : Webhook → Gmail, minimal, sans module Airtable — même architecture qu'AUT-FAC-001.

**Destinataire.** Adresse fixe de l'assistante de direction, identique à AUT-FAC-001.

**Contenu de l'e-mail.** Nom du chantier, client, montant HT restant à facturer, lien vers la page "Chantiers à facturer".

**Gestion des erreurs.** Aucun error handler — pas de lecture ni d'écriture Airtable en aval, un échec Gmail reste non bloquant, cohérent avec AUT-FAC-001.

**Statut : Implémentée.**

---

## 9.6 Domaine métier — Assistance intelligente

### Objectif

Exploiter l'intelligence artificielle pour assister les utilisateurs dans les tâches nécessitant une analyse ou une génération de contenu.

### Automatisations prévues

| Référence | Processus automatisé | Déclencheur | Statut |
|------------|----------------------|-------------|---------|
| AUT-IA-001 | Résumé automatique d'un rapport terrain, suggestion de points de suivi et alerte de blocage | Nouveau rapport | Implémentée |
| AUT-IA-002 | Génération d'une réponse à une demande de devis | Nouvelle demande | Abandonnée |
| AUT-IA-003 | Classification automatique des documents | Nouveau document | Abandonnée |
| AUT-IA-004 | Génération d'un compte rendu synthétique de chantier | Fin de chantier | Abandonnée |

**Note sur le domaine Assistance intelligente.** Trois des quatre automatisations prévues initialement (AUT-IA-002, 003, 004) ont été abandonnées après confrontation avec le texte exact du cahier des charges. Celui-ci ne formule que trois exigences en matière d'IA : le résumé automatique des notes de visite ou des échanges terrain, la rédaction assistée des relances clients, et la suggestion de points de suivi à intégrer dans les comptes rendus. Aucune des trois automatisations abandonnées ne correspond à l'une de ces exigences.

**AUT-IA-002 — Génération d'une réponse à une demande de devis.** Non demandée par le cahier des charges, ni dans la section IA, ni dans la section Automatisations. Le cadrage a établi qu'une telle réponse ne peut être que de deux natures, toutes deux inadaptées : soit un accusé de réception, dont le contenu strictement templaté ne tire aucune valeur d'une rédaction générée (principe du chapitre 5.3, déjà appliqué à la route de notification interne d'AUT-FAC-002) ; soit une réponse commerciale engageante (chiffrage, délais, faisabilité), qui relève du jugement du chargé d'affaires et non d'un traitement automatisable — même constat que celui ayant justifié l'abandon d'AUT-CHA-001 et de la version initiale d'AUT-FAC-001. Si un accusé de réception au client s'avérait souhaitable ultérieurement, il devrait être construit comme automatisation templatée du domaine Commercial, sans module IA.

**AUT-IA-003 — Classification automatique des documents.** Non demandée par le cahier des charges, qui n'exige que le "stockage et la consultation des documents et photos liés aux chantiers". Le besoin est par ailleurs déjà couvert nativement par les champs `Type`, `Catégorie` et `VisibleClient` de la table Document chantier. Cette automatisation constitue en outre un doublon d'AUT-DOC-002 ("Classement automatique des documents", même déclencheur), déjà abandonnée pour cette même raison en section 9.4 — le plan initial des 18 automatisations comportait donc un doublon inter-domaines non détecté à sa rédaction.

**AUT-IA-004 — Génération d'un compte rendu synthétique de chantier.** Non demandée telle que définie. Le cahier des charges demande la "suggestion de points de suivi à intégrer dans les comptes rendus" — une assistance à la rédaction, et non la génération autonome d'un livrable. Deux obstacles supplémentaires ont été relevés au cadrage : aucune entité "compte rendu de chantier" n'existe dans la base (les comptes rendus existants sont les Rapports terrain), et aucune interface décrite dans 01_ n'en prévoit la consultation ; par ailleurs le déclencheur "fin de chantier" désigne le moment où une synthèse a le moins de valeur opérationnelle, un chantier terminé n'appelant plus d'action. L'exigence réelle du cahier des charges est reprise par AUT-IA-005, cadrée sur le déclencheur pertinent (création d'un Rapport terrain).

### AUT-IA-001 — Détail d'implémentation

**Besoin métier.** Trois exigences liées, rattachées au même déclencheur (création d'un Rapport terrain) : générer un résumé automatique du rapport via IA, conformément à l'exigence du cahier des charges ("résumé automatique des notes de visite ou des échanges terrain") ; suggérer les points de suivi à ne pas oublier, conformément à l'exigence "suggestion de points de suivi à intégrer dans les comptes rendus" ; et notifier le chef de chantier et la Direction lorsqu'un problème bloquant est signalé. Le volet blocage était initialement rattaché à AUT-CHA-006 (cf. note de section 9.7) — retiré de ce périmètre après cadrage, car reposant sur un déclencheur distinct. Le volet points de suivi a d'abord été cadré sous une référence propre (AUT-IA-005) avant d'être absorbé ici : le cadrage a établi qu'il partageait avec le résumé le même déclencheur, le même périmètre (tous les rapports), le même destinataire (le chef de chantier) et le même canal. Deux scénarios distincts auraient produit deux e-mails simultanés au même destinataire pour un même rapport ; la contrainte d'un e-mail unique rend la fusion structurelle et non optionnelle.

**Choix d'architecture.** Un scénario Make à déclencheur unique et Router, sur le modèle d'AUT-FAC-002 : un seul processus métier ("traiter un rapport terrain"), deux traitements qui en découlent selon la présence d'un problème bloquant, plutôt que deux automatisations indépendantes dupliquant l'événement racine.

**Champs Airtable créés sur la table Rapport terrain :**
- `ResumeIA` (Texte long) — stocke le résumé généré par le modèle, pour chaque rapport, indépendamment de la présence d'un blocage.
- `PointsSuiviIA` (Texte long) — stocke les points de suivi suggérés par le modèle, dans un champ distinct de `ResumeIA` : deux contenus de nature différente, consultables séparément (principe un champ = une donnée).
- `ChefChantierResponsable_CHANTIER_Rapport` (Recherche, source `ChefChantierResponsable` via le lien natif vers Chantier). Un seul niveau de Lookup suffit ici — contrairement à `ArtisanResponsable_Etape_successeur` (AUT-CHA-006), Rapport terrain étant directement lié à Chantier, aucun passage intermédiaire par Étape n'est nécessaire.

**Déclenchement.** Automatisation Airtable native, "Quand un enregistrement est créé", table Rapport terrain. Action "Exécuter le script" relaie les valeurs vers Make via un webhook POST, secret dédié `MAKE_WEBHOOK_URL_IA001`, cohérent avec la politique retenue depuis AUT-COM-001.

**Saisies du script.** Sept input variables : `recordId`, `descriptionIntervention` (`RapportTerrain`), `problemeBloquant` (`ProblemeBloquant`, Case à cocher), `descriptionProbleme` (`DescriptionProbleme`), `nomEtape` (`ETAPE_Rapport`), `nomChantier` (`CHANTIER_Rapport`), `chefChantierEmail` (`ChefChantierResponsable_CHANTIER_Rapport`, résolu directement en adresse e-mail, sans objet Collaborator imbriqué).

**Comportement observé — case à cocher non cochée.** `problemeBloquant` transmis au webhook vaut `empty` lorsque la case n'est pas cochée, jamais `false` littéral. Point de vigilance à connaître pour toute automatisation future exploitant un champ Case à cocher côté Make : une condition de filtre construite sur `= false` ne matcherait jamais ce cas.

**Modules Make, dans l'ordre :**
1. Réception du rapport terrain (Webhook).
2. Rédaction du résumé IA — OpenAI, Create a Chat Completion, `gpt-4.1-mini-2025-04-14`, 1000 tokens maximum (cohérent avec AUT-COM-003/FAC-002). Le prompt système impose un résumé factuel de 3 à 4 phrases, sans formule de politesse ni formatage Markdown, sans invention au-delà des informations fournies. Le message utilisateur transmet `descriptionIntervention` et, via un `if()` Make, `descriptionProbleme` si renseigné, sinon "Aucun" — aucun module conditionnel dédié nécessaire.
3. Rédaction des points de suivi IA — second module OpenAI, mêmes modèle et paramètres, mêmes entrées. Le prompt système impose 2 à 4 points maximum, un par ligne préfixée d'un tiret, formulés à l'infinitif ou à l'impératif, strictement ancrés dans le rapport, sans délai ni intervenant ni montant inventé, et sans proposer d'action que le rapport décrit déjà comme réalisée.
4. Filtre de garde "Si résumé et points de suivi existent" — double condition `Result → Exists` en AND sur les deux modules IA.
5. Ajout du résumé et des points de suivi dans le rapport — Airtable Update a Record : `ResumeIA` et `PointsSuiviIA`. Seuls ces deux champs sont mappés, aucun autre champ du rapport n'est touché.
6. Répartition selon présence d'un problème bloquant — Router, deux routes construites sur `Exists`/`Does not exist` (et non `Equal to true`/`Is not equal to true`) : ce choix colle exactement au comportement observé sur la case à cocher non cochée, plus robuste qu'une comparaison booléenne stricte.

**Choix de deux modules IA plutôt qu'un seul.** Trois options ont été comparées : deux modules séquentiels ; un module unique produisant une réponse JSON structurée à parser côté Make ; un module unique produisant un texte continu contenant les deux blocs. La troisième a été écartée d'emblée — impossible de séparer les deux contenus pour les écrire dans deux champs distincts. La deuxième a été écartée malgré son appel API unique : elle impose un module Parse JSON supplémentaire, un prompt système portant deux consignes de fond, un risque de sortie non parsable, et le projet n'a aucun précédent de parsing JSON depuis un LLM. La première a été retenue : le surcoût d'un appel `gpt-4.1-mini` par rapport est négligeable au volume de l'entreprise, et le cahier des charges demande de suivre le coût d'exécution, non de le minimiser au détriment de la maintenabilité. En échange : aucun parsing, aucun risque de sortie malformée, et deux prompts ajustables séparément — l'expérience d'AUT-COM-003 ayant montré qu'un prompt se règle par itérations, deux consignes de fond dans un même système auraient rendu chaque itération plus risquée.

**Route "Rapport sans problème bloquant".** Gmail "Notification résumé - chef de chantier", destinataire `chefChantierEmail` seul. Corps : nom du chantier, nom de l'étape, résumé généré, points de suivi suggérés.

**Route "Rapport avec problème bloquant".** Gmail "Alerte problème bloquant - CDC et direction", destinataires `chefChantierEmail` + adresse fixe de la Direction (même adresse que sur AUT-CHA-007/FAC-001). Corps : résumé généré, suivi de la description brute du problème (`descriptionProbleme`), puis des points de suivi suggérés — ces derniers positionnés en dernier, le blocage primant dans la hiérarchie de lecture d'un e-mail d'alerte. Résumé et description brute figurent tous deux dans le même e-mail, la répétition étant volontaire : le résumé reste une reformulation synthétique, la description brute garantit qu'aucun détail signalé par l'artisan n'est perdu sur un point potentiellement sensible. Objet de cet e-mail préfixé d'un pictogramme d'alerte (⚠️), seule notification du projet à utiliser un tel préfixe visuel — choix assumé, dérogatoire à la convention d'objets neutres suivie sur le reste des automatisations.

**Écritures Airtable.** `ResumeIA` et `PointsSuiviIA` sur le rapport traité, avant le Router — un échec d'écriture bloque donc l'envoi des deux notifications possibles (contrairement à AUT-FAC-002, où le Router précède l'écriture). Choix assumé : garantit qu'un e-mail envoyé reflète toujours des champs à jour, au prix de bloquer les notifications en cas d'échec d'écriture.

**Gestion des erreurs.** Route d'erreur dédiée sur chacun des deux modules OpenAI ("Erreur - Rédaction du résumé IA", "Erreur - Rédaction des points de suivi IA") et sur le module Update a Record ("Erreur - Ajout du résumé dans le rapport") : notification par e-mail suivie de la directive Commit, cohérente avec la politique retenue depuis AUT-COM-001. Aucun error handler sur les modules Gmail, cohérent avec le reste du projet.

**Point de vigilance — absence de rejeu.** Contrairement à AUT-CHA-004/005/007 (déclencheur Schedule + vue Airtable, offrant un rattrapage automatique au cycle suivant), AUT-IA-001 repose sur un événement ponctuel sans mécanisme de reprise. Un échec (l'un des deux appels IA ou l'écriture Airtable) sur un rapport signalant un blocage n'est pas rejoué automatiquement ; le rapport reste consultable manuellement depuis l'interface Chef de chantier. Traitement uniforme assumé après cadrage explicite, malgré le risque plus élevé porté par la route "problème bloquant" sur ce point précis.

**Mise en forme des contenus générés.** Le résumé est restitué comme un bloc continu et découpé côté Make par `replace(replace(Result; newline; " "); ". "; ".<br>")`, formule identique à celle documentée sur AUT-COM-003. Les points de suivi sont produits par le prompt avec un retour à la ligne par point : un simple `replace(Result; newline; <br>)` suffit, sans le double `replace()`. Les deux formules s'écrivent sans aucun guillemet, conformément à la précision apportée en section 4.7.

**Intégration avec le reste du système.** Aucune automatisation existante n'écrit sur `ResumeIA` ni `PointsSuiviIA`. Indépendant d'AUT-CHA-006, recentré sur `Statut` d'Étape (cf. section 9.3) depuis le retrait du volet blocage de son périmètre. Cette automatisation couvre à elle seule deux des trois exigences IA du cahier des charges ; la troisième (rédaction assistée des relances clients) est couverte par AUT-COM-003 et AUT-FAC-002.

**Statut : Implémentée.**

### Décisions retenues

Pour NeoBati, les principes suivants sont retenus :

- Les automatisations sont organisées par domaine métier plutôt que par outil ou par technologie.
- Chaque domaine regroupe plusieurs processus poursuivant un même objectif fonctionnel.
- Chaque automatisation possède une responsabilité unique et clairement définie.
- Toute nouvelle automatisation devra être intégrée à cette cartographie avant son développement.
- Cette cartographie constitue la feuille de route des évolutions du projet et sera mise à jour au fur et à mesure de l'implémentation des nouvelles fonctionnalités.

## 9.7 Feuille de route de mise en conformité (cahier des charges)

Cette section documente l'écart identifié entre le plan initial des 18 automatisations et les exigences exactes du cahier des charges, ainsi que le plan de reprise convenu pour le combler.

### Automatisations à modifier/enrichir

| Référence | Modification nécessaire |
|---|---|
| AUT-COM-003 | Enrichir la relance devis avec une rédaction assistée par IA (actuellement templatée), conformément à l'exigence "Rédaction assistée des relances clients" — **Implémenté** |
| AUT-FAC-002 | Cadrage et construction terminés — module IA conçu dès le départ (pas en enrichissement a posteriori), sans plafond de relance à la différence d'AUT-COM-003 — **Implémenté** |

### Automatisations à cadrer avant construction

| Référence | Point à clarifier |
|---|---|
| AUT-FAC-001 | Cadrage terminé : besoin initial abandonné, redéfini en notification de facture d'acompte à la création d'un chantier — **Implémenté** |
| AUT-IA-001 | Cadrage terminé : résumé IA systématique + alerte de blocage au chef de chantier et à la Direction, un seul scénario avec Router sur le modèle d'AUT-FAC-002 — **Implémenté** |
| AUT-IA-005 | Cadrage terminé : besoin absorbé par AUT-IA-001 plutôt que construit séparément — **Absorbé** |

### Nouvelles automatisations identifiées

| Référence | Besoin couvert |
|---|---|
| AUT-CHA-006 | Notification changement de statut d'une étape (En cours / Terminée) — exigence explicite non couverte par le plan initial — **Implémenté** |
| AUT-CHA-007 | Alerte dépassement budgétaire — la donnée (écart budgétaire) existe déjà nativement, seule l'alerte manque — **Implémenté** |

**Note sur AUT-CHA-006.** Le périmètre initial associait à cette référence deux déclencheurs distincts : le changement de statut d'une Étape et le signalement d'un problème bloquant sur un Rapport terrain. Après cadrage, seul le premier a été retenu dans AUT-CHA-006 ; le second a été couvert par AUT-IA-001 (résumé automatique d'un rapport terrain et alerte de blocage), implémentée — cf. section 9.6 pour le détail d'implémentation, section 9.3 pour AUT-CHA-006.

### Automatisations abandonnées

| Référence | Besoin initial | Statut |
|---|---|---|
| AUT-FAC-003 | Notification des échéances à venir | Abandonnée |
| AUT-FAC-004 | Alerte acomptes non reçus | Abandonnée |
| AUT-IA-002 | Génération d'une réponse à une demande de devis | Abandonnée |
| AUT-IA-003 | Classification automatique des documents | Abandonnée |
| AUT-IA-004 | Génération d'un compte rendu synthétique de chantier | Abandonnée |

**Note sur AUT-FAC-003.** Cf. section 9.5 pour le détail — besoin non couvert par le cahier des charges, absorbé par AUT-FAC-002.

**Note sur AUT-FAC-004.** Le besoin a été absorbé par l'enrichissement d'AUT-FAC-002 plutôt que construit comme automatisation distincte : la route de notification interne à `NombreRelances = 0` couvre le même signalement, étendue à l'ensemble des factures (Acompte et Solde) plutôt qu'aux seules factures d'acompte. Le champ structuré "Acompte" initialement prévu comme préalable n'a plus lieu d'être créé, ce besoin étant couvert sans lui.

**Note sur AUT-IA-002, AUT-IA-003 et AUT-IA-004.** Cf. section 9.6 pour le détail des trois abandons — aucune n'était demandée par le cahier des charges. L'exigence "suggestion de points de suivi à intégrer dans les comptes rendus", seule exigence IA restée non couverte après ces abandons, a d'abord été ouverte sous la référence AUT-IA-005 plutôt que par une réinterprétation d'AUT-IA-004, dont le périmètre ne correspondait pas à ce besoin. Le cadrage d'AUT-IA-005 a ensuite conclu à son absorption par AUT-IA-001 : même déclencheur, même périmètre, même destinataire, même canal, et exigence d'un e-mail unique rendant deux scénarios distincts intenables. Aucune automatisation n'est construite sous cette référence, conservée comme trace du cadrage — même logique que l'absorption d'AUT-FAC-004 par AUT-FAC-002.

**Note sur le canal SMS.** Le cahier des charges mentionne le SMS à deux reprises, à des niveaux différents. Dans le contexte du projet (p.2), il apparaît comme un constat du désordre existant chez le client : « photos de chantier envoyées par SMS » y décrit une pratique actuelle à corriger, non une exigence de canal à reproduire. Dans les fonctionnalités attendues (section Automatisations), il apparaît entre parenthèses au sein d'une exigence de fond : « Génération de messages cohérents (emails, SMS) grâce à l'IA. » C'est cette seconde occurrence qui porte la question d'architecture ; la première ne fait que confirmer que le SMS existe dans le vocabulaire du projet, sans en faire une exigence de canal autonome. La lecture retenue est que l'exigence porte sur la cohérence des messages générés par IA, les canaux cités étant illustratifs du type de messages concernés — les exigences réellement formulées comme telles dans le document (« Notifications internes », « Relances clients automatiques ») sont explicites et indépendantes, sans jamais nommer le SMS comme un livrable à part. Le canal SMS n'est en conséquence pas implémenté. Cette décision est un écart assumé, pris après évaluation du coût et du risque, et non par évitement.

**Ce que l'ajout du canal impliquerait.** Quatre chantiers distincts, aucun marginal : un fournisseur tiers (Twilio, Vonage, Brevo ou équivalent), impliquant compte, moyen de paiement et gestion de crédits, alors que le projet n'a aujourd'hui aucune dépendance payante hors Make et OpenAI ; une décision de périmètre non tranchée (SMS doublonnant l'e-mail, intrusif, ou le remplaçant, avec perte du contenu détaillé) ; une conformité RGPD à construire, avec consentement et opt-out à recueillir avant tout envoi ; une refonte des prompts, un SMS tenant en 160 caractères là où les prompts actuels produisent trois à cinq phrases.

**Bénéfice métier évalué — argument central de la décision.** Les messages générés par IA dans ce système s'adressent tous à des **clients** : relances de devis (AUT-COM-003) et relances de factures (AUT-FAC-002). Un SMS à un client particulier suppose un consentement recueilli et un mécanisme d'opt-out — au minimum un champ de consentement sur la table Client et un filtre de garde sur chaque scénario concerné. Aucun de ces éléments n'existe, et leur absence constitue à elle seule un motif suffisant de ne pas ouvrir ce canal pour la relation client, indépendamment de toute autre considération.

Il existe par ailleurs deux automatisations du système qui notifient directement l'artisan (AUT-CHA-005, AUT-CHA-006) — un profil qui n'est pas toujours en accès e-mail sur chantier. Mais ces notifications sont **templatées**, sans module IA : elles ne relèvent pas de l'exigence « génération de messages cohérents par IA » examinée ici, qui ne concerne que les communications client. Le canal SMS pourrait présenter un intérêt pour ces notifications terrain — c'est un sujet distinct, hors du périmètre de l'exigence IA, qui pourrait être ouvert séparément s'il devenait prioritaire.

**Données disponibles.** Les numéros de téléphone existent déjà (`Telephone` sur les tables Client et Artisan) et resteraient exploitables sans modification structurelle si la décision devait être révisée. Aucune capacité d'émission n'existe en revanche : ni fournisseur, ni module SMS dans les scénarios Make, ni champ de consentement.

**Conditions de révision de cette décision.** Deux situations justifieraient de rouvrir le sujet pour la relation client : une exigence explicite du commanditaire ou du jury portant sur le canal lui-même ; la mise en place d'un mécanisme de consentement/opt-out rendant le SMS client viable en RGPD. Une notification artisan par SMS reste un sujet distinct, ouvrable indépendamment de cette décision.

### Ordre de reprise convenu

1. AUT-COM-003 (enrichissement IA)
2. AUT-FAC-001 (cadrage préalable)
3. AUT-FAC-002 (relance factures, avec IA dès la conception)
4. Champ Acompte + AUT-FAC-004  (abandonné, absorbé par AUT-FAC-002)
5. AUT-FAC-003 (abandonné — besoin déjà couvert par AUT-FAC-002)
6. AUT-CHA-006 — Implémentée
7. AUT-CHA-007 — Implémentée
8. AUT-IA-002 (abandonnée — non demandée par le cahier des charges)
9. AUT-IA-003 (abandonnée — redondante avec les champs natifs, doublon d'AUT-DOC-002)
10. AUT-IA-004 (abandonnée — périmètre non conforme à l'exigence réelle du cahier des charges)
11. AUT-IA-005 (absorbée par AUT-IA-001 — suggestion de points de suivi)
12. SMS (décision d'architecture — écart assumé, non implémenté)

### Évolution post-audit

| Référence | Besoin couvert |
|---|---|
| AUT-CHA-008 | Notification de démarrage du chantier (chef de chantier, artisans, Direction) à la case `PretADemarrer` — ajoutée après clôture de l'audit de conformité, sur le même raisonnement que l'ajout d'AUT-CHA-005 — **Implémenté** |

Cette section distingue les automatisations ajoutées après la clôture de l'audit de conformité (sections précédentes) de celles identifiées pendant l'audit lui-même, pour ne pas réécrire l'historique du processus de mise en conformité déjà mené.

13. AUT-CHA-008 (évolution post-audit — notification de démarrage de chantier)

# 10. Maintenance et évolutivité

Ce chapitre définit les bonnes pratiques permettant d'assurer la qualité, la stabilité et l'évolutivité du projet NeoBati.

L'objectif est de garantir qu'une évolution puisse être réalisée sans remettre en cause l'architecture existante.

Chaque modification du système doit privilégier la simplicité, la lisibilité et la maintenabilité.

---

## 10.1 Évolutivité

Le projet NeoBati a été conçu afin de pouvoir évoluer progressivement.

Toute nouvelle fonctionnalité devra respecter les principes suivants :

- préserver l'architecture existante ;
- limiter les impacts sur les autres composants ;
- privilégier les évolutions incrémentales ;
- éviter les modifications globales lorsqu'une évolution locale est suffisante.

Une évolution doit enrichir le système sans augmenter inutilement sa complexité.

---

## 10.2 Documentation

Toute évolution significative du projet doit être documentée.

La documentation constitue une partie intégrante du projet et doit évoluer au même rythme que celui-ci.

Les éléments suivants doivent être mis à jour lorsque cela est nécessaire :

- architecture de la base Airtable ;
- interfaces ;
- automatisations ;
- conventions techniques ;
- documentation utilisateur.

Une fonctionnalité non documentée est considérée comme incomplète.

---

## 10.3 Gestion des erreurs

Les automatisations doivent être conçues afin de gérer correctement les erreurs.

Les principes suivants sont recommandés :

- identifier clairement les erreurs ;
- éviter les blocages complets du processus ;
- prévoir des mécanismes de reprise lorsque cela est pertinent ;
- informer les utilisateurs lorsqu'une intervention est nécessaire.

Les erreurs ne doivent jamais être ignorées silencieusement.

---

## 10.4 Tests

Toute évolution importante doit être testée avant son déploiement.

Les tests doivent notamment vérifier :

- le bon fonctionnement des automatisations ;
- la cohérence des données ;
- le comportement des interfaces ;
- les cas d'erreur les plus courants.

Les modifications ne doivent être appliquées en production qu'après validation.

---

## 10.5 Performances

La simplicité reste le principal facteur de performance.

| Recommandation | Objectif |
|----------------|----------|
| Limiter les automatisations inutiles | Réduire les temps d'exécution et la maintenance. |
| Éviter les calculs redondants | Simplifier le modèle de données. |
| Supprimer les composants obsolètes | Conserver une architecture claire. |
| Privilégier les fonctionnalités natives d'Airtable | Réduire la dépendance aux automatisations. |
| Réutiliser les scénarios existants lorsque cela est pertinent | Éviter la duplication de logique métier. |

Une architecture simple est généralement plus performante et plus facile à maintenir.

---

## 10.6 Évolutions futures

Le projet a été conçu afin de pouvoir intégrer progressivement de nouvelles fonctionnalités.

Les principales pistes d'évolution identifiées sont les suivantes.

| Domaine | Évolution envisagée |
|----------|---------------------|
| Automatisations | Développement de nouveaux scénarios métier. |
| Intelligence artificielle | Enrichissement des traitements d'analyse et de génération. |
| Intégrations | Connexion à de nouveaux services externes. |
| Pilotage | Ajout de nouveaux indicateurs et tableaux de bord. |
| Processus métier | Optimisation continue des flux de travail. |

Ces évolutions devront respecter les conventions définies dans le présent guide.

### Décisions retenues

Pour NeoBati, les principes suivants sont retenus :

- Toute évolution doit préserver la cohérence globale de l'architecture.
- La documentation fait partie intégrante du projet et doit être maintenue à jour.
- Les nouvelles fonctionnalités sont développées de manière incrémentale.
- Les automatisations sont testées avant leur mise en production.
- La simplicité est privilégiée à la sophistication technique.
- Chaque évolution doit améliorer le système sans augmenter inutilement sa complexité.

 # 11. Check-list d'évolution du projet

Cette check-list constitue un outil d'aide à la décision avant toute évolution de NeoBati.

Son objectif est de garantir que chaque modification reste cohérente avec l'architecture définie dans ce guide et respecte les conventions du projet.

Elle peut être utilisée aussi bien avant la création d'une nouvelle fonctionnalité que lors de la modification d'un composant existant.

---

## 11.1 Avant de modifier la base Airtable

### Structure des données

- [ ] La nouvelle information représente-t-elle réellement une nouvelle donnée métier ?
- [ ] Un champ existant ne permet-il pas déjà de répondre au besoin ?
- [ ] Une relation entre tables serait-elle préférable à une duplication de données ?
- [ ] Une nouvelle table est-elle réellement nécessaire ?
- [ ] La granularité de la table est-elle cohérente ?

### Calculs

- [ ] Une formule Airtable permet-elle de répondre au besoin ?
- [ ] Un champ Lookup ou Rollup est-il suffisant ?
- [ ] Le calcul peut-il rester entièrement dans Airtable ?

### Cohérence

- [ ] Les conventions de nommage sont-elles respectées ?
- [ ] Les nouvelles relations sont-elles cohérentes avec le modèle de données ?
- [ ] Les modifications restent-elles compatibles avec les interfaces existantes ?

---

## 11.2 Avant de créer une automatisation

### Choix de la solution

- [ ] Une fonctionnalité native d'Airtable suffit-elle ?
- [ ] Une automatisation est-elle réellement nécessaire ?
- [ ] Le traitement doit-il être réalisé par Airtable ou par Make ?

### Architecture

- [ ] Le scénario possède-t-il une seule responsabilité métier ?
- [ ] Le scénario appartient-il au bon domaine métier ?
- [ ] Le scénario respecte-t-il l'architecture des automatisations définie dans ce guide ?

### Qualité

- [ ] Les erreurs sont-elles prises en compte ?
- [ ] Une journalisation est-elle nécessaire ?
- [ ] Les modules sont-ils clairement nommés ?
- [ ] Le scénario reste-t-il simple à maintenir ?

---

## 11.3 Avant d'utiliser un modèle d'intelligence artificielle

### Pertinence

- [ ] L'IA apporte-t-elle une réelle valeur ajoutée ?
- [ ] Le traitement pourrait-il être réalisé de manière déterministe ?

### Conception

- [ ] Le prompt est-il suffisamment précis ?
- [ ] Le format de sortie est-il clairement défini ?
- [ ] Une réponse au format JSON est-elle préférable ?

### Fiabilité

- [ ] Les données générées seront-elles validées avant d'être enregistrées ?
- [ ] Une stratégie est-elle prévue en cas de réponse invalide ou incomplète ?

---

## 11.4 Avant de créer une nouvelle interface ou un formulaire

### Expérience utilisateur

- [ ] L'utilisateur a-t-il réellement besoin d'une nouvelle interface ?
- [ ] Une interface existante pourrait-elle être enrichie ?
- [ ] Les informations affichées sont-elles adaptées au profil utilisateur ?

### Simplicité

- [ ] Les champs inutiles sont-ils masqués ?
- [ ] Le parcours utilisateur est-il clair ?
- [ ] Les actions proposées sont-elles limitées au besoin réel ?

---

## 11.5 Avant de terminer une évolution

### Validation

- [ ] Les tests fonctionnels ont-ils été réalisés ?
- [ ] Les cas d'erreur ont-ils été vérifiés ?
- [ ] Les données produites sont-elles cohérentes ?

### Documentation

- [ ] Les documents de référence ont-ils été mis à jour ?
- [ ] Les modifications sont-elles documentées ?
- [ ] Les nouvelles conventions éventuelles sont-elles décrites ?

### Architecture

- [ ] L'évolution respecte-t-elle les principes définis dans ce guide ?
- [ ] La solution retenue est-elle la plus simple répondant au besoin ?
- [ ] La nouvelle fonctionnalité reste-t-elle facilement maintenable ?
- [ ] L'architecture globale du projet demeure-t-elle cohérente ?

---

## Glossaire

| Terme                   | Définition                                      |
| ----------------------- | ----------------------------------------------- |
| Entité métier           | Concept représenté par une table                |
| Référentiel             | Source unique de vérité                         |
| Domaine métier          | Ensemble cohérent de processus                  |
| Table de liaison        | Table représentant une relation N:N             |
| Traitement déterministe | Traitement produisant toujours le même résultat |
| Orchestration           | Coordination de plusieurs traitements           |
| Interface               | Ensemble de pages Airtable destiné à un profil utilisateur |
| Processus métier        | Suite d'actions permettant d'atteindre un objectif fonctionnel |

# Conclusion

Le présent guide constitue la référence technique du projet **NeoBati**.

Il définit les principes d'architecture, les conventions de développement et les bonnes pratiques à respecter pour assurer la cohérence, la maintenabilité et l'évolutivité du système.

Ce document est complémentaire aux documents de contexte du projet :

- **00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md**, qui décrit l'architecture fonctionnelle de la base Airtable ;
- **01_CONTEXTE_INTERFACES_NEOBATI.md**, qui présente les interfaces, les formulaires et les parcours utilisateurs.

À chaque évolution du projet, les décisions techniques et les nouvelles conventions devront être intégrées à ce guide afin qu'il demeure la référence de développement de NeoBati.

Son objectif est de garantir que toute évolution future respecte une architecture claire, cohérente et pérenne, indépendamment des outils utilisés ou des personnes impliquées dans le développement du projet.