# 02_CONTEXTE_INTERFACES_NEOBATI

## Projet professionnel – NeoBati

Version : 1.0

---

# 1. Présentation du document

## Objectif

Ce document décrit l'organisation fonctionnelle des interfaces Airtable développées pour le projet **NeoBati**.

Il complète le document **00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md**, qui présente la structure de la base de données, en documentant la couche de présentation utilisée par les différents profils métiers.

Son objectif est de fournir une vision claire de l'architecture des interfaces, de leur rôle dans le système d'information et des principales interactions avec les données de la base Airtable.

Contrairement à une documentation utilisateur, ce document ne décrit pas chaque composant graphique en détail. Il constitue un document de contexte destiné à faciliter la compréhension globale du projet et à servir de référence lors des évolutions futures, notamment la création de formulaires, le développement d'automatisations Make et l'intégration de fonctionnalités basées sur l'intelligence artificielle.

---

# 2. Vue d'ensemble des interfaces

Les interfaces Airtable ont été organisées selon les responsabilités des différents métiers intervenant dans la gestion d'un chantier.

Chaque utilisateur accède uniquement aux informations nécessaires à son activité quotidienne. Cette organisation permet de simplifier la navigation, de limiter les risques d'erreur et de présenter des interfaces adaptées aux besoins opérationnels de chaque profil.

En complément des interfaces métiers, plusieurs interfaces transversales donnent accès à des registres communs permettant de consulter les chantiers, les clients et les documents de l'entreprise.

## 2.1 Cartographie des accès

| Interface | Utilisateur | Finalité |
|------------|-------------|----------|
| **Direction – Pilotage global** | Dirigeant | Suivre l'activité globale de l'entreprise à l'aide d'indicateurs stratégiques et d'une vision consolidée des chantiers. |
| **Administratif – Facturation & documents** | Assistante de direction | Gérer la facturation, les encaissements et les documents administratifs liés aux chantiers. |
| **Chargé d'affaires – Devis & suivi commercial** | Chargé d'affaires | Assurer le suivi des demandes de devis, des prospects et de la relation commerciale. |
| **Chefs de chantier – Planning & avancement** | Chefs de chantier | Planifier les chantiers, organiser les interventions et suivre l'avancement des travaux. |
| **Artisans – Mobile terrain** | Artisans | Consulter les interventions assignées, mettre à jour leur avancement et transmettre les informations terrain. |
| **Registre des chantiers** | Tous les utilisateurs | Consulter la liste complète des chantiers et leurs principales informations. |
| **Registre des clients** | Tous les utilisateurs | Consulter le registre centralisé des clients de l'entreprise. |
| **Documents & photos** | Tous les utilisateurs | Consulter les documents du projet et ajouter de nouveaux fichiers via un formulaire dédié. |

## 2.2 Organisation générale

L'ensemble des interfaces est organisé selon une logique métier.

Les interfaces principales sont réservées à un profil utilisateur unique et regroupent les fonctionnalités nécessaires à son activité. Les interfaces transversales sont quant à elles accessibles à l'ensemble des utilisateurs afin de faciliter la consultation de données communes sans multiplier les droits d'accès aux tables de la base Airtable.

Cette séparation entre interfaces métiers et interfaces de consultation contribue à améliorer l'expérience utilisateur tout en limitant les manipulations directes sur les données.

## 2.3 Philosophie de conception

Les interfaces ont été conçues selon le principe de séparation des responsabilités.

Chaque profil utilisateur dispose uniquement des fonctionnalités nécessaires à son activité quotidienne. Cette approche permet de limiter les erreurs de manipulation, de simplifier la navigation et de garantir que chaque utilisateur intervient uniquement sur les données dont il est responsable.

L'architecture distingue trois niveaux d'intervention :

| Niveau | Interfaces concernées | Finalité |
|--------|-----------------------|----------|
| Pilotage | Direction | Analyser les indicateurs et suivre la performance globale de l'entreprise. |
| Gestion | Administratif, Chargé d'affaires, Chefs de chantier | Réaliser les opérations quotidiennes liées à leur métier. |
| Exécution | Artisans | Mettre à jour les interventions réalisées sur le terrain. |

Les interfaces « Registre des chantiers », « Registre des clients » et « Documents & photos » constituent des espaces transversaux accessibles à l'ensemble des utilisateurs afin de faciliter la consultation de données communes.

## 2.4 Architecture fonctionnelle des interfaces

L'architecture des interfaces Airtable est organisée autour des différents métiers de l'entreprise.

Chaque profil utilisateur dispose d'une interface dédiée regroupant les fonctionnalités correspondant à ses responsabilités. Trois interfaces transversales complètent ce dispositif afin de permettre la consultation des informations communes à l'ensemble des collaborateurs.

Le schéma ci-dessous présente l'organisation générale des interfaces développées pour le projet NeoBati.

                              NeoBati
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        │                         │                         │
    Pilotage                  Gestion                 Consultation
        │                         │                         │
 ┌──────────────┐       ┌────────────────────┐      ┌───────────────────┐
 │ Direction    │       │ Administratif      │      │ Registre chantiers│
 └──────────────┘       ├────────────────────┤      ├───────────────────┤
                        │ Chargé d'affaires  │      │ Registre clients  │
                        ├────────────────────┤      ├───────────────────┤
                        │ Chef de chantier   │      │ Documents & photos│
                        └────────────────────┘      └───────────────────┘
                                  │
                           ┌──────────────┐
                           │ Artisans     │
                           └──────────────┘

# 3. Interface – Direction : Pilotage global

## Objectif

L'interface **Direction – Pilotage global** constitue l'espace de pilotage stratégique du dirigeant.

Elle centralise les principaux indicateurs de performance de l'entreprise afin de fournir une vision globale de l'activité sans nécessiter l'accès direct aux tables de la base Airtable.

Cette interface permet notamment de suivre la rentabilité, la facturation, l'avancement des chantiers ainsi que les principaux indicateurs commerciaux.

---

## Utilisateur concerné

- Dirigeant

Cette interface est exclusivement destinée au dirigeant. Aucun autre profil utilisateur n'y a accès.

---

## Organisation de l'interface

L'interface est composée de deux pages complémentaires.

| Page | Rôle |
|------|------|
| **Tableau de bord – Direction** | Vue synthétique de l'activité de l'entreprise à l'aide de KPI, graphiques et tableaux de suivi. |
| **Suivi détaillé des chantiers** | Consultation détaillée des informations relatives à chaque chantier. |

---

## Page : Tableau de bord – Direction

### Objectif

Cette page constitue le point d'entrée principal de l'interface.

Elle rassemble les indicateurs stratégiques nécessaires au suivi de l'activité et permet au dirigeant d'identifier rapidement les éléments nécessitant une attention particulière.

---

### Organisation

La page est structurée autour de quatre groupes fonctionnels.

