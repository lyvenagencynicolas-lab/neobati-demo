# 00_CONTEXTE_BASE_AIRTABLE_NEOBATI

## Projet professionnel – NeoBati

Version : 2.0

---

# 1. Présentation du document

## 1.1 Objectif

Ce document décrit l'architecture fonctionnelle de la base Airtable développée pour le projet **NeoBati**.

Il constitue le document de référence présentant l'organisation des données, les principales règles métier et les relations entre les différentes tables composant le système d'information.

L'objectif n'est pas de détailler l'ensemble des champs ou des vues de la base, mais de fournir une compréhension globale de son fonctionnement afin de faciliter son évolution, sa maintenance et le développement des automatisations associées.

Ce document est complété par :

- **01_DOCUMENTATION_DETAILLEE_BASE_AIRTABLE_NEOBATI.md**, qui décrit en détail la structure technique de la base ;
- **02_CONTEXTE_INTERFACES_NEOBATI.md**, qui présente l'architecture des interfaces Airtable utilisées par les différents métiers.

---

## 1.2 Positionnement dans la documentation

La documentation du projet NeoBati est organisée en plusieurs documents complémentaires.

Chaque document répond à un objectif spécifique.

| Document | Objectif |
|-----------|----------|
| **00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md** | Présenter l'architecture générale de la base Airtable et les principales règles métier. |
| **01_DOCUMENTATION_DETAILLEE_BASE_AIRTABLE_NEOBATI.md** | Décrire en détail la structure technique de la base, les champs, les formules et les éléments d'implémentation. |
| **02_CONTEXTE_INTERFACES_NEOBATI.md** | Décrire les interfaces Airtable mises à disposition des différents profils utilisateurs. |

Ensemble, ces documents constituent la documentation fonctionnelle de référence du projet.

# 2. Présentation générale du système d'information

## 2.1 Objectifs du système

Le système d'information NeoBati a été conçu afin de centraliser l'ensemble des informations nécessaires au pilotage d'une entreprise spécialisée dans les travaux de rénovation.

Il couvre l'ensemble du cycle de vie d'un projet, depuis la réception d'une demande de devis jusqu'au suivi des paiements, en passant par la planification des travaux, le suivi des interventions terrain et la gestion documentaire.

La base Airtable constitue le référentiel unique des données utilisées par les différents utilisateurs de l'entreprise.

---

## 2.2 Architecture générale

La base est organisée autour d'une table centrale : **Chantier**.

Autour de cette table gravitent les différentes entités représentant les acteurs, les documents, les opérations et les événements intervenant au cours de la réalisation d'un projet.

Cette organisation permet de limiter les duplications d'information tout en facilitant la navigation entre les différentes données du système.

---

## 2.3 Principes de modélisation

La conception de la base repose sur plusieurs principes.

### Centralisation des données

Chaque information est enregistrée une seule fois dans une table dédiée, puis réutilisée au travers des relations entre les tables.

Cette approche garantit la cohérence des données et simplifie leur maintenance.

### Séparation des responsabilités

Chaque table représente une entité métier clairement identifiée (client, devis, chantier, étape, facture, etc.).

Cette séparation facilite l'évolution du système et limite les dépendances entre les différentes fonctionnalités.

### Utilisation de tables de jonction

Lorsque plusieurs entités entretiennent une relation de type plusieurs-à-plusieurs, une table intermédiaire est utilisée afin de conserver un modèle relationnel normalisé.

C'est notamment le cas de la table **Quantité matériel**, qui relie les étapes aux matériels utilisés tout en enregistrant les quantités consommées.

### Automatisation des processus

La structure de la base a été pensée afin de faciliter la mise en œuvre d'automatisations via Airtable Automation et Make.

Les principales règles métier reposent sur les relations entre les tables plutôt que sur des traitements manuels.

---

## 2.4 Vue d'ensemble des tables

La base NeoBati est composée de onze tables représentant les principales entités du système d'information.

| Table | Rôle principal |
|--------|----------------|
| Client | Référentiel des clients de l'entreprise. |
| Demande de devis | Centralisation des demandes reçues depuis le formulaire public. |
| Devis | Gestion des propositions commerciales. |
| Chantier | Table centrale représentant les projets réalisés. |
| Étape | Planification et suivi des différentes interventions composant un chantier. |
| Rapport terrain | Comptes rendus transmis depuis le terrain par les artisans. |
| Artisan | Référentiel des intervenants réalisant les travaux. |
| Matériel | Référentiel des matériaux et équipements utilisés. |
| Quantité matériel | Association entre les étapes et les matériels consommés. |
| Facture | Gestion de la facturation et des paiements. |
| Document chantier | Centralisation des documents et photographies associés aux projets. |

# 3. Description des tables

## 3.1 Table Client

### Objectif

La table **Client** constitue le référentiel des clients et prospects de NeoBati.

Elle centralise les informations d'identification de chaque client tout en consolidant les principaux indicateurs commerciaux, opérationnels et financiers issus des autres tables de la base.

Chaque enregistrement représente un client unique pouvant être lié à plusieurs demandes de devis, devis, chantiers et factures.

La table sert ainsi de point d'entrée pour consulter l'ensemble de l'historique d'un client.

---

### Données gérées

La table regroupe quatre grandes catégories d'informations.

#### Informations d'identification

Ces champs permettent d'identifier le client.

- Identifiant client
- Nom
- Adresse e-mail
- Téléphone
- Adresse postale
- Type de client (Particulier ou Professionnel)

---

#### Suivi commercial

Ces informations synthétisent l'activité commerciale du client.

On y retrouve notamment :

- le nombre de devis associés ;
- le statut des devis ;
- les demandes de devis liées ;
- le chargé d'affaires responsable du client.

Ces données permettent d'identifier rapidement la position du client dans le cycle commercial.

---

#### Suivi des chantiers

La table consolide également les informations liées aux chantiers.

Parmi les principaux indicateurs figurent :

- les chantiers associés ;
- le nombre de chantiers réalisés ;
- le statut du dernier chantier.

Ces informations permettent de distinguer les prospects des clients actifs ou des anciens clients.

---

#### Suivi financier

La table regroupe enfin plusieurs indicateurs calculés automatiquement à partir des factures.

Les principaux montants suivis sont :

- chiffre d'affaires potentiel HT ;
- chiffre d'affaires HT facturé ;
- montant HT restant à facturer ;
- montant HT encaissé ;
- montant HT restant à encaisser ;
- statut des factures.

Ces indicateurs offrent une vision synthétique de la situation financière de chaque client.

---

### Relations

La table Client est reliée aux tables suivantes :

| Table liée | Relation | Description |
|------------|----------|-------------|
| Demande de devis | 1 → N | Un client peut effectuer plusieurs demandes de devis. |
| Devis | 1 → N | Un client peut recevoir plusieurs devis. |
| Chantier | 1 → N | Un client peut être associé à plusieurs chantiers. |
| Facture | 1 → N | Un client peut posséder plusieurs factures. |

---

### Principales règles métier

- Un client peut exister sans devis ni chantier.
- Une demande de devis peut être rattachée à un client existant ou conduire à la création d'un nouveau client.
- Les indicateurs commerciaux sont calculés automatiquement à partir des devis liés.
- Les indicateurs financiers sont calculés automatiquement à partir des factures liées.
- Le statut du client est déterminé par son niveau d'activité (Prospect, Actif ou Ancien).
- Le chargé d'affaires responsable est associé directement à la fiche client afin de faciliter le suivi commercial.

---

### Utilisation dans les interfaces

Cette table est utilisée dans plusieurs interfaces du projet.

- **Direction** : analyse du portefeuille clients, chiffre d'affaires et indicateurs financiers.
- **Administratif** : consultation des fiches clients, relances et suivi des factures.
- **Chargé d'affaires** : suivi des prospects et préparation des devis.
- **Registre des clients** : consultation détaillée de l'historique commercial, des chantiers et des indicateurs financiers.

---

### Remarques de conception

La table Client ne constitue pas uniquement un annuaire.

Elle joue le rôle de tableau de synthèse en agrégeant automatiquement les informations provenant des devis, des chantiers et des factures. Cette approche permet de disposer, depuis une seule fiche client, d'une vision globale de la relation commerciale sans avoir à consulter séparément chaque table.

