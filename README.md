> **Ce dépôt contient la documentation technique complète d'un système
> d'automatisation Airtable + Make + IA, conçu de bout en bout pour une
> entreprise fictive du secteur du bâtiment.**
>
> 23 automatisations planifiées, 14 construites, 9 abandonnées après
> analyse — chaque décision et chaque abandon est documenté avec son
> raisonnement.
>
> Contexte, architecture et décisions principales, en version lisible :
> [lyven.io/documentation-neobati](https://lyven.io/documentation-neobati.html)
>
> Nicolas Gamard — [lyven.io](https://lyven.io)

> ## Utilisation de cette documentation
>
> Cette documentation constitue la référence officielle du projet NeoBati.
>
> Avant de proposer une évolution du projet :
>
> 1. Lire ce README afin de comprendre l'organisation de la documentation.
> 2. Identifier le document contenant les informations recherchées.
> 3. Respecter les conventions définies dans `02_GUIDE_TECHNIQUE_NEOBATI.md`.
> 4. Considérer les documents de contexte comme la référence fonctionnelle du projet.
> 5. Toute évolution significative devra être répercutée dans la documentation concernée.


# README_NEOBATI

## Documentation de référence du projet NeoBati

**Version :** 1.1

---

# 1. Présentation

NeoBati est un projet de démonstration réalisé dans le cadre de la certification **Déployer des systèmes automatisés (IA, Airtable, Make)**.

Le projet consiste à concevoir un système d'information complet destiné à une entreprise fictive du secteur du bâtiment.

L'objectif n'est pas uniquement de construire une base Airtable, mais de concevoir une architecture métier complète intégrant :

- une base de données relationnelle ;
- des interfaces adaptées aux différents profils utilisateurs ;
- des formulaires de saisie ;
- des automatisations avec Make ;
- des traitements utilisant un modèle d'intelligence artificielle ;
- une organisation documentaire cohérente.

L'ensemble du projet est documenté afin de garantir sa compréhension, sa maintenabilité et son évolutivité.

## Public concerné

Cette documentation est destinée :

- aux développeurs reprenant le projet ;
- aux concepteurs d'automatisations ;
- aux évaluateurs du projet ;
- aux modèles de langage (LLM) utilisés comme assistants de développement.

---

# 2. Architecture générale du projet

Le projet repose sur une séparation claire des responsabilités entre les différents composants.

```text
                    Utilisateurs
                          │
                          ▼
                Interfaces Airtable
                          │
                          ▼
                 Base Airtable (référentiel)
                          │
                          ▼
                 Automatisations Make
                          │
        ┌─────────────────┴─────────────────┐
        ▼                                   ▼
      Gmail                                 LLM
                          │
                          ▼
                 Retour des données
                    dans Airtable
```

Principes retenus :

- Airtable constitue le référentiel unique des données.
- Les interfaces sont le point d'entrée des utilisateurs.
- Make orchestre les processus métier.
- Les services externes sont appelés uniquement par Make.
- Les modèles d'intelligence artificielle interviennent uniquement pour les traitements non déterministes.

## 2.1 Technologies utilisées

Le projet NeoBati repose sur les technologies suivantes.

| Technologie | Rôle |
|--------------|------|
| Airtable | Base de données relationnelle, interfaces et formulaires |
| Make | Orchestration des automatisations |
| LLM | Analyse et génération de contenu |

---

# 3. Organisation de la documentation

La documentation du projet est répartie en plusieurs documents complémentaires.

Ils doivent être consultés dans l'ordre suivant.

| Ordre | Document | Contenu |
|-------:|----------|---------|
| 1 | **README_NEOBATI.md** | Vue d'ensemble du projet et organisation de la documentation. |
| 2 | **00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md** | Architecture de la base Airtable, tables, relations et règles métier. |
| 3 | **01_CONTEXTE_INTERFACES_NEOBATI.md** | Interfaces Airtable, formulaires et parcours utilisateurs. |
| 4 | **02_GUIDE_TECHNIQUE_NEOBATI.md** | Architecture technique, conventions et bonnes pratiques de développement. |

Chaque document possède un rôle spécifique et évite les redondances avec les autres.

Les informations ne sont volontairement pas dupliquées entre les documents.

Chaque sujet est documenté dans un seul document de référence afin de faciliter la maintenance et de garantir la cohérence de la documentation.

---

# 4. Où trouver l'information ?

Le tableau ci-dessous indique dans quel document rechercher une information selon le besoin.

| Si vous recherchez... | Document à consulter |
|------------------------|----------------------|
| Une table Airtable | 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md |
| Une relation entre deux tables | 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md |
| Une règle métier | 00_CONTEXTE_BASE_AIRTABLE_NEOBATI.md |
| Une interface utilisateur | 01_CONTEXTE_INTERFACES_NEOBATI.md |
| Un formulaire | 01_CONTEXTE_INTERFACES_NEOBATI.md |
| Le parcours d'un utilisateur | 01_CONTEXTE_INTERFACES_NEOBATI.md |
| Une convention de nommage | 02_GUIDE_TECHNIQUE_NEOBATI.md |
| Une bonne pratique Airtable | 02_GUIDE_TECHNIQUE_NEOBATI.md |
| Une bonne pratique Make | 02_GUIDE_TECHNIQUE_NEOBATI.md |
| Une règle de modélisation | 02_GUIDE_TECHNIQUE_NEOBATI.md |
| L'architecture des automatisations | 02_GUIDE_TECHNIQUE_NEOBATI.md |

---

# 5. Principes de maintenance de la documentation

Cette documentation constitue la référence officielle du projet NeoBati.

Toute évolution du projet doit respecter les principes suivants :

- conserver une séparation claire entre les données, les interfaces et les automatisations ;
- documenter toute évolution importante ;
- maintenir la cohérence entre les différents documents ;
- privilégier les fonctionnalités natives avant les développements plus complexes ;
- respecter les conventions définies dans le guide technique.

---

# 6. État d'avancement du projet

La documentation couvre actuellement les éléments suivants.

| Élément | Statut |
|----------|:------:|
| Architecture de la base Airtable | ✅ Documentée |
| Interfaces Airtable | ✅ Documentées |
| Guide technique | ✅ Documenté |
| Automatisations Make | ✅ Implémentées et documentées |
| Prompts IA | ✅ Documentés |
| Jeu de données de démonstration | ✅ Préparé pour la soutenance |

Ce document évoluera au fur et à mesure de l'avancement du projet.

---

## Cycle de mise à jour

La documentation doit évoluer en parallèle du projet.

Toute modification significative de la base Airtable, des interfaces ou des automatisations devra être répercutée dans le ou les documents concernés afin de maintenir la cohérence de l'ensemble documentaire.

# Conclusion

Le présent fichier constitue le point d'entrée de la documentation NeoBati.

Il a pour objectif de faciliter la navigation entre les différents documents et de fournir une vision globale de l'architecture du projet avant d'aborder les aspects fonctionnels ou techniques.

Pour toute nouvelle contribution au projet, il est recommandé de commencer par la lecture de ce document avant de consulter les documents de contexte et le guide technique.