| Groupe | Objectif |
|---------|----------|
| **Suivi financier** | Visualiser les principaux indicateurs financiers de l'entreprise. |
| **Suivi des factures** | Contrôler les encaissements, les retards de paiement et le montant restant à facturer. |
| **Suivi opérationnel** | Mesurer l'avancement des chantiers et identifier les projets en retard. |
| **Clients clés** | Identifier les clients générant le plus de chiffre d'affaires. |

Chaque groupe présente une vue synthétique des données et permet d'accéder rapidement aux informations concernées.

#### Inventaire du groupe Suivi financier

- KPI « Chiffre d'affaires HT facturé » (Somme sur `MontantFactureHT`).
- KPI « Chiffre d'affaires HT encaissé » (Somme sur `PaiementRecuHT`).
- KPI « Montant HT restant à facturer » (Somme sur `ResteAFactureHT`).
- KPI « Marge brute prévisionnelle HT » (Somme sur `MargeBrutPrevisionnelleHT`).
- KPI « Marge moyenne prévisionnelle HT par chantier » (Moyenne sur `MargeBrutPrevisionnelleHT`).
- KPI « Taux de marge prévisionnel moyen HT » (Moyenne sur `TauxMargePrevisionnelleHT`).
- KPI « Taux prévisionnel de chantiers déficitaires » (Moyenne sur `ChantierDeficitaire`, mise en forme Pourcentage).
- Graphique « Rentabilité prévisionnelle des chantiers » : comparaison, par chantier, de la marge brute prévisionnelle (`MargeBrutPrevisionnelleHT`), triée par valeur décroissante. Couvre l'indicateur « Top 5 des chantiers par marge » de l'annexe du cahier des charges, sur l'ensemble du portefeuille plutôt que sur les cinq premiers seulement.
- Graphique « Comparaison des coûts MO / Achats » : pour chaque chantier, deux séries juxtaposées (Somme `CoutTotalArtisan`, Somme `CoutMateriel`). Ce graphique répond à l'esprit de l'indicateur « Répartition coûts MO/achats » de l'annexe, sous une forme comparative plutôt qu'un pourcentage consolidé unique — ce dernier ayant été écarté après évaluation, la variation entre chantiers apportant davantage de valeur de pilotage qu'un ratio moyen portefeuille.

Les KPI de marge prévisionnelle et de taux de déficitaires reposent sur `MargeBrutPrevisionnelleHT` plutôt que sur `MargeBrutHT` : cette dernière reste vide pour tout chantier non encore facturé (cf. 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md, section 3.4), ce qui exclurait ces chantiers des indicateurs consolidés au moment où ils sont le plus utile de les surveiller.

#### Inventaire du groupe Suivi opérationnel

- KPI « Chantiers en cours » (comptage filtré sur le statut).
- KPI « Chantiers en retard » (comptage filtré sur `EnRetard`).
- KPI « Coût total des chantiers » (Somme sur `CoutTotalChantier`).
- KPI « Trésorerie nette » (Somme sur `TresorerieNette`).
- Tableau « Avancement des chantiers en cours » : ChantierID, Client, Avancement (%), Facturation (%), Montant facturé HT, Reste à facturer HT — pour les chantiers au statut « En cours ».
- Filtres disponibles : Date de démarrage, Statut du chantier.

#### Inventaire du groupe Clients clés

- Tableau « Top clients » : Nom, Type, Statut, Chantier(s) lié(s), Nombre de chantiers, Factures liées, CA HT Total — trié par CA HT Total décroissant.

---

### Sources de données

Cette page exploite principalement les informations issues des tables suivantes :

- Chantier
- Facture
- Client
- Devis

Les indicateurs sont calculés directement à partir des données présentes dans ces tables.

---

### Interactions

Cette page est exclusivement destinée à la consultation.

Aucun enregistrement ne peut être créé, modifié ou supprimé depuis cette interface.

---

## Page : Suivi détaillé des chantiers

### Objectif

Cette page permet au dirigeant de consulter l'ensemble des informations relatives à un chantier donné.

Elle complète le tableau de bord en offrant une vision détaillée de chaque projet.

---

### Informations consultables

Pour chaque chantier, le dirigeant peut consulter notamment :

- les informations générales du chantier ;
- le client associé ;
- le devis accepté ;
- les étapes de réalisation ;
- les artisans affectés ;
- les documents du chantier ;
- les factures émises ;
- l'avancement global ;
- les principaux indicateurs financiers.

---

### Sources de données

Cette page repose principalement sur la table **Chantier** et exploite les relations avec les tables :

- Client
- Devis
- Étape
- Artisan
- Facture
- Document chantier

---

### Interactions

Cette page est destinée uniquement à la consultation.

Aucune modification directe des données n'est réalisée depuis cette interface.

---

## Interactions avec la base Airtable

### Tables consultées

- Client
- Devis
- Chantier
- Étape
- Artisan
- Facture
- Document chantier

### Tables modifiées

Aucune.

### Formulaires utilisés

Aucun.

---

## Rôle dans le système

Cette interface constitue le principal outil d'aide à la décision du dirigeant.

Elle permet de suivre simultanément les dimensions financière, commerciale et opérationnelle de l'entreprise tout en limitant les manipulations directes dans les tables Airtable.

# 4. Interface – Administratif : Facturation & documents

## Objectif

L'interface **Administratif – Facturation & documents** est dédiée à la gestion administrative et financière de l'entreprise.

Elle permet à l'assistante de direction de suivre la facturation des chantiers, de contrôler les paiements, d'identifier les chantiers nécessitant une nouvelle facture et de gérer les documents administratifs associés aux projets.

Cette interface centralise l'ensemble des tâches administratives afin de limiter les manipulations dans les tables de la base Airtable.

---

## Utilisateur concerné

- Assistante de direction

Cette interface est exclusivement réservée à ce profil utilisateur.

---

## Organisation de l'interface

L'interface est composée de quatre pages complémentaires.

| Page | Rôle |
|------|------|
| **Tableau de bord – Administratif** | Vue synthétique de la situation administrative et financière de l'entreprise. |
| **Suivi des factures** | Contrôle des encaissements, des retards de paiement et des factures restant à percevoir. |
| **Chantiers à facturer** | Préparation de la facturation des chantiers et création des nouvelles factures. |
| **Documents administratifs** | Consultation des documents liés aux chantiers et aux clients. |

---

## Page : Tableau de bord – Administratif

### Objectif

Cette page regroupe les principaux indicateurs utiles au suivi administratif quotidien.

Elle permet de visualiser rapidement les montants restant à encaisser, les factures en retard ainsi que plusieurs indicateurs liés à l'avancement des chantiers.

---

### Sources de données

Cette page exploite principalement les données issues des tables :

- Facture
- Chantier
- Client

Les informations sont présentées sous forme d'indicateurs et de tableaux de synthèse.

---

### Interactions

Cette page est destinée uniquement à la consultation.