## 3.2 Table Demande de devis

### Objectif

La table **Demande de devis** constitue le point d'entrée du processus commercial de NeoBati.

Elle centralise l'ensemble des demandes reçues avant la création d'un devis et permet d'assurer leur suivi jusqu'à leur qualification.

Chaque enregistrement correspond à une demande exprimée par un prospect ou un client souhaitant obtenir une proposition commerciale.

Cette table permet de conserver l'historique des demandes, même lorsqu'elles ne donnent finalement pas lieu à un devis.

---

### Données gérées

La table regroupe quatre catégories d'informations.

#### Informations de la demande

Ces champs décrivent la demande initiale.

Ils comprennent notamment :

- Identifiant de la demande ;
- Date de création de la demande ;
- Statut de la demande.

Le statut permet de suivre l'avancement de l'étude commerciale.

---

#### Informations du prospect

Ces champs permettent d'identifier le demandeur.

Ils comprennent :

- Nom ;
- Adresse e-mail ;
- Téléphone ;
- Adresse ;
- Type de prospect (Particulier ou Professionnel).

Lorsque le prospect devient client, un lien est créé avec la table **Client**.

---

#### Description du projet

Cette partie regroupe les informations nécessaires à l'établissement du devis.

Les principaux éléments sont :

- adresse du chantier ;
- description du projet ;
- type de chantier ;
- budget estimé ;
- date de début souhaitée.

Ces informations servent de base au travail du chargé d'affaires lors de la préparation du devis.

---

#### Documents et suivi commercial

La table permet également de stocker les éléments utiles à l'étude de la demande.

On y retrouve notamment :

- les documents transmis par le prospect ;
- le devis créé à partir de la demande ;
- la raison du refus lorsqu'aucun devis n'est finalement retenu.

Ces informations permettent de conserver l'historique complet du traitement de chaque demande.

---

### Relations

La table Demande de devis est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Client | N → 1 | Une demande est associée à un client ou à un prospect qui deviendra client. |
| Devis | 1 → 1 | Une demande peut donner lieu à la création d'un devis. |

---

### Principales règles métier

- Chaque demande possède un identifiant unique.
- Une demande peut être créée avant l'existence d'un client dans la base.
- Une demande peut aboutir à la création d'un devis.
- Une demande peut être refusée sans création de devis.
- Les documents transmis par le prospect restent rattachés à la demande.
- Lorsqu'une demande est refusée, une raison peut être renseignée afin de conserver un historique commercial.

---

### Utilisation dans les interfaces

Cette table est principalement utilisée dans l'interface **Chargé d'affaires — Devis & suivi commercial**.

Elle intervient dans plusieurs pages :

- **Demande de devis**, permettant d'étudier une demande et de qualifier le besoin ;
- **Pipeline devis**, depuis lequel un devis peut être créé à partir d'une demande validée.

Les informations de cette table sont également consultables depuis les fiches clients afin de conserver l'historique commercial.

---

### Remarques de conception

La table Demande de devis est volontairement distincte de la table Devis.

Cette séparation permet de distinguer clairement :

- la phase de qualification du besoin ;
- la phase de chiffrage ;
- la proposition commerciale.

Ce découpage facilite le suivi des taux de transformation entre les demandes reçues et les devis effectivement réalisés, tout en conservant l'historique des demandes n'ayant pas abouti.

## 3.3 Table Devis

### Objectif

La table **Devis** constitue le cœur du processus commercial de NeoBati.

Elle centralise les propositions commerciales établies pour les clients et assure la transition entre la phase de qualification du besoin et le lancement opérationnel du chantier.

Chaque enregistrement représente un devis unique, pouvant être accepté, refusé, en attente de réponse ou expiré.

Lorsqu'un devis est accepté, il constitue la base de création du chantier et du processus de facturation.

---

### Données gérées

La table regroupe cinq catégories d'informations.

#### Informations générales

Ces champs permettent d'identifier le devis et de suivre son cycle de vie.

Ils comprennent notamment :

- Identifiant du devis ;
- Client associé ;
- Date d'envoi ;
- Date de validité ;
- Statut du devis.

Le statut représente l'état d'avancement commercial du devis.

---

#### Description du projet

Cette catégorie reprend les informations nécessaires à la réalisation des travaux.

Les principaux champs sont :

- Description du projet ;
- Type de chantier ;
- Adresse du chantier ;
- Date de début souhaitée ;
- Notes commerciales.

Ces informations sont ensuite réutilisées lors de la création du chantier.

---

#### Informations financières

Le devis centralise l'ensemble des montants de la proposition commerciale.

Les principaux champs sont :

- Montant HT ;
- Taux de TVA ;
- Montant de TVA ;
- Montant TTC.

Les montants TTC sont calculés automatiquement à partir du montant HT et du taux de TVA.

---

#### Suivi commercial

Cette catégorie permet de gérer le suivi des devis en attente.

Elle comprend notamment :

- Nombre de relances effectuées (`NombreRelances`) ;
- Date de dernière relance (`DateDerniereRelance`) ;
- Indicateur « À relancer » (`ARelancer`, champ Formule) ;
- Jours restants avant expiration (`JoursRestantsValidite`, champ Formule).

Ces champs facilitent le suivi commercial des devis n'ayant pas encore reçu de réponse. `ARelancer` pilote l'éligibilité à la relance automatique (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md, AUT-COM-003) ; `JoursRestantsValidite` alimente le contenu des e-mails de relance.

Deux champs Lookup complètent ces informations pour les besoins de l'automatisation de relance : le nom du client (`NomClient_CLIENT`) et son adresse e-mail (`EmailClient_CLIENT`), évitant une recherche supplémentaire côté Make pour récupérer les coordonnées à chaque envoi.

---

#### Liens avec les autres processus

La table conserve les liens vers les différentes étapes du cycle de vie du projet.

On y retrouve notamment :

- le client concerné ;
- la demande de devis d'origine ;
- le chantier créé à partir du devis ;
- les factures associées.

Ces relations permettent de suivre l'ensemble du parcours d'un projet depuis la première demande jusqu'à la facturation.

---

### Relations

La table Devis est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Client | N → 1 | Chaque devis est associé à un client. |
| Demande de devis | N → 1 | Un devis peut être créé à partir d'une demande de devis. |
| Chantier | 1 → 1 | Un devis accepté peut générer un chantier. |
| Facture | 1 → N | Un devis peut être associé à plusieurs factures (acompte, situations, solde). |

---

### Principales règles métier

- Chaque devis possède un identifiant unique.
- Un devis est obligatoirement associé à un client.
- Un devis peut être créé indépendamment d'une demande de devis.
- Un devis accepté peut donner lieu à la création d'un chantier.
- Plusieurs factures peuvent être rattachées au même devis.
- Les montants TTC sont calculés automatiquement à partir du montant HT et du taux de TVA.
- Les devis en attente peuvent être identifiés automatiquement pour les campagnes de relance commerciale.

---

### Utilisation dans les interfaces

La table est utilisée dans plusieurs interfaces du projet.

**Chargé d'affaires**

- Pipeline des devis ;
- Demande de devis ;
- Devis à relancer.

Le chargé d'affaires pilote l'ensemble du cycle commercial depuis ces pages.

**Administratif**

- Consultation des devis ;
- Identification des devis acceptés devant être facturés.

**Chefs de chantier**

- Consultation des devis transformés en chantier.

---

### Remarques de conception

La table Devis constitue le point de bascule entre la phase commerciale et la phase opérationnelle.

Elle centralise l'ensemble des informations nécessaires au lancement d'un chantier tout en conservant le suivi financier et commercial de la proposition.

Grâce à ses relations avec les tables Client, Demande de devis, Chantier et Facture, elle joue un rôle de pivot dans le modèle de données et garantit la continuité du processus métier, depuis la qualification du besoin jusqu'à la facturation finale.

## 3.4 Table Chantier

### Objectif

La table **Chantier** représente l'ensemble des projets de travaux réalisés par NeoBati.