Aucun enregistrement ne peut être créé ou modifié.

---

## Page : Suivi des factures

### Objectif

Cette page permet d'assurer le suivi des factures émises et des paiements reçus.

Elle facilite l'identification des factures en attente d'encaissement ainsi que des retards de règlement afin d'anticiper les actions de relance.

---

### Informations consultables

L'assistante de direction peut notamment consulter :

- les factures restant à encaisser ;
- les factures en retard ;
- le montant restant à percevoir ;
- le statut de paiement de chaque facture ;
- les principaux indicateurs opérationnels associés aux chantiers.

---

### Sources de données

- Facture
- Chantier
- Client

---

### Interactions

Cette page est exclusivement dédiée au suivi.

Les modifications des factures sont réalisées directement dans leur fiche lorsque cela est nécessaire.

---

## Page : Chantiers à facturer

### Objectif

Cette page facilite la préparation de la facturation des chantiers en cours.

Elle permet de comparer l'avancement réel des travaux avec le niveau de facturation déjà réalisé afin d'identifier les situations nécessitant l'émission d'une nouvelle facture.

---

### Informations consultables

Pour chaque chantier, l'utilisateur retrouve notamment :

- les informations générales du chantier ;
- le client associé ;
- le devis accepté ;
- le pourcentage d'avancement ;
- le pourcentage déjà facturé ;
- le montant restant à facturer ;
- montant HT du devis ;
- l'historique des factures existantes.

---

### Actions disponibles

Depuis cette page, l'assistante de direction peut :

- consulter les factures déjà émises ;
- créer une nouvelle facture grâce au bouton **Créer une facture**.

La création d'une facture s'effectue au moyen d'un formulaire Airtable dédié, accessible directement depuis cette interface.

---

### Sources de données

Cette page exploite principalement les tables :

- Chantier
- Devis
- Facture
- Client

---

## Page : Documents administratifs

### Objectif

Cette page centralise les documents administratifs associés aux différents chantiers.

Elle facilite leur consultation sans nécessiter l'ouverture des fiches chantier.

---

### Informations consultables

Les utilisateurs peuvent accéder notamment :

- aux devis ;
- aux factures ;
- aux documents administratifs ;
- aux autres pièces enregistrées dans le projet.

---

### Sources de données

- Document chantier

---

### Interactions

Cette page est dédiée à la consultation des documents.

L'ajout de nouveaux documents est réalisé depuis l'interface transversale **Documents & photos**.

---

## Page : Liste des matériaux chantier

### Objectif

Cette page centralise le référentiel des matériaux, fournitures et équipements utilisés sur les chantiers NeoBati. Elle constitue le point d'entrée unique pour la création et la mise à jour des matériaux du catalogue.

---

### Sources de données

- Matériel

---

### Contenu de la page

Vue grille listant l'ensemble des matériaux avec :

- le nom du matériel ;
- la catégorie ;
- l'unité de mesure ;
- le coût unitaire ;
- les notes.

Le bouton **Ajouter un matériau** ouvre un formulaire de création dédié, structuré en une section "Informations matériel" regroupant les champs Nom, Catégorie, Unité de mesure et Coût unitaire, ainsi qu'un champ Notes libre.

---

### Interactions

L'assistante de direction est la seule utilisatrice habilitée à créer et modifier les matériaux depuis cette page. La modification du coût unitaire d'un matériau existant s'effectue directement en grille.

Cette page a été introduite pour éviter qu'un chef de chantier ne doive accéder à la grille de la base afin de créer un matériau non référencé au moment de l'ajout de matériel à une étape (cf. page "Nouveaux chantiers (à préparer)"). Le chef de chantier reste limité à la sélection dans le référentiel existant ; toute création de nouveau matériau transite par cette page.

---

## Interactions avec la base Airtable

### Tables consultées

- Chantier
- Client
- Devis
- Facture
- Document chantier
- Matériel

### Tables modifiées

- Facture (création via formulaire)
- Matériel (création et modification via la page Liste des matériaux chantier)

### Formulaires utilisés

- Créer une facture
- Ajouter un matériau

---

## Rôle dans le système

Cette interface constitue le principal espace de travail de l'assistante de direction.

Elle concentre les opérations liées à la facturation et au suivi administratif tout en garantissant une séparation claire entre les activités de gestion financière et les autres processus métier.

# 5. Interface – Chargé d'affaires : Devis & suivi commercial

## Objectif

L'interface **Chargé d'affaires – Devis & suivi commercial** centralise l'ensemble des activités commerciales précédant la réalisation d'un chantier.

Elle permet de suivre les devis tout au long de leur cycle de vie, de traiter les nouvelles demandes de devis reçues depuis le formulaire public et d'assurer le suivi commercial des prospects jusqu'à la signature d'un devis.

Cette interface constitue le principal espace de travail du chargé d'affaires.

---

## Utilisateur concerné

- Chargé d'affaires

Cette interface est exclusivement réservée à ce profil utilisateur.

---

## Organisation de l'interface

L'interface est composée de trois pages complémentaires.

| Page | Rôle |
|------|------|
| **Pipeline devis** | Suivre les devis selon leur statut commercial et créer de nouveaux devis. |
| **Devis à relancer** | Identifier les devis nécessitant une relance et assurer leur suivi commercial. |
| **Demande de devis** | Examiner les demandes reçues depuis le formulaire public et créer les nouveaux clients. |

---

## Page : Pipeline devis

### Objectif

Cette page constitue le point d'entrée principal de l'interface.

Elle offre une vue Kanban permettant de visualiser rapidement l'ensemble des devis selon leur statut (Brouillon, Envoyé, En attente, Accepté, Refusé, Expiré...) afin de suivre leur progression commerciale.

---

### Fonctionnement

Chaque devis est représenté par une carte affichant les principales informations commerciales (client, montant, date de validité...).

Des filtres et des options de tri permettent au chargé d'affaires d'affiner l'affichage selon ses besoins.

Depuis cette page, il est également possible de créer un nouveau devis grâce au bouton **Créer un devis**.

Ce bouton ouvre un formulaire Airtable dédié permettant de créer directement un nouvel enregistrement dans la table **Devis**.

---

### Sources de données

- Devis
- Client

---

### Interactions

Depuis cette page, le chargé d'affaires peut :

- consulter les devis ;
- suivre leur évolution dans le pipeline commercial ;
- filtrer et trier les devis ;
- créer un nouveau devis via le formulaire **Créer un devis**.

---

## Page : Devis à relancer

### Objectif

Cette page regroupe les devis nécessitant une action commerciale.

Elle permet d'assurer le suivi des prospects n'ayant pas encore répondu ou dont la période de validité du devis approche.

---

### Fonctionnement

Chaque fiche présente les principales informations relatives au devis ainsi que les coordonnées du client concerné.

Le chargé d'affaires peut compléter directement les informations de suivi commercial afin de conserver un historique des relances réalisées.

---

### Informations modifiables

Depuis cette page, il est notamment possible de mettre à jour :

- le statut du devis ;
- la date de dernière relance ;
- les notes commerciales.

---

### Sources de données

- Devis
- Client

---

### Interactions

Cette page permet :

- la consultation des devis à relancer ;
- la mise à jour des informations de suivi commercial ;
- le suivi des échanges avec les prospects.

---

## Page : Demande de devis

### Objectif

Cette page permet de traiter les demandes de devis reçues depuis le formulaire public NeoBati.

Elle constitue le point d'entrée du processus commercial en centralisant les demandes avant leur transformation en client puis en devis.

---

### Fonctionnement

Chaque demande envoyée par un prospect via le formulaire public est automatiquement enregistrée dans la table **Demande de devis**.

Le chargé d'affaires analyse ensuite les informations fournies afin de qualifier la demande.

Lorsque celle-ci est jugée recevable, il peut créer directement un nouveau client grâce au bouton **Créer le client**.

Le client est automatiquement créé dans la table **Client** à partir des informations de la demande.

Une fois le client créé, un devis peut être créé et associé directement à cette demande.

---

### Sources de données

- Demande de devis
- Client
- Devis

---

### Interactions

Depuis cette page, le chargé d'affaires peut :

- consulter les demandes de devis ;
- qualifier une demande ;
- créer automatiquement un client ;
- associer un devis à la demande.

---

## Parcours utilisateur

Le processus commercial suivi dans cette interface est le suivant :

```text
Formulaire public
        │
        ▼
Demande de devis
        │
        ▼
Qualification de la demande
        │
        ▼
Création du client
        │
        ▼
Création du devis
        │
        ▼
Pipeline commercial
        │
        ▼
Relance éventuelle
```

---

## Interactions avec la base Airtable

### Tables consultées

- Demande de devis
- Client
- Devis

### Tables modifiées

- Client (création via le bouton **Créer le client**)
- Devis (création via le formulaire **Créer un devis**)
- Demande de devis (mise à jour du statut et qualification)

### Formulaires utilisés

- Demande de devis (formulaire public)
- Créer un devis

---

## Rôle dans le système

Cette interface constitue le cœur du processus commercial de NeoBati.

Elle assure la continuité entre la réception d'une demande client, sa qualification, la création du client, la réalisation du devis et le suivi commercial jusqu'à la décision finale du prospect.

# 6. Interface – Chefs de chantier : Planning & avancement

## Objectif

L'interface **Chefs de chantier – Planning & avancement** constitue l'espace de travail quotidien des chefs de chantier.

Elle centralise l'ensemble des informations nécessaires au pilotage opérationnel des chantiers : suivi de l'avancement, planification des interventions, affectation des artisans, gestion des documents terrain et contrôle des retards.

Cette interface permet au chef de chantier de disposer d'une vision globale de son activité tout en accédant au détail de chaque étape d'un chantier.

---

## Utilisateur concerné

- Chef de chantier

Cette interface est exclusivement destinée à ce profil utilisateur.

---

## Responsabilités métier

Le chef de chantier est chargé de superviser l'exécution des travaux.

Ses principales missions sont :

- suivre l'avancement des chantiers ;
- organiser les différentes étapes de réalisation ;
- affecter les artisans aux interventions ;
- suivre les retards éventuels ;
- contrôler les coûts opérationnels des étapes ;
- consulter et enrichir la documentation des chantiers.

---

## Organisation de l'interface

L'interface est composée de sept pages.

| Page | Fonction |
|------|----------|
| Tableau de bord - Chantiers | Vue synthétique de l'activité terrain |
| Nouveaux chantiers (à préparer) | Préparation des chantiers avant démarrage |
| Planning des chantiers | Planning global des chantiers |
| Planning des étapes | Organisation chronologique des étapes |
| Étapes en cours | Suivi détaillé des interventions actives |
| Étapes non affectées | Affectation des ressources aux étapes |
| Documents chantiers | Consultation des documents associés aux chantiers |

---

# Page : Tableau de bord - Chantiers

## Objectif

Cette page constitue le point d'entrée principal de l'interface.

Elle offre une vue synthétique des chantiers en cours et met immédiatement en évidence les situations nécessitant une intervention du chef de chantier.

---

## Sources de données

Cette page s'appuie principalement sur les tables :

- Chantier
- Étape

---

## Contenu de la page

Le tableau de bord est organisé autour de deux sections principales.

### Suivi des chantiers

Cette première section présente les principaux indicateurs liés aux chantiers :

- nombre de chantiers en cours ;
- nombre de chantiers en retard.

Une liste détaille ensuite les chantiers actifs avec notamment :

- le client ;
- le pourcentage d'avancement ;
- le statut de retard ;
- la date de fin prévue ;
- l'adresse du chantier.

Cette vue permet d'identifier rapidement les chantiers nécessitant une attention particulière.

---

### Indicateurs terrain

La seconde partie du tableau de bord est consacrée au suivi opérationnel des étapes.

Les principaux indicateurs affichés sont :

- nombre d'étapes actuellement en cours ;
- nombre d'étapes en retard ;
- nombre d'étapes non affectées.

Une liste récapitule également les étapes actuellement en cours d'exécution.

---

## Interactions utilisateur

Cette page est principalement destinée à la consultation.

Elle permet au chef de chantier d'obtenir une vision globale avant de naviguer vers les pages de planification ou de suivi.

---

# Page : Nouveaux chantiers (à préparer)

## Objectif

Cette page centralise les chantiers créés automatiquement après acceptation d'un devis (AUT-COM-004) dont la préparation n'est pas encore terminée. Elle permet au chef de chantier de créer les étapes, d'affecter les artisans et de définir le matériel nécessaire avant le démarrage effectif des travaux.

---

## Sources de données

- Chantier
- Étape
- Devis
- Client

---

## Règle de filtrage

Les chantiers affichés sont ceux dont la case à cocher **Chantier prêt à démarrer** n'est pas cochée. Cette case est renseignée manuellement par le chef de chantier une fois que la préparation (étapes, artisans, matériel) est jugée complète ; aucune automatisation ne détermine cet état.

---

## Contenu de la page

Présentée sous forme d'"Examen des entrées", chaque fiche affiche :

### Informations chantier

- description du projet ;
- adresse ;
- statut du chantier ;
- budget et écart budgétaire ;
- client associé (nom, type, téléphone, e-mail) ;
- devis d'origine (statut, montant HT, montant TTC).

---

### Étapes

Liste des étapes déjà créées pour ce chantier. Le bouton **Créer une étape** ouvre le formulaire dédié, qui pré-remplit automatiquement le chantier concerné et permet de renseigner le nom, la description, le planning et l'artisan affecté. Le matériel n'est volontairement pas saisi à cette étape (voir justification ci-dessous) : la validation ouvre directement la fiche de l'étape créée, où le matériel est ajouté via la section **Matériel utilisé**.