Elle constitue le cœur du suivi opérationnel de l'entreprise en regroupant toutes les informations nécessaires au pilotage d'un chantier, depuis son démarrage jusqu'à sa clôture.

Chaque chantier est créé à partir d'un devis accepté et centralise les données relatives à l'avancement, aux coûts, à la facturation, aux intervenants, aux documents et aux rapports terrain.

---

### Données gérées

La table regroupe plusieurs catégories d'informations.

#### Informations générales

Ces champs permettent d'identifier le chantier.

Ils comprennent notamment :

- Identifiant du chantier ;
- Nom du chantier ;
- Client associé ;
- Description du projet ;
- Adresse du chantier ;
- Nom du client (`Nom_CLIENT_Chantier`, champ Lookup sur le champ lié `CLIENT_Chantier`).

Ce champ Lookup a été ajouté car le champ lié `CLIENT_Chantier` seul, une fois mappé comme input variable dans un script d'automatisation Airtable, renvoie le champ primaire de l'enregistrement Client lié (`Identifiant client`, qui concatène un numéro et le nom du client), et non le nom du client isolément. Ce Lookup permet d'obtenir le nom seul, notamment pour la notification AUT-CHA-002.

Ces informations proviennent principalement du devis accepté.

---

#### Préparation

- Chantier prêt à démarrer (case à cocher, `PretADemarrer`).

Ce champ est renseigné manuellement par le chef de chantier une fois que la préparation du chantier (création des étapes, affectation des artisans, définition du matériel) est jugée complète. Aucune automatisation ne coche cette case ; elle sert de filtre sur la page "Nouveaux chantiers (à préparer)" de l'interface Chef de chantier (cf. 01_CONTEXTE_INTERFACES_NEOBATI.md). Cocher cette case déclenche la notification de démarrage du chantier au chef de chantier, aux artisans affectés et à la Direction (AUT-CHA-008, cf. 02_GUIDE_TECHNIQUE_NEOBATI.md).

---

#### Planning

Cette catégorie permet le suivi temporel du chantier.

Les principaux champs sont :

- Date de démarrage (champ calculé, voir remarque ci-dessous) ;
- Date de fin estimée (champ calculé, voir remarque ci-dessous) ;
- Date de fin réelle (champ calculé, voir remarque ci-dessous) ;
- Statut du chantier (champ calculé, voir remarque ci-dessous) ;
- Premier statut d'étape ;
- Dernier statut d'étape.

Ces informations permettent de suivre la progression générale du chantier.

**Remarque technique.** Quatre de ces champs sont calculés automatiquement à partir des Étapes liées (`ETAPES_Chantier`) et ne doivent jamais être mappés en écriture dans une automatisation Make :

- `Statut du chantier` : champ Formula.
- `Date de démarrage` : champ Rollup, `MIN(DateDebutPrevu)` sur les Étapes liées. Reste vide tant qu'aucune Étape n'a été créée.
- `Date de fin estimée` : champ Rollup, `MAX(DateFinPrevu)` sur les Étapes liées.
- `Date de fin réelle` : champ Lookup sur `DateFinReelle` (Étape), limité au dernier élément lié. Point de vigilance : ce champ retient la dernière Étape selon l'ordre du lien `ETAPES_Chantier`, pas nécessairement l'Étape la plus tardive chronologiquement — à vérifier en usage réel si les Étapes ne sont pas toujours liées dans leur ordre d'achèvement.

Ces quatre champs se peuplent uniquement une fois les Étapes du chantier créées manuellement par le chef de chantier (aucune automatisation ne génère les étapes, cf. domaine Gestion des chantiers, 02_GUIDE_TECHNIQUE_NEOBATI.md).

---

#### Avancement

Le suivi d'avancement est calculé automatiquement à partir des étapes.

Les principaux indicateurs sont :