**Limite Airtable et choix retenu** : un formulaire d'interface ne peut pas créer, en une seule soumission, plusieurs enregistrements de jonction porteurs d'attributs propres (ici, chaque ligne de `Quantité Matériel` porte une quantité spécifique). Le champ de liaison d'un formulaire ne permet que de sélectionner des enregistrements déjà existants dans la table liée, jamais d'en créer plusieurs avec une valeur saisie par ligne. La saisie du matériel a donc été déplacée en un second temps, sur la fiche de l'étape, où un élément de liste liée avec formulaire d'ajout dédié permet de créer autant de lignes `Quantité Matériel` que nécessaire, chacune avec sa propre quantité.

---

### Planning

Dates de démarrage et de fin prévue du chantier (champs calculés, restent vides tant qu'aucune étape n'a été créée).

---

### Chantier prêt à démarrer ?

Case à cocher renseignée par le chef de chantier une fois la préparation terminée. Une fois cochée, le chantier sort de cette page et déclenche l'envoi d'une notification de démarrage au chef de chantier, aux artisans affectés aux étapes du chantier et à la Direction (AUT-CHA-008, cf. 02_GUIDE_TECHNIQUE_NEOBATI.md).

---

## Interactions utilisateur

Cette page permet notamment :

- créer une ou plusieurs étapes depuis le formulaire dédié ;
- consulter le contexte complet du chantier (client, devis) sans changer de page ;
- cocher la case de fin de préparation une fois le chantier prêt.

---

## Interactions avec la base Airtable

### Tables consultées

- Chantier
- Devis
- Client

### Tables modifiées

- Chantier (case Chantier prêt à démarrer)
- Étape (création)
- Quantité Matériel (création)

# Page : Planning des chantiers

## Objectif

Cette page permet de visualiser le planning général des chantiers sous forme de chronologie.

Le chef de chantier peut ainsi anticiper les chevauchements d'activité et contrôler les échéances des différents projets.

---

## Fonctionnement

Chaque chantier est représenté sur une frise chronologique.

Des filtres permettent notamment d'affiner l'affichage selon :

- le chantier ;
- le client ;
- le statut.

Cette page est dédiée à la consultation du planning global.

---

# Page : Planning des étapes

## Objectif

Cette page permet de planifier les différentes étapes composant chaque chantier.

Elle offre une vision chronologique des interventions et facilite la coordination des équipes terrain.

---

## Fonctionnement

Les étapes sont présentées sur une chronologie.

Le chef de chantier peut notamment visualiser :

- les étapes en retard ;
- les dépendances entre les étapes ;
- les ressources affectées ;
- la succession des interventions.

Des filtres permettent de retrouver rapidement une étape selon plusieurs critères.

---

# Page : Étapes en cours

## Objectif

Cette page centralise les interventions actuellement en cours d'exécution.

Elle permet au chef de chantier de suivre précisément l'avancement de chaque étape et de mettre à jour les informations opérationnelles.

---

## Sources de données

- Étape
- Artisan
- Chantier
- Quantité matériel
- Document chantier

---

## Informations affichées

Chaque fiche étape présente notamment :

### Suivi de l'étape

- nom de l'étape ;
- statut ;
- indicateur de retard ;
- chantier associé ;
- coût de main-d'œuvre ;
- coût matériel ;
- coût total de l'étape.

Le statut peut être directement modifié depuis cette interface.

---

### Planning

Le planning affiche :

- la date de début prévue ;
- la date de fin prévue ;
- la date de fin réelle ;
- l'étape précédente ;
- l'étape suivante.

Ces informations facilitent le suivi de l'enchaînement logique des interventions.

---

### Artisan(s) affecté(s)

La fiche présente les artisans affectés à l'étape ainsi que leurs principales informations :

- nom ;
- téléphone ;
- compétence principale ;
- coût journalier.

Le bouton **Ajouter ressource** permet d'affecter un nouvel artisan directement à l'étape.

---

### Matériel utilisé

La liste des matériaux consommés est affichée avec :

- le matériel ;
- la quantité utilisée ;
- l'unité ;
- le coût unitaire ;
- le coût total.

Le bouton **Ajouter matériau** ouvre un formulaire de création dans la table `Quantité Matériel`, limité à quatre champs : le matériel (sélection contrainte au référentiel existant dans la table Matériel, sans possibilité de création à la volée), la quantité, les notes, et le lien vers l'étape courante (`ETAPE_QuantiteMateriel`), pré-rempli et verrouillé. Les champs formule et lookup (identifiant, unité, coût unitaire, coût matériel) ne sont pas exposés en saisie. Ce mécanisme permet au chef de chantier d'ajouter autant de lignes de matériel que nécessaire sans jamais manipuler la grille de la base ni créer d'entrée hors référentiel.

---

### Rapport terrain

Cette section est destinée à la consultation des rapports d'intervention associés à l'étape.

---

### Documents & photos

Les documents liés à l'étape sont regroupés dans cette section.

Pour chaque document sont affichés :

- le nom ;
- le fichier ;
- la date ;
- le type ;
- la catégorie ;
- le créateur ;
- l'indicateur de visibilité client.

Le bouton **Ajouter un document** permet d'associer un nouveau document directement depuis cette page.

---

## Interactions utilisateur

Cette page permet notamment :

- modifier le statut d'une étape ;
- renseigner la date de fin réelle ;
- affecter un artisan ;
- consulter les coûts de réalisation ;
- consulter les rapports terrain ;
- ajouter un document au chantier.

---

# Page : Étapes non affectées

## Objectif

Cette page regroupe les étapes ne disposant d'aucun artisan affecté.

Elle permet au chef de chantier d'identifier rapidement les interventions restant à planifier.

---

## Informations affichées

Chaque fiche présente notamment :

### Étape

- nom ;
- statut ;
- indicateur de retard ;
- chantier associé.

---

### Planning

- date de début prévue ;
- date de fin prévue ;
- étape précédente ;
- étape suivante.

---

### Affectation artisan

Le bouton **Ajouter ressource** permet d'affecter un ou plusieurs artisans à l'étape.

---

### Matériel utilisé

Le matériel déjà prévu pour cette intervention est également consultable.

---

## Interactions utilisateur

Cette page est principalement utilisée pour organiser les ressources humaines avant le démarrage des travaux.

---

# Page : Documents chantiers

## Objectif

Cette page centralise l'ensemble des documents liés aux chantiers.

Elle facilite leur consultation sans avoir à ouvrir individuellement chaque chantier ou chaque étape.

---

## Sources de données

- Document chantier

---

## Informations affichées

Chaque document dispose d'une fiche détaillée comprenant :

### Informations générales

- nom du document ;
- description ;
- date ;
- type ;
- catégorie ;
- créateur ;
- visibilité client.

---

### Aperçu du fichier

La partie inférieure de la page affiche directement un aperçu du document ou de la photographie stockée dans Airtable.

Cette fonctionnalité permet de consulter rapidement les pièces du chantier sans téléchargement préalable.

---

## Interactions utilisateur

Cette page est principalement destinée à la consultation documentaire.

Les utilisateurs peuvent retrouver rapidement :

- les plans ;
- les photographies de chantier ;
- les comptes rendus ;
- tout autre document associé à un chantier.

---

## Interactions avec la base Airtable

### Tables consultées

- Chantier
- Étape
- Artisan
- Quantité matériel
- Document chantier

### Tables modifiées

- Étape
- Affectation Artisan
- Document chantier

---

## Rôle dans le système

Cette interface constitue le centre de pilotage opérationnel des chantiers.

Elle relie les données de planification, les ressources humaines, les coûts d'exécution et la documentation afin de permettre au chef de chantier d'assurer le suivi quotidien des travaux et de coordonner efficacement les équipes terrain.

# 7. Interface – Artisans : Mobile terrain

## Objectif

L'interface **Artisans – Mobile terrain** est destinée aux équipes intervenant directement sur les chantiers.

Conçue pour une utilisation sur tablette ou smartphone, elle permet à chaque artisan de consulter les étapes qui lui sont affectées, de suivre l'avancement de ses interventions et de transmettre les informations terrain nécessaires au suivi du chantier.

Cette interface limite volontairement les fonctionnalités disponibles afin de proposer une expérience simple, adaptée aux utilisateurs terrain.

---

## Utilisateurs concernés

- Artisans

Cette interface est exclusivement réservée aux intervenants réalisant les travaux.

---

## Responsabilités métier

L'artisan utilise cette interface afin de :

- consulter les interventions qui lui sont attribuées ;
- prendre connaissance des informations relatives au chantier ;
- suivre le planning des interventions ;
- mettre à jour les informations de réalisation ;
- transmettre un rapport d'avancement ;
- consulter les documents nécessaires à son intervention.

---

## Organisation de l'interface

Cette interface est composée d'une seule page.

| Page | Fonction |
|------|----------|
| Mes étapes | Consultation et suivi des interventions affectées à l'utilisateur connecté |

---

# Page : Mes étapes

## Objectif

Cette page constitue l'espace de travail personnel de chaque artisan.

Elle regroupe exclusivement les étapes qui lui sont attribuées afin de lui fournir toutes les informations nécessaires à la réalisation de son intervention.

---

## Sources de données

Cette page s'appuie principalement sur les tables :

- Étape
- Chantier
- Document chantier
- Rapport terrain

---

## Règle de filtrage

Les données affichées sont automatiquement filtrées selon l'utilisateur Airtable connecté.

Chaque artisan visualise uniquement les étapes dont il est affecté.

Le filtrage repose sur une condition comparant le champ **ArtisanResponsable** de la table **Étape** — champ Lookup remontant le collaborateur de l'artisan affecté à l'étape — avec l'**utilisateur actuellement connecté** (`Utilisateur en cours`).

Ce mécanisme garantit que chaque utilisateur n'accède qu'à ses propres interventions.

**Limite actuelle (à lever en production).** Les enregistrements de la table Artisan partagent aujourd'hui un même collaborateur Airtable (le compte du chef de chantier), utilisé pour la démonstration. Le filtre par utilisateur connecté affiche donc l'ensemble des étapes affectées, quel que soit l'artisan. En usage réel, chaque artisan devra disposer de son propre compte collaborateur, renseigné dans le champ `Collaborateur` de la table Artisan, pour que le cloisonnement par intervenant soit effectif.
---

## Contenu de la page

### Intervention

Cette première section présente les principales informations concernant l'étape :

- nom de l'étape ;
- statut ;
- indicateur de retard ;
- artisan(s) affecté(s).

Le statut de l'étape peut être mis à jour directement depuis cette interface afin de refléter l'avancement réel des travaux.

---

### Planning

Les informations de planification comprennent :

- la date de début prévue ;
- la date de fin prévue ;
- la date de fin réelle.

L'artisan peut renseigner la date de fin réelle lorsque l'intervention est terminée.

---

### Chantier

Cette section présente les informations essentielles concernant le chantier associé :

- nom du chantier ;
- client ;
- description ;
- adresse.

Ces informations permettent à l'artisan de retrouver rapidement le contexte de son intervention.

---

### Rapport terrain

Cette section regroupe les rapports d'avancement liés à l'étape.

Lorsque aucun rapport n'existe encore, l'interface propose un bouton **Créer un rapport d'avancement** ouvrant le formulaire dédié.

Ce formulaire permet notamment de transmettre :

- l'avancement des travaux ;
- les difficultés rencontrées ;
- les observations terrain ;
- les informations destinées au chef de chantier.

---

### Documents

Les documents associés à l'étape sont directement consultables depuis cette page.

L'artisan peut notamment accéder :

- aux plans ;
- aux photographies ;
- aux documents techniques ;
- aux autres pièces nécessaires à son intervention.

---

## Interactions utilisateur

Depuis cette interface, l'artisan peut :

- consulter ses interventions ;
- modifier le statut d'une étape ;
- renseigner la date de fin réelle ;
- consulter les informations du chantier ;
- créer un rapport d'avancement ;
- consulter les documents associés.

---

## Interactions avec la base Airtable

### Tables consultées

- Étape
- Chantier
- Rapport terrain
- Document chantier

### Tables modifiées

- Étape
- Rapport terrain

---

## Rôle dans le système

Cette interface constitue le point d'accès des équipes terrain.

Elle permet aux artisans de disposer uniquement des informations utiles à leurs interventions tout en alimentant la base Airtable avec les données remontées depuis le chantier.

Le filtrage automatique des enregistrements garantit une expérience utilisateur simplifiée et limite l'accès aux seules informations nécessaires à chaque intervenant.

# 8. Interface – Registre des chantiers

## Objectif

L'interface **Registre des chantiers** centralise l'ensemble des informations relatives aux chantiers réalisés par l'entreprise.

Elle constitue un espace de consultation transversal permettant d'accéder rapidement à l'ensemble des données d'un chantier, depuis les informations générales jusqu'au suivi opérationnel, financier et documentaire.

Cette interface est principalement destinée à la consultation afin d'offrir une vision complète de chaque projet.

---

## Utilisateurs concernés

- Tous les utilisateurs

---

## Responsabilités métier

Cette interface permet de :

- consulter les informations générales d'un chantier ;
- suivre son avancement ;
- consulter les étapes de réalisation ;
- visualiser les informations financières associées ;
- consulter les factures liées au chantier ;
- accéder aux rapports terrain ;
- retrouver l'ensemble des documents et photographies du chantier.

---

## Organisation de l'interface

Cette interface est composée d'une seule page.

| Page | Fonction |
|-------|----------|
| Liste des chantiers | Consultation détaillée des informations d'un chantier |