- Pourcentage d'avancement (`Avancement(%)`, champ Formule : `IF(NbrEtapesTotales=0, 0, NbrEtapesTerminee/NbrEtapesTotales)`) ;
- Nombre total d'étapes (`NbrEtapesTotales`, champ Quantité — comptage des Étapes liées) ;
- Nombre d'étapes terminées (`NbrEtapesTerminee`, champ Cumul — somme du champ Formule `EstTerminée` des Étapes liées) ;
- Chantier en retard (`EnRetard`, champ Formule — "Oui" si le chantier a des étapes, que la date de fin estimée est dépassée et que le statut n'est pas "Terminé") ;
- Nombre de jours de retard (`JoursRetardChantier`, champ Formule, calculé uniquement si `EnRetard = "Oui"`) ;
- Notifié retard (`NotifieRetard`, checkbox coché automatiquement par l'automatisation AUT-CHA-004 une fois la notification de retard envoyée — cf. 02_GUIDE_TECHNIQUE_NEOBATI.md).

Les cinq premiers champs sont entièrement natifs et se recalculent automatiquement sans aucune automatisation (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md, note sur AUT-CHA-003). Le champ `NotifieRetard`, en revanche, est renseigné par l'automatisation AUT-CHA-004 elle-même (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md pour le détail d'implémentation).

Ces indicateurs permettent un pilotage rapide de l'état d'avancement.

---

#### Budget et rentabilité

La table centralise l'ensemble des indicateurs financiers du chantier.

Les principaux champs sont :

- Budget du chantier (`Budget`) ;
- Coût total des artisans ;
- Coût des matériaux ;
- Coût total du chantier (`CoutTotalChantier`) ;
- Écart budgétaire (`EcartBudget`, champ Formule : `Budget - CoutTotalChantier`) ;
- Marge brute HT (`MargeBrutHT`, champ Formule) ;
- Taux de marge (`TauxMargeHT`, champ Formule) ;
- Marge brute prévisionnelle HT (`MargeBrutPrevisionnelleHT`, champ Formule) ;
- Taux de marge prévisionnelle HT (`TauxMargePrevisionnelleHT`, champ Formule) ;
- Chantier prévisionnellement déficitaire (`ChantierDeficitaire`, champ Formule).

Ces informations sont calculées automatiquement à partir des coûts réellement engagés. Un `EcartBudget` négatif signifie un dépassement du budget prévisionnel — convention de signe exploitée par l'automatisation AUT-CHA-007 (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md).

**Marge réalisée et marge prévisionnelle — deux lectures distinctes et non redondantes.**

`MargeBrutHT` (`IF(MontantFactureHT = 0, BLANK(), MontantFactureHT - CoutTotalChantier)`) mesure la marge **réalisée** : elle rapporte ce qui a été effectivement facturé au coût engagé, et reste volontairement vide (`BLANK()`) tant qu'aucune facture n'a été émise pour le chantier — un chantier non facturé n'a pas de marge réalisée nulle, il n'en a pas encore. `TauxMargeHT` applique la même garde.

`MargeBrutPrevisionnelleHT` (`MontantHTDevis - CoutTotalChantier`) mesure la marge **prévisionnelle** : elle rapporte l'engagement commercial total du devis au coût engagé, sans condition, et reste donc renseignée pour tout chantier, y compris ceux qui n'ont encore émis aucune facture. `TauxMargePrevisionnelleHT` (`IF(MontantHTDevis = 0, BLANK(), MargeBrutPrevisionnelleHT / MontantHTDevis)`) applique la même logique en pourcentage.

Cette distinction existe pour couvrir un cas que la seule marge réalisée laisse hors de portée : un chantier tout juste démarré, non encore facturé, a une `MargeBrutHT` vide alors que son coût peut déjà dépasser son devis (chantier prévisionnellement déficitaire dès le démarrage). La marge prévisionnelle permet de le détecter sans attendre la première facture — c'est notamment ce qui alimente le champ `ChantierDeficitaire` et les indicateurs consolidés de la direction (cf. 01_CONTEXTE_INTERFACES_NEOBATI.md, section 3).

`ChantierDeficitaire` (`IF(MargeBrutPrevisionnelleHT < 0, 1, 0)`) est un champ binaire (0/1) dont la seule fonction est de servir de base à un récapitulatif Moyenne côté interface, afin d'obtenir directement un taux de chantiers déficitaires exprimé en pourcentage — conformément à l'indicateur « Taux de chantiers déficitaires » de l'annexe du cahier des charges.

**Distinction entre `Budget` et `MontantHTDevis`.** `Budget` est initialisé automatiquement à la création du chantier avec la valeur du `MontantHTDevis` du devis d'origine (AUT-COM-004), mais reste ensuite **modifiable par le chef de chantier** en cours de réalisation, à titre indicatif pour son propre pilotage opérationnel. `MontantHTDevis`, à l'inverse, reste **figé** : il reflète l'engagement commercial d'origine et n'est jamais modifié après acceptation du devis.

Cette différence explique pourquoi `EcartBudget` (basé sur `Budget`) et `MargeBrutPrevisionnelleHT` (basée sur `MontantHTDevis`) peuvent légitimement diverger sur un même chantier : le premier répond à la question « sommes-nous en train de tenir le budget de travail actuellement fixé par le chef de chantier », le second répond à « quelle marge sur l'engagement commercial d'origine, indépendamment des révisions terrain ». Si un chef de chantier révise `Budget` à la baisse après un dépassement constaté, `EcartBudget` peut redevenir positif pendant que `MargeBrutPrevisionnelleHT` reste dégradée pour le même chantier — ce n'est pas une incohérence entre les deux champs, mais l'expression normale de deux questions différentes.

---

#### Facturation

Les principaux champs sont :

- Montant HT du devis ;
- Montant d'acompte suggéré (`MontantAcompteSuggere`, champ Formule : `{MontantHTDevis} * 0.3`) ;
- Montant HT facturé ;
- Paiements reçus ;
- Reste à facturer ;
- Pourcentage de facturation ;
- Action de facturation à réaliser ;
- Trésorerie nette du chantier ;
- Montant restant à facturer (`ResteAFactureHT`, champ Formule : `MontantHTDevis - {MontantFactureHT}`), exploité par la notification de facture de solde adressée à l'assistante de direction (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md, AUT-FAC-005).

Le montant d'acompte suggéré est calculé à la création du chantier et exploité par la notification adressée à l'assistante de direction (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md, AUT-FAC-001).

Ces indicateurs permettent d'identifier rapidement les chantiers nécessitant une action administrative.

---

#### Intervenants

Le chantier est relié aux équipes qui interviennent sur le terrain.

Les principaux champs sont :

- Artisan responsable ;
- Artisans affectés ;
- Étapes du chantier ;
- Chef de chantier responsable (`ChefChantierResponsable`, champ Utilisateur/Collaborator — pas un champ lié vers une table dédiée) ;
- E-mails des artisans affectés (`ArtisansEmails_ETAPES_Chantier`, champ Cumul).

Ce champ identifie le chef de chantier en charge de la préparation et du suivi du chantier. Il est renseigné manuellement, aucune automatisation n'affecte de chef de chantier automatiquement (cf. domaine Gestion des chantiers, 02_GUIDE_TECHNIQUE_NEOBATI.md). Tant que ce champ est vide, la notification envoyée à la création du chantier (AUT-CHA-002) est adressée à une adresse fixe unique (limitation assumée à ce stade du développement), en attendant qu'une diffusion vers l'ensemble des chefs de chantier soit implémentée — cf. 02_ pour le détail de cette limitation.

**Champ `ArtisansEmails_ETAPES_Chantier` — détail technique.** Champ Cumul (Rollup), source `ETAPES_Chantier`, champ agrégé `EmailArtisan_ARTISAN_Etape` (Lookup créé sur la table Étape, cf. 3.5), formule d'agrégation `ARRAYJOIN(ARRAYCOMPACT(ARRAYUNIQUE(values)), ", ")`. Produit une chaîne unique des e-mails des artisans affectés aux étapes du chantier, dédupliquée (un artisan intervenant sur plusieurs étapes n'apparaît qu'une fois) et sans valeur vide (une étape sans artisan assigné n'introduit pas d'entrée vide dans la liste). Exploité par la notification de démarrage du chantier (AUT-CHA-008, cf. 02_GUIDE_TECHNIQUE_NEOBATI.md).

Point de vigilance retenu lors de la construction : ce champ agrège volontairement `EmailArtisan_ARTISAN_Etape` (Lookup vers le champ texte `Adresse e-mail` de la table Artisan) et non `ArtisanResponsable` (Lookup vers le champ `Collaborateur`, de type Utilisateur). Une agrégation directe de `ArtisanResponsable` produit le nom d'affichage du collaborateur plutôt que son adresse e-mail, les fonctions de formule Airtable convertissant un objet Collaborateur en texte via son nom et non son e-mail.

---

#### Documents

Le chantier conserve également les documents produits pendant sa réalisation.

Il peut notamment être lié à :

- Documents administratifs ;
- Plans ;
- Photos de chantier ;
- Comptes rendus ;
- Rapports terrain.

---

### Relations

La table Chantier est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Client | N → 1 | Le chantier appartient à un client. |
| Devis | 1 → 1 | Chaque chantier est issu d'un devis accepté. |
| Étape | 1 → N | Un chantier est composé de plusieurs étapes. |
| Facture | 1 → N | Plusieurs factures peuvent être émises pour un chantier. |
| Document chantier | 1 → N | Les documents sont rattachés au chantier. |
| Rapport terrain | 1 → N | Les rapports d'avancement concernent un chantier. |
| Artisan | N ↔ N | Plusieurs artisans interviennent sur un chantier via les étapes. |

---

### Principales règles métier

- Un chantier est créé uniquement après acceptation d'un devis.
- Chaque chantier est associé à un seul client.
- Le pourcentage d'avancement est calculé automatiquement à partir des étapes.
- Les indicateurs financiers sont calculés à partir des devis, factures, coûts artisans et coûts matériels.
- Les documents et rapports terrain restent associés au chantier pendant toute sa durée de vie.
- Les indicateurs de retard sont calculés automatiquement à partir du planning des étapes.
- Les actions de facturation sont déterminées automatiquement selon l'état de facturation du chantier.

---

### Utilisation dans les interfaces

La table est utilisée par la majorité des interfaces du projet.

**Direction**

- Suivi de la rentabilité des chantiers ;
- Chantiers en retard.

**Administratif**

- Suivi de la facturation ;
- Chantiers restant à facturer.

**Chargé d'affaires**

- Chantiers en cours ;
- Suivi de l'avancement.

**Chef de chantier**

- Planning des chantiers ;
- Avancement détaillé.

**Artisan**

- Mes chantiers.

**Registre des chantiers**

- Consultation complète de l'ensemble des informations du chantier.

---

### Remarques de conception

La table **Chantier** joue le rôle de table centrale du suivi opérationnel.

Elle ne stocke pas uniquement les informations propres au chantier mais agrège également de nombreux indicateurs calculés provenant des autres tables (Étapes, Factures, Artisans, Documents et Rapports terrain).

Ce choix permet de disposer rapidement de l'ensemble des indicateurs nécessaires au pilotage sans avoir à consulter chaque table individuellement.

Elle constitue ainsi le point d'entrée principal pour le suivi quotidien des projets.

## 3.5 Table Étape

### Objectif

La table **Étape** représente les différentes interventions nécessaires à la réalisation d'un chantier.

Chaque chantier est découpé en plusieurs étapes correspondant aux travaux à réaliser (préparation, électricité, plomberie, peinture, revêtements, réception, etc.).

Cette table constitue le cœur du pilotage opérationnel puisqu'elle permet de planifier les interventions, suivre leur avancement, affecter les artisans, estimer les coûts et gérer les dépendances entre les différentes phases du chantier.

---

### Données gérées

La table regroupe plusieurs catégories d'informations.

#### Informations générales

Ces champs permettent d'identifier une étape.

Ils comprennent notamment :

- Identifiant de l'étape ;
- Nom de l'étape ;
- Description ;
- Chantier associé.

---

#### Planning

Cette catégorie permet d'organiser chronologiquement les travaux.

Les principaux champs sont :

- Date de début prévue ;
- Date de fin prévue ;
- Date de fin réelle ;
- Durée estimée ;
- Statut de l'étape ;
- Étape précédente ;
- Étape suivante.

Les relations entre étapes permettent de respecter l'ordre logique des travaux.

---

#### Suivi d'avancement

Ces champs permettent de suivre l'exécution des travaux.

Ils comprennent notamment :

- Statut (Non commencée, En cours, Terminée) ;
- En retard ;
- Étape terminée (booléen) ;
- Notifié retard (`NotifieRetard`, checkbox coché automatiquement par l'automatisation AUT-CHA-005 une fois la notification de retard envoyée — cf. 02_GUIDE_TECHNIQUE_NEOBATI.md).

Ces indicateurs alimentent automatiquement le suivi global du chantier.

---

#### Affectation des ressources

Chaque étape peut être affectée à un artisan.

Les principaux champs sont :

- Artisan affecté ;
- Artisan responsable — e-mail (`ArtisanResponsable`, champ Recherche sur le champ `Collaborateur` de la table Artisan, via le lien `ARTISANT_Etape`) ;
- Chef de chantier responsable — e-mail (`ChefChantierResponsable_CHANTIER_Etape`, champ Recherche sur le champ `ChefChantierResponsable` de la table Chantier, via le lien `CHANTIER_Etape`) ;
- Artisan affecté — e-mail (`EmailArtisan_ARTISAN_Etape`, champ Recherche sur le champ `Adresse e-mail` de la table Artisan, via le lien `ARTISANT_Etape`) ;
- Coût journalier de l'artisan ;
- Nombre de jours occupés.

Ces informations facilitent la planification des équipes.

**Champ `EmailArtisan_ARTISAN_Etape` — justification.** Distinct d'`ArtisanResponsable`, qui expose le champ `Collaborateur` (type Utilisateur) de l'Artisan lié. Ce nouveau champ expose à la place le champ texte `Adresse e-mail` de l'Artisan — nécessaire car un champ Cumul (Rollup) agrégeant `ArtisanResponsable` sur plusieurs Étapes liées ne peut restituer que le nom d'affichage du collaborateur, pas son adresse e-mail (cf. 3.4, remarque sur `ArtisansEmails_ETAPES_Chantier`). Consommé uniquement par ce Rollup au niveau du Chantier, pour AUT-CHA-008.

---

#### Matériel

Chaque étape peut nécessiter plusieurs matériaux.

Les principaux champs sont :

- Quantités de matériel associées ;
- Coût total du matériel.

Les détails des matériaux sont stockés dans la table **Quantité Matériel**.

---

#### Coûts

Les coûts de chaque étape sont calculés automatiquement.

Les principaux indicateurs sont :

- Coût de la main-d'œuvre ;
- Coût des matériaux ;
- Coût total de l'étape.

Ces valeurs alimentent ensuite les indicateurs financiers du chantier.

---

#### Documents

Une étape peut être liée à différents documents :

- Photos ;
- Plans ;
- Comptes rendus ;
- Documents techniques.

---

#### Rapports terrain

Les rapports rédigés par les artisans sont rattachés à l'étape concernée.

Ils permettent de conserver un historique des interventions réalisées.

---

### Relations

La table Étape est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Chantier | N → 1 | Chaque étape appartient à un chantier. |
| Artisan | N → 1 | Une étape est généralement affectée à un artisan. |
| Quantité Matériel | 1 → N | Une étape peut utiliser plusieurs matériaux. |
| Rapport terrain | 1 → N | Les rapports concernent une étape. |
| Document chantier | 1 → N | Les documents peuvent être rattachés à une étape. |
| Étape | Auto-relation | Gestion des dépendances entre étapes (prédécesseur / successeur). |

---

### Principales règles métier

- Une étape appartient obligatoirement à un chantier.
- Une étape peut être affectée à un ou plusieurs artisans.
- Une étape ne peut être terminée qu'après validation des travaux réalisés.
- Les dépendances permettent d'imposer un ordre d'exécution entre certaines étapes.
- Les coûts de l'étape sont calculés automatiquement à partir du coût de l'artisan et des matériaux consommés.
- Les rapports terrain et les documents restent associés à l'étape concernée.
- Les informations d'avancement alimentent automatiquement les indicateurs du chantier.

---

### Utilisation dans les interfaces

La table est utilisée par plusieurs profils.

**Chef de chantier**

- Planning des étapes ;
- Étapes non affectées ;
- Étapes en cours ;
- Étapes à venir ;
- Étapes en retard.

**Artisan**

- Mes étapes à réaliser ;
- Consultation des informations d'intervention ;
- Dépôt de rapports terrain.

**Direction**

- Analyse des coûts par étape.

---

### Remarques de conception

La table **Étape** constitue l'unité opérationnelle de la base NeoBati.

Le chantier représente le projet dans son ensemble tandis que les étapes représentent les interventions concrètes réalisées sur le terrain.

Le choix d'utiliser une relation d'auto-référence entre les étapes (prédécesseur / successeur) permet de modéliser simplement les dépendances entre les différentes phases des travaux sans avoir recours à un outil de planification externe.

Les coûts calculés au niveau des étapes sont ensuite agrégés dans la table **Chantier**, ce qui permet de suivre précisément la rentabilité de chaque projet.

## 3.6 Table Rapport terrain

### Objectif

La table **Rapport terrain** centralise les comptes rendus rédigés par les artisans ou les chefs de chantier lors de l'exécution des travaux.

Chaque rapport est associé à une étape et à un chantier afin de conserver un historique détaillé des interventions réalisées sur le terrain.

Cette table facilite le suivi quotidien des chantiers, la remontée des problèmes rencontrés et la validation des interventions par le chef de chantier.

---

### Données gérées

La table regroupe plusieurs catégories d'informations.

#### Informations générales

Les principaux champs sont :

- Identifiant du rapport ;
- Auteur du rapport ;
- Date et heure de création ;
- Type de rapport.

Le type de rapport permet notamment de distinguer différents comptes rendus (par exemple : compte rendu quotidien, rapport d'incident, visite de contrôle, etc.).

---

#### Rattachement

Chaque rapport est associé aux éléments suivants :

- Chantier concerné ;
- Étape concernée.

Cette relation permet de retrouver rapidement l'ensemble des rapports liés à une intervention ou à un chantier.

---

#### Compte rendu

Cette partie contient les informations saisies par l'artisan.

Les principaux champs sont :

- Description de l'intervention réalisée ;
- Problème bloquant (Oui / Non) ;
- Description du problème éventuel ;
- Résumé généré par IA (`ResumeIA`, champ Texte long, alimenté automatiquement à la création du rapport — cf. AUT-IA-001, 02_GUIDE_TECHNIQUE_NEOBATI.md) ;
- Points de suivi suggérés par IA (`PointsSuiviIA`, champ Texte long, alimenté automatiquement à la création du rapport — cf. AUT-IA-001, 02_GUIDE_TECHNIQUE_NEOBATI.md) ;
- Chef de chantier responsable — e-mail (`ChefChantierResponsable_CHANTIER_Rapport`, champ Recherche sur le champ `ChefChantierResponsable` de la table Chantier, via le lien natif vers Chantier).

Ces informations permettent au chef de chantier de suivre l'avancement réel des travaux.

---

#### Validation

Après consultation du rapport, le chef de chantier peut :

- Valider le rapport ;
- Ajouter des remarques ou des commentaires.

Cette validation permet d'assurer un suivi qualité des interventions réalisées.

---

#### Documents associés

Un rapport peut être lié à plusieurs documents stockés dans la table **Document chantier**, notamment :

- Photos d'avancement ;
- Photos d'anomalies ;
- Documents techniques ;
- Autres pièces justificatives.

---

### Relations

La table Rapport terrain est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Chantier | N → 1 | Chaque rapport concerne un chantier. |
| Étape | N → 1 | Chaque rapport est associé à une étape. |
| Document chantier | 1 → N | Plusieurs documents peuvent illustrer un rapport. |

---

### Principales règles métier

- Un rapport est toujours rattaché à un chantier.
- Un rapport est généralement associé à une étape précise.
- Un rapport peut signaler un problème bloquant.
- Les documents associés permettent d'illustrer l'état d'avancement des travaux.
- Les remarques du chef de chantier complètent le rapport initial sans modifier son contenu.

---

### Utilisation dans les interfaces

La table est principalement utilisée par les profils suivants.

**Artisan**

- Déposer un compte rendu d'intervention ;
- Signaler un problème rencontré ;
- Ajouter des photos ou documents.

**Chef de chantier**

- Consulter les rapports du chantier ;
- Valider les comptes rendus ;
- Ajouter des observations.

---

### Remarques de conception

Cette table constitue un historique des interventions réalisées sur le terrain.

Son modèle de données a volontairement été conçu de manière simple afin de pouvoir être enrichi ultérieurement par des automatisations.

Par exemple, un rapport pourra à terme :

- notifier automatiquement le chef de chantier lorsqu'un problème bloquant est signalé ;
- générer un résumé quotidien des interventions réalisées ;
- mettre à jour automatiquement le statut d'une étape après validation ;
- alimenter un historique complet des interventions sur chaque chantier.

## 3.7 Table Artisan

### Objectif

La table **Artisan** centralise l'ensemble des ressources humaines intervenant sur les chantiers de NeoBati.

Chaque enregistrement représente un artisan pouvant être affecté à une ou plusieurs étapes de chantier.

Cette table est utilisée pour :

- planifier les interventions ;
- suivre la disponibilité des artisans ;
- calculer les coûts de main-d'œuvre ;
- faciliter l'affectation des ressources sur les chantiers.

---

### Données gérées

Les informations sont organisées en plusieurs catégories.

#### Informations générales

Les principaux champs sont :

- Identifiant de l'artisan ;
- Nom ;
- Téléphone ;
- Adresse e-mail.

Ces informations permettent d'identifier rapidement chaque intervenant.

---

#### Compétences

Chaque artisan possède une compétence principale représentée par un champ à sélection unique.

Exemples de compétences :

- Menuiserie ;
- Électricité ;
- Peinture ;
- Plomberie ;
- Plâtrerie ;
- Revêtement de sol.

Cette information facilite l'affectation des artisans aux étapes correspondant à leur domaine d'expertise.

---

#### Disponibilité

La table contient un champ indiquant la disponibilité actuelle de chaque artisan.

Les principaux statuts sont :

- Disponible ;
- Occupé.

Cette information permet au chef de chantier de connaître rapidement les ressources mobilisables.

---

#### Informations financières

Chaque artisan possède un coût journalier utilisé dans le calcul des coûts de chantier.

Ce coût est réutilisé automatiquement dans les calculs des étapes puis du chantier afin d'estimer le coût global de la main-d'œuvre.

---

#### Affectations

Chaque artisan peut être associé à plusieurs étapes.

Les principaux champs liés aux affectations sont :

- Étapes attribuées ;
- Nombre d'étapes en cours.

Ces informations permettent d'évaluer rapidement la charge de travail de chaque ressource.

---

#### Notes

Un champ libre permet de conserver diverses informations concernant l'artisan :

- spécialités ;
- remarques ;
- contraintes particulières ;
- observations internes.

---

### Relations

La table Artisan est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Étape | 1 → N | Un artisan peut intervenir sur plusieurs étapes. |

---

### Principales règles métier

- Un artisan possède une compétence principale.
- Un artisan peut intervenir sur plusieurs étapes.
- Une étape ne peut être affectée qu'à un seul artisan responsable.
- Le coût journalier est utilisé dans le calcul du coût des étapes.
- Le statut de disponibilité permet d'identifier rapidement les ressources disponibles.

---

### Utilisation dans les interfaces

La table est principalement utilisée par les profils suivants.

**Chef de chantier**

- Consulter les artisans disponibles ;
- Affecter un artisan à une étape ;
- Rééquilibrer la charge de travail.

**Direction**

- Consulter les ressources mobilisées ;
- Analyser les coûts de main-d'œuvre.

---

### Remarques de conception

Le champ **Disponibilité actuelle** est volontairement simplifié et reflète uniquement l'état de disponibilité au moment de la consultation.

La planification réelle des interventions est assurée à partir des dates prévues des étapes de chantier, qui permettent de connaître précisément les périodes d'affectation des artisans.

**Champ Collaborateur — état actuel.** Chaque artisan dispose d'un champ `Collaborateur` (Utilisateur Airtable) qui pilote le filtrage de l'interface Artisans – Mobile terrain (cf. 01_CONTEXTE_INTERFACES_NEOBATI.md, page « Mes étapes »). Dans le jeu de données de démonstration, tous les artisans pointent vers un même collaborateur ; en production, chaque artisan devra être associé à son propre compte pour que chacun ne voie que ses interventions.

À terme, cette table pourra être enrichie par plusieurs automatisations, notamment :

- mise à jour automatique de la disponibilité selon les étapes planifiées ;
- détection des conflits de planning ;
- proposition automatique de l'artisan le plus adapté selon sa compétence et sa disponibilité ;
- calcul automatique de la charge de travail de chaque artisan.

## 3.8 Table Matériel

### Objectif

La table **Matériel** centralise l'ensemble des matériaux, fournitures et équipements utilisés sur les chantiers NeoBati.

Chaque enregistrement représente une ressource matérielle pouvant être utilisée dans une ou plusieurs étapes de chantier.

Cette table permet notamment de :

- constituer un catalogue des matériaux utilisés par l'entreprise ;
- estimer le coût des travaux ;
- calculer automatiquement le coût des étapes et des chantiers ;
- éviter les doublons de matériaux dans la base.

---

### Données gérées

Les informations sont organisées en plusieurs catégories.

#### Informations générales

Les principaux champs sont :

- Nom du matériel ;
- Catégorie ;
- Unité de mesure.

Chaque matériel est unique dans la base afin de constituer un référentiel commun à l'ensemble des chantiers.

---

#### Catégorisation

Chaque matériel appartient à une catégorie facilitant son identification.

Exemples de catégories :

- Préparation ;
- Plâtrerie ;
- Peinture ;
- Électricité ;
- Revêtement ;
- Plomberie ;
- Outillage.

Cette classification facilite les recherches et les analyses de coûts.

---

#### Unité de mesure

Chaque matériel possède une unité de mesure correspondant à son mode d'utilisation.

Exemples :

- unité ;
- mètre linéaire (ml) ;
- m² ;
- kilogramme (kg) ;
- litre ;
- sac ;
- lot ;
- location (prix journalier).

Cette information est utilisée lors de l'estimation des quantités nécessaires pour une étape.

---

#### Informations financières

Chaque matériel possède un coût unitaire.

Ce coût est utilisé dans les calculs automatiques des coûts de matériaux des étapes, puis du coût global des chantiers.

---

#### Notes

Un champ libre permet d'ajouter des informations complémentaires telles que :

- caractéristiques techniques ;
- conseils d'utilisation ;
- remarques internes.

---

#### Utilisation sur les chantiers

La table contient également les liens vers les enregistrements de la table **Quantité Matériel**.

Ces relations permettent d'identifier les différentes étapes utilisant un même matériau.

---

### Relations

La table Matériel est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Quantité Matériel | 1 → N | Un matériel peut être utilisé plusieurs fois sur différentes étapes. |

---

### Principales règles métier

- Un matériel n'est créé qu'une seule fois dans le catalogue.
- Les quantités utilisées ne sont pas stockées dans cette table.
- Le coût unitaire sert de référence pour tous les calculs financiers.
- Un même matériel peut être utilisé sur plusieurs étapes et plusieurs chantiers.

---

### Utilisation dans les interfaces

La table est principalement utilisée par les profils suivants.

**Administratif**

- Créer et maintenir le référentiel matériel (nom, catégorie, unité, coût unitaire) via la page "Liste des matériaux chantier" ;
- Ajuster le coût unitaire en cas de variation de prix fournisseur.

**Chargé d'affaires**

- Constituer le chiffrage d'un devis ;
- Estimer le coût des matériaux.

**Chef de chantier**

- Consulter les matériaux prévus sur une étape ;
- Sélectionner un matériau existant du référentiel lors de l'ajout de matériel à une étape ;
- Vérifier les ressources nécessaires avant intervention.

**Direction**

- Analyser les coûts des matériaux par chantier.

---

### Remarques de conception

Cette table constitue un référentiel des matériaux de l'entreprise. La création et la mise à jour du référentiel sont centralisées auprès de l'assistante de direction (interface Administratif), ce qui évite toute manipulation directe de la grille par les autres profils utilisateurs.

La gestion des quantités a volontairement été séparée dans la table **Quantité Matériel** afin de respecter le principe de normalisation des données.

Chaque ligne de la table **Quantité Matériel** représente l'utilisation d'un matériel donné sur une étape précise avec une quantité définie.

Cette séparation évite la duplication des matériaux et facilite les calculs de coûts ainsi que les futures automatisations.

## 3.9 Table Quantité Matériel

### Objectif

La table **Quantité Matériel** constitue une table de liaison entre les tables **Étape** et **Matériel**.

Chaque enregistrement représente l'utilisation d'un matériel spécifique pour une étape donnée, en indiquant la quantité nécessaire ainsi que le coût correspondant.

Cette table permet notamment de :

- associer plusieurs matériaux à une même étape ;
- définir les quantités réellement nécessaires ;
- calculer automatiquement le coût des matériaux par étape ;
- consolider les coûts des chantiers.

---

### Données gérées

Les informations sont réparties en plusieurs catégories.

#### Références

Chaque enregistrement possède un identifiant unique permettant d'identifier une utilisation précise d'un matériel.

---

#### Matériel associé

Chaque ligne est reliée à un unique matériel provenant de la table **Matériel**.

Les informations principales du matériel (nom, unité et coût unitaire) sont récupérées automatiquement grâce aux champs liés et aux champs Lookup.

---

#### Quantité utilisée

La quantité représente le volume réellement utilisé pour une étape.

Selon le type de matériel, cette quantité peut correspondre à :

- un nombre d'unités ;
- des mètres linéaires ;
- des mètres carrés ;
- des kilogrammes ;
- des litres ;
- un lot ;
- une durée de location.

---

#### Coût du matériel

Le coût est calculé automatiquement à partir :

- du coût unitaire du matériel ;
- de la quantité utilisée.

Cette valeur est ensuite utilisée pour calculer le coût total de chaque étape puis du chantier.

---

#### Liaison avec les étapes

Chaque enregistrement est obligatoirement associé à une étape.

Une étape peut contenir autant de lignes de matériaux que nécessaire.

---

#### Liaison avec les chantiers

Le chantier est récupéré automatiquement via la relation avec l'étape.

Cette liaison facilite les analyses et les calculs de coûts sans nécessiter de relation supplémentaire.

---

#### Notes

Un champ libre permet d'ajouter des remarques particulières concernant l'utilisation du matériel.

Exemples :

- matériau de remplacement ;
- quantité exceptionnelle ;
- remarque du conducteur de travaux.

---

### Relations

La table Quantité Matériel est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Matériel | N → 1 | Chaque ligne référence un unique matériel. |
| Étape | N → 1 | Chaque ligne est rattachée à une étape. |
| Chantier | N → 1 (indirecte) | Le chantier est récupéré automatiquement via l'étape associée. |

---

### Principales règles métier

- Une ligne correspond à un seul matériel utilisé sur une seule étape.
- Une étape peut contenir plusieurs matériaux.
- Un même matériel peut être utilisé sur plusieurs étapes.
- Le coût est calculé automatiquement à partir du coût unitaire et de la quantité.
- Les informations descriptives du matériel sont récupérées automatiquement depuis la table Matériel.

---

### Utilisation dans les interfaces

La table est principalement utilisée par les profils suivants.

**Chargé d'affaires**

- Estimer les besoins matériels d'un devis ;
- Évaluer le coût des matériaux.

**Chef de chantier**

- Consulter les matériaux nécessaires à chaque étape ;
- Ajuster les quantités si nécessaire.

**Direction**

- Analyser les coûts détaillés des matériaux par chantier.

---

### Remarques de conception

Cette table constitue une **table de liaison** entre les tables **Matériel** et **Étape**.

Le matériel est volontairement stocké dans une table indépendante afin d'éviter la duplication des données.

Les informations telles que le nom du matériel, son unité ou son coût unitaire sont récupérées automatiquement via les relations Airtable.

Cette modélisation facilite les calculs financiers, garantit l'intégrité des données et permet à un même matériau d'être réutilisé sur un nombre illimité d'étapes sans créer de doublons.

## 3.10 Table Facture

### Objectif

La table **Facture** centralise l'ensemble des factures émises par NeoBati dans le cadre des différents chantiers.

Elle permet de gérer le cycle complet de facturation, depuis la création d'une facture jusqu'à son paiement, tout en assurant le suivi des montants encaissés, des échéances et des éventuelles relances.

Les données de cette table alimentent également les indicateurs financiers présents dans les tableaux de bord de la direction et du service administratif.

---

### Données gérées

Les informations sont réparties en plusieurs catégories.

#### Identification

Chaque facture possède un identifiant unique facilitant son suivi administratif.

---

#### Liaisons métier

Chaque facture est associée à :

- un devis ;
- un chantier ;
- un client.

Ces relations permettent de retrouver rapidement le contexte commercial et opérationnel de chaque facture.

---

#### Informations financières

La table enregistre notamment :

- le montant HT ;
- le taux de TVA ;
- le montant de TVA ;
- le montant TTC.

Ces montants sont calculés automatiquement afin de garantir la cohérence des données financières.

---

#### Suivi des paiements

Pour chaque facture, la base suit :

- le montant déjà encaissé ;
- le montant restant à encaisser (HT et TTC) ;
- le statut du paiement.

Ce suivi permet de connaître en permanence la trésorerie effectivement encaissée ainsi que les sommes restant dues.

Le montant restant à encaisser TTC (`ResteAEncaisserTTC`, Formule : `{ResteAEncaisserHT} * (1 + {TVA})`) est utilisé dans les communications de relance adressées au client et dans l'alerte interne de recouvrement (cf. AUT-FAC-002).

---

#### Gestion des échéances

Chaque facture comporte plusieurs dates importantes :

- date de création ;
- date d'émission ;
- date d'échéance ;
- date de dernière relance.

Ces informations servent au calcul automatique des retards de paiement.

Un champ Formule (`JoursRetardFac`) calcule le nombre de jours de retard par rapport à la date d'échéance. Il alimente le calcul automatique du champ `Statut` ainsi que le contenu des e-mails de relance.

---

#### Statut de la facture

Le statut est calculé automatiquement (champ Formule) à partir du statut de paiement, de l'indicateur de retard et d'une case à cocher manuelle réservée à l'annulation.

Les valeurs possibles sont :

- Émise ;
- Partiellement payée ;
- En retard : partiellement payée ;
- En retard : impayée ;
- Payée ;
- Annulée.

Seule l'annulation reste une décision manuelle (champ `Annulee`, Case à cocher) : une facture ne peut être identifiée comme annulée par aucune combinaison de dates ou de montants, cette décision relevant du jugement de l'assistante de direction.

Le statut est automatiquement utilisé dans les tableaux de bord et les vues de suivi.

---

#### Statut de paiement

Le paiement est suivi indépendamment du statut administratif de la facture.

Les principaux états sont :

- Non payée ;
- Partiellement payée ;
- Payée.

Cette distinction permet de suivre précisément les règlements clients.

---

#### Type de facture

Chaque facture porte un type (`TypeFacture`) : Acompte, Solde ou Correction / complément. Cette information distingue la nature de la facture sans conditionner aucune automatisation du domaine — les relances et notifications s'appliquent identiquement aux trois types (cf. AUT-FAC-002).

---

#### Relances

La table dispose d'un champ Formule (`FacARelancer`) identifiant automatiquement les factures devant être relancées : facture non annulée, reste à encaisser positif, et échéance dépassée sans relance encore effectuée ou dernière relance datant d'au moins 15 jours.

Un compteur (`NombreRelances`) et une date de dernière relance (`DateDerniereRelance`) permettent de piloter la cadence et le registre des messages de relance. Aucun plafond n'est appliqué : la relance se poursuit jusqu'au règlement intégral (cf. AUT-FAC-002).

Deux champs Lookup complètent ces informations pour les besoins de l'automatisation de relance : le nom du client (`Nom_CLIENT_Facture`) et son adresse e-mail (`Email_CLIENT_Facture`), utilisés lors de l'envoi de l'e-mail de relance (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md, AUT-FAC-002).

---

#### Commentaires

Un champ de notes permet d'ajouter des informations complémentaires concernant la facturation ou les échanges avec le client.

Exemples :

- acompte reçu ;
- accord de paiement échelonné ;
- commentaire administratif.

---

### Relations

La table Facture est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Devis | N → 1 | Une facture est issue d'un devis validé. |
| Chantier | N → 1 | Le chantier est récupéré automatiquement via le devis. |
| Client | N → 1 | Le client est récupéré automatiquement afin de faciliter le suivi financier. |

---

### Principales règles métier

- Une facture est obligatoirement liée à un devis.
- Un devis peut générer plusieurs factures (acomptes, facture intermédiaire, solde).
- Les montants TTC sont calculés automatiquement à partir du montant HT et de la TVA.
- Le montant restant à encaisser est recalculé automatiquement après chaque paiement.
- Les factures en retard sont identifiées automatiquement selon leur échéance.
- Les indicateurs financiers de la direction sont alimentés à partir de cette table.

---

### Utilisation dans les interfaces

La table est principalement utilisée par les profils suivants.

**Administratif**

- Créer les factures.
- Suivre les échéances.
- Enregistrer les paiements.
- Effectuer les relances.

**Direction**

- Consulter le chiffre d'affaires encaissé.
- Suivre la trésorerie.
- Identifier les retards de paiement.
- Analyser la rentabilité globale.

**Chargé d'affaires**

- Consulter l'état de facturation des chantiers.
- Vérifier les acomptes et les soldes.

---

### Remarques de conception

La facturation est volontairement séparée des devis afin de permettre plusieurs scénarios de facturation :

- acompte avant démarrage ;
- facturation intermédiaire ;
- facture de solde ;
- paiements partiels.

Cette modélisation offre une meilleure flexibilité qu'une relation 1:1 entre devis et facture et reflète davantage le fonctionnement réel d'une entreprise du bâtiment.

Les principaux indicateurs financiers (montant encaissé, reste à encaisser, trésorerie, rentabilité) sont ensuite consolidés à partir des données de cette table.

## 3.11 Table Document chantier

### Objectif

La table **Document chantier** centralise l'ensemble des documents liés aux chantiers réalisés par NeoBati.

Elle permet de stocker aussi bien les documents administratifs que les documents produits sur le terrain (photos, plans, comptes rendus, procès-verbaux, etc.) afin de disposer d'un historique complet de chaque projet.

Cette table constitue le référentiel documentaire unique de la base Airtable.

---

### Données gérées

Les informations sont réparties en plusieurs catégories.

#### Identification

Chaque document possède un identifiant unique permettant de le retrouver rapidement.

---

#### Informations du document

Chaque enregistrement contient notamment :

- le nom du document ;
- le fichier importé dans Airtable ;
- le type de document.

Le type permet de distinguer différents documents tels que :

- Devis signé ;
- Facture ;
- Plan ;
- Photo chantier ;
- Compte rendu ;
- Autre.

---

#### Catégorie

Chaque document est classé dans une catégorie métier.

Les principales catégories sont :

- Administratif ;
- Terrain.

Cette classification facilite la recherche des documents dans les interfaces.

---

#### Description

Une description libre permet de préciser le contenu du document ou son contexte.

Exemples :

- Photos avant démolition.
- Bon de commande fournisseur.
- Procès-verbal de réception.
- État d'avancement des travaux.

---

#### Date et auteur

Chaque document enregistre :

- sa date d'ajout ;
- le collaborateur ayant importé le document.

Ces informations assurent une meilleure traçabilité.

---

#### Visibilité client

Un indicateur permet de définir si le document peut être partagé avec le client.

Cette distinction permet de différencier :

- les documents strictement internes ;
- les documents pouvant être consultés ou transmis au client.

---

### Relations

La table Document chantier est reliée aux tables suivantes.

| Table liée | Relation | Description |
|------------|----------|-------------|
| Chantier | N → 1 | Chaque document est rattaché à un chantier. |
| Étape | N → 1 (optionnelle) | Un document peut être associé à une étape précise du chantier. |
| Rapport terrain | N → 1 (optionnelle) | Certains documents proviennent directement d'un rapport terrain. |

---

### Principales règles métier

- Un document est toujours rattaché à un chantier.
- Un document peut être lié à une étape spécifique lorsque celui-ci concerne une intervention précise.
- Les photographies d'avancement sont généralement associées aux étapes concernées.
- Les documents administratifs peuvent être uniquement liés au chantier.
- Les documents issus des rapports terrain conservent un lien vers le rapport ayant généré leur création.
- Le champ "VisibleClient" permet de contrôler les documents pouvant être partagés avec le client.

---

### Utilisation dans les interfaces

La table est principalement utilisée par les profils suivants.

**Chefs de chantier**

- Ajouter des photos du chantier.
- Déposer des comptes rendus.
- Archiver les documents terrain.

**Chargé d'affaires**

- Consulter les plans.
- Retrouver les devis signés.
- Accéder aux documents techniques.

**Administratif**

- Stocker les documents contractuels.
- Archiver les factures.
- Conserver les documents officiels.

**Direction**

- Consulter l'ensemble des documents d'un chantier.
- Vérifier l'historique documentaire.
- Contrôler les justificatifs.

---

### Remarques de conception

La gestion documentaire a été volontairement centralisée dans une table unique plutôt que de créer plusieurs tables spécialisées (Photos, Plans, Factures, etc.).

Cette approche présente plusieurs avantages :

- un seul espace de stockage pour tous les documents ;
- une recherche simplifiée ;
- une meilleure évolutivité ;
- une réduction de la duplication des données.

La distinction entre les différents usages est assurée par les champs **Type**, **Catégorie** et **VisibleClient**, qui permettent de filtrer les documents selon les besoins des différents profils utilisateurs.

## 3.12 Interaction client

Cette table conserve une trace des interactions automatisées envoyées aux clients, afin de répondre à l'exigence d'historisation des interactions clients du cahier des charges. Elle vient en complément des champs `NombreRelances` et `DateDerniereRelance` présents sur Devis et Facture, qui ne conservent qu'un compteur et une date, sans le contenu du message envoyé.

Les principaux champs sont :

- Identifiant de l'interaction (`InteractionID`) ;
- Type d'interaction (`TypeInteraction`) : Relance devis ou Relance facture ;
- Client concerné (`CLIENT_Interaction`, lien vers Client) ;
- Devis concerné (`DEVIS_Interaction`, lien vers Devis, renseigné uniquement pour une relance devis) ;
- Facture concernée (`FACTURE_Interaction`, lien vers Facture, renseignée uniquement pour une relance facture) ;
- Canal utilisé (`Canal`) : Email, seul canal actif à ce jour (cf. 02_GUIDE_TECHNIQUE_NEOBATI.md, section 9.7, note sur le canal SMS) ;
- Contenu du message envoyé (`ContenuEnvoye`) ;
- Date d'envoi (`DateEnvoi`) ;
- Numéro de la relance (`NumeroRelance`), correspondant au rang de la relance au moment de l'envoi.

**Remarque de conception — fidélité du contenu conservé.** Le champ `ContenuEnvoye` restitue le contenu informationnel intégral du message envoyé, avec une mise en forme simplifiée : les sauts de ligne internes au corps du message, présents dans l'e-mail reçu par le client, ne sont pas reproduits dans ce champ. Ce choix est délibéré : il évite de dupliquer dans Airtable la logique de mise en forme HTML propre au module d'envoi (cf. 02_, conventions Make, gestion du formatage HTML), pour un gain de fidélité jugé marginal au regard de l'usage visé — retrouver ce qui a été communiqué à un client, non reproduire à l'identique la présentation de l'e-mail reçu.

**Périmètre.** Seules les communications adressées directement à un client sont historisées dans cette table. Les notifications internes générées par les mêmes automatisations (alerte à l'assistante ou au chargé d'affaires en cas de relances sans réponse, par exemple) n'y figurent pas, celles-ci ne constituant pas une interaction avec le client.

Un enregistrement est créé automatiquement à chaque relance envoyée avec succès par AUT-COM-003 et AUT-FAC-002 (cf. 02_, sections correspondantes).