---

# Page : Liste des chantiers

## Objectif

Cette page constitue la fiche complète d'un chantier.

Après sélection d'un chantier dans la liste de gauche, l'ensemble des informations liées à celui-ci est automatiquement affiché dans le panneau principal.

Elle regroupe aussi bien les informations commerciales que les données de suivi opérationnel, financier et documentaire.

---

## Sources de données

Cette page exploite principalement les tables :

- Chantier
- Client
- Devis
- Étape
- Facture
- Rapport terrain
- Document chantier

---

## Contenu de la page

### Informations chantier

Cette première section présente les informations générales du chantier :

- description ;
- adresse ;
- statut du chantier ;
- prochaine action de facturation ;
- client associé ;
- devis accepté ayant généré le chantier.

Deux indicateurs visuels permettent également de suivre :

- le pourcentage d'avancement du chantier ;
- le pourcentage de facturation.

Ces informations offrent une vision synthétique de la situation globale du projet.

---

### Avancement & planning

Cette section présente les principaux indicateurs de planification :

- date de démarrage ;
- date de fin prévue ;
- date de fin réelle ;
- indicateur de retard ;
- nombre de jours de retard.

Elle permet d'identifier rapidement les éventuels écarts entre le planning prévu et la réalisation effective.

---

### Informations financières

Cette section synthétise les principaux indicateurs financiers du chantier :

- montant HT facturé ;
- montant HT restant à facturer ;
- montant HT encaissé.

Ces indicateurs permettent de suivre rapidement la situation financière du chantier.

---

### Étapes

Cette section affiche l'ensemble des étapes composant le chantier.

Pour chaque étape sont notamment affichés :

- l'identifiant ;
- le statut ;
- la date de début ;
- la date de fin prévue ;
- la date de fin réelle ;
- l'indicateur de retard ;
- l'artisan affecté ;
- le coût de la main-d'œuvre.

Cette vue permet de suivre la progression opérationnelle du chantier.

---

### Factures du chantier

Toutes les factures associées au chantier sont regroupées dans cette section.

Pour chaque facture sont affichés :

- l'identifiant ;
- la date d'émission ;
- la date d'échéance ;
- le statut de la facture ;
- le statut de paiement ;
- le montant HT ;
- le montant TTC ;
- le montant HT encaissé ;
- le montant restant à encaisser.

Cette vue facilite le suivi administratif et financier du chantier.

---

### Rapport terrain

Les rapports d'avancement transmis depuis le terrain sont regroupés dans cette section.

Les principales informations affichées sont :

- identifiant du rapport ;
- auteur ;
- étape concernée ;
- type de rapport ;
- présence éventuelle d'un problème bloquant.

Cette vue permet de retrouver rapidement les comptes rendus liés au chantier.

---

### Documents & photos

Cette dernière section regroupe l'ensemble des documents associés au chantier.

Elle permet notamment de consulter :

- devis signés ;
- factures ;
- photographies du chantier ;
- plans ;
- autres documents administratifs ou techniques.

Pour chaque document sont affichés :

- le nom du document ;
- le fichier ;
- la date ;
- le type ;
- la catégorie ;
- le créateur ;
- l'indicateur de visibilité client.

Cette centralisation facilite le partage d'informations entre les différents intervenants.

---

## Interactions utilisateur

Depuis cette interface, l'utilisateur peut :

- rechercher un chantier ;
- filtrer les chantiers par client ;
- consulter les informations détaillées d'un chantier ;
- consulter les étapes associées ;
- consulter les factures ;
- consulter les rapports terrain ;
- consulter les documents et photographies.

Cette interface est principalement destinée à la consultation des données.

---

## Interactions avec la base Airtable

### Tables consultées

- Chantier
- Client
- Devis
- Étape
- Facture
- Rapport terrain
- Document chantier

### Tables modifiées

Aucune.

L'interface est utilisée comme registre de consultation centralisé.

---

## Rôle dans le système

Le registre des chantiers constitue le point d'accès principal aux informations historiques et opérationnelles des projets.

En regroupant dans une seule interface les données commerciales, opérationnelles, financières et documentaires, il facilite le suivi des chantiers par l'ensemble des collaborateurs tout en limitant les changements entre les différentes tables de la base Airtable.

# 9. Interface – Registre des clients

## Objectif

L'interface **Registre des clients** centralise l'ensemble des informations relatives aux clients de l'entreprise.

Elle permet d'accéder rapidement à la fiche complète d'un client ainsi qu'à l'ensemble de son historique commercial, de ses chantiers et de sa situation financière.

Cette interface est principalement destinée à la consultation afin d'offrir une vision globale de la relation client.

---

## Utilisateurs concernés

- Tous les utilisateurs 

---

## Responsabilités métier

Cette interface permet de :

- consulter les informations d'un client ;
- accéder à son historique commercial ;
- consulter ses devis ;
- consulter les chantiers réalisés ;
- suivre les factures associées ;
- visualiser les principaux indicateurs financiers.

---

## Organisation de l'interface

Cette interface est composée d'une seule page.

| Page | Fonction |
|-------|----------|
| Liste des clients | Consultation détaillée des informations d'un client |

---

# Page : Liste des clients

## Objectif

Cette page constitue la fiche complète d'un client.

Après sélection d'un client dans la liste de gauche, l'ensemble des informations liées à celui-ci est affiché dans le panneau principal.

Elle regroupe les informations administratives, l'historique commercial ainsi que les principaux indicateurs financiers du client.

---

## Sources de données

Cette page exploite principalement les tables :

- Client
- Demande de devis
- Devis
- Chantier
- Facture

---

## Contenu de la page

### Informations client

Cette première section présente les informations générales du client.

Les informations affichées comprennent notamment :

- nom ;
- adresse e-mail ;
- numéro de téléphone ;
- adresse postale ;
- type de client (particulier ou professionnel) ;
- statut du client (prospect, actif ou ancien) ;
- nombre de devis ;
- nombre de chantiers réalisés.

Cette vue permet d'obtenir rapidement une synthèse de la relation commerciale.

---

### Historique commercial

Cette section regroupe les principaux éléments de l'historique commercial du client.

Elle présente successivement :

#### Demandes de devis

Lorsque des demandes existent, elles sont directement accessibles depuis cette section.

#### Devis

Les devis associés au client sont affichés avec leurs principales informations :

- identifiant ;
- statut ;
- date d'envoi ;
- date de validité ;
- montant TTC.

#### Chantiers

Les chantiers réalisés pour ce client sont consultables avec notamment :

- nom du chantier ;
- description ;
- statut ;
- taux d'avancement ;
- taux de facturation.

#### Factures

Les factures du client sont également regroupées dans cette section.

Pour chacune sont affichés :

- identifiant ;
- type de facture ;
- statut ;
- montant HT ;
- montant TTC.

Cette organisation permet de suivre rapidement l'ensemble du cycle commercial du client, depuis le devis jusqu'à la facturation.

---

### Historique des interactions

Chaque fiche client affiche un groupe « Historique des interactions », listant les relances automatisées envoyées à ce client (InteractionID, Date/Heure, Type, Canal, Devis ou Facture concerné), issu de la table Interaction client (cf. 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md, section 3.12). Chaque ligne renvoie vers la fiche détaillée de l'interaction, présentant le contenu intégral du message envoyé.

---

### Synthèse financière

Cette dernière section présente les principaux indicateurs financiers du client.

Les indicateurs affichés sont :

- chiffre d'affaires HT réalisé ;
- chiffre d'affaires HT potentiel ;
- montant HT facturé ;
- montant HT restant à facturer ;
- montant HT restant à encaisser.

Cette synthèse offre une vision immédiate de la valeur générée par chaque client ainsi que du chiffre d'affaires encore mobilisable.

---

## Interactions utilisateur

Depuis cette interface, l'utilisateur peut :

- rechercher un client ;
- filtrer les clients par type ;
- consulter la fiche détaillée d'un client ;
- consulter son historique commercial ;
- consulter ses devis ;
- consulter ses chantiers ;
- consulter ses factures ;
- consulter l'historique de ses interactions ;
- suivre sa situation financière.

Cette interface est principalement destinée à la consultation des données.

---

## Interactions avec la base Airtable

### Tables consultées

- Client
- Demande de devis
- Devis
- Chantier
- Facture

### Tables modifiées

Aucune.

L'interface est utilisée comme registre de consultation centralisé.

---

## Rôle dans le système

Le registre des clients constitue le point d'entrée principal pour le suivi de la relation client.

En regroupant dans une seule interface les informations administratives, commerciales, opérationnelles et financières, il permet aux différents collaborateurs d'accéder rapidement à une vision complète de chaque client sans naviguer entre plusieurs tables de la base Airtable.

# 10. Interface – Documents & photos

## Objectif

L'interface **Documents & photos** centralise l'ensemble des documents produits ou utilisés dans le cadre des projets de l'entreprise.

Elle constitue une bibliothèque documentaire permettant de retrouver rapidement tous les fichiers associés aux chantiers, indépendamment de leur provenance.

Cette interface facilite la consultation, le partage et la traçabilité des documents tout au long du cycle de vie d'un chantier.

---

## Utilisateurs concernés

- Direction
- Assistant administratif
- Chargé d'affaires
- Chef de chantier

---

## Responsabilités métier

Cette interface permet de :

- consulter l'ensemble des documents enregistrés ;
- visualiser directement les fichiers stockés ;
- retrouver les documents d'un chantier ;
- consulter les informations associées à chaque document ;
- vérifier si un document est visible par le client.

---

## Organisation de l'interface

Cette interface est composée d'une seule page.

| Page | Fonction |
|-------|----------|
| Tous les documents | Bibliothèque documentaire centralisée |

---

# Page : Tous les documents

## Objectif

Cette page centralise tous les documents enregistrés dans la base Airtable.

Après sélection d'un document dans la liste de gauche, l'ensemble de ses informations est affiché dans le panneau principal.

Cette organisation permet de retrouver rapidement un document sans devoir rechercher le chantier auquel il est rattaché.

---

## Sources de données

Cette page exploite principalement la table :

- Document chantier

Des informations complémentaires sont récupérées via les relations avec :

- Chantier
- Étape

---

## Contenu de la page

### Informations document

Cette première section présente les métadonnées du document.

Les informations affichées comprennent notamment :

- nom du document ;
- description ;
- date de création ;
- type de document ;
- catégorie ;
- créateur ;
- indicateur de visibilité client.

Ces informations permettent d'identifier rapidement le document et son contexte d'utilisation.

---

### Document / photo

Cette section affiche directement le fichier enregistré dans Airtable.

Selon son type, l'utilisateur peut consulter :

- une photographie de chantier ;
- un plan ;
- une facture ;
- un devis signé ;
- un compte rendu ;
- tout autre document technique ou administratif.

L'aperçu intégré évite de devoir télécharger systématiquement le document avant consultation.

---

### Rattachement chantier / étape

Cette section indique à quel chantier est associé le document.

Lorsque le document est lié à une étape spécifique, celle-ci est également affichée.

Cette relation facilite la compréhension du contexte dans lequel le document a été produit.

---

## Types de documents gérés

La base documentaire permet notamment de stocker :

- photographies avant travaux ;
- photographies de suivi de chantier ;
- photographies de fin de chantier ;
- devis signés ;
- factures ;
- plans techniques ;
- comptes rendus terrain ;
- autres documents administratifs.

Cette catégorisation facilite la recherche et la consultation des documents.

---

## Interactions utilisateur

Depuis cette interface, l'utilisateur peut :

- rechercher un document ;
- parcourir la bibliothèque documentaire ;
- consulter les informations détaillées d'un document ;
- visualiser le fichier associé ;
- identifier le chantier concerné ;
- vérifier la visibilité d'un document pour le client.

Cette interface est principalement destinée à la consultation centralisée des ressources documentaires.

---

## Interactions avec la base Airtable

### Tables consultées

- Document chantier
- Chantier
- Étape

### Tables modifiées

Aucune.

Cette interface constitue une bibliothèque documentaire centralisée reposant sur la table **Document chantier**.

---

## Rôle dans le système

L'interface **Documents & photos** centralise l'ensemble des ressources documentaires de l'entreprise.

Contrairement au **Registre des chantiers**, où les documents sont consultés dans le contexte d'un projet spécifique, cette interface permet une consultation transversale de tous les documents enregistrés dans la base.

Elle constitue ainsi le point d'accès principal à la documentation des projets, qu'il s'agisse de documents administratifs, techniques ou de photographies de chantier.

# 11. Synthèse de l'architecture des interfaces

L'organisation des interfaces a été pensée selon une logique métier afin de répondre aux besoins des différents profils utilisateurs.

Les interfaces se répartissent en quatre catégories :

- **Interfaces de pilotage** : destinées à la Direction et à l'administratif pour le suivi de l'activité via des tableaux de bord et des indicateurs clés.

- **Interfaces opérationnelles** : destinées aux chargés d'affaires, chefs de chantier et artisans afin de réaliser les actions quotidiennes (création de devis, affectation des ressources, suivi terrain, rapports d'avancement, etc.).

- **Interfaces de consultation** : registres des chantiers, des clients et bibliothèque documentaire offrant une vision consolidée des données.

- **Interfaces collaboratives** : formulaires permettant la création de devis, de factures, de rapports terrain ou de documents directement depuis les interfaces.

Cette organisation limite les manipulations dans les tables Airtable, simplifie l'expérience utilisateur et adapte chaque interface aux besoins réels de son métier.

---

# Objectif des prochaines conversations
1. Automatisations Make
2. Scénarios IA