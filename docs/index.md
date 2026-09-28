---
title: Vue d'ensemble du projet
---

<style>
    @media screen and (min-width: 76em) {
        .md-sidebar--primary {
            display: none !important;
        }
    }
</style>

# Vue d'ensemble du projet

!!! info "Informations générales"
    **Session**: Automne 2026  
    **Auteur(s)**: Nassim Barhoumi (20315513)  
    **Thème(s)**: Ingénierie des données, pipelines de données, science des données sportives  
    **Superviseur(s)**: Louis-Edouard Lafontant (DIRO, Université de Montréal)  
    **Collaborateur(s):** Tennis Canada  

## Description du projet

### Contexte

Tennis Canada utilise des données de joueurs et de joueuses pour le suivi de la performance, l'analyse et la prise de décision (développement des athlètes, haute performance, tournois). Ces données proviennent de trois sources externes : les circuits professionnels **WTA** et **ATP**, ainsi que la Fédération internationale de tennis (**ITF**), qui couvre notamment le circuit junior et les tournois de niveau ITF.

Chaque organisation publie ses propres données, avec ses propres API, formats, identifiants et conditions d'accès. Tennis Canada ne dispose aujourd'hui d'aucun pipeline automatisé pour récupérer et stocker ces données de façon fiable.

### Parties prenantes

- **Nassim Barhoumi** — développement des pipelines et des analyses
- **Directeur, Tennis Canada** — supervision du projet côté organisation
- **Sylvain Gaudet** — data scientist, Institut national du sport (INS), rattaché à l'équipe haute performance ; utilisateur des données pour ses analyses
- **Entraîneurs** — consultation des rapports (Power BI)

### Problématique

Les données de joueurs sont difficiles à obtenir et à exploiter :

- aucune ingestion automatisée n'existe pour les données WTA, ATP et ITF ;
- chaque source impose ses propres contraintes techniques (authentification, pagination, limites d'appels, formats, volumes historiques importants) ;
- les données sont fragmentées entre trois fournisseurs, avec des structures et des identifiants différents ;
- un même joueur peut apparaître dans plusieurs sources (ex. passage du circuit ITF junior au circuit professionnel) sans lien entre ses profils ;
- sans données fiables et centralisées, aucune analyse ni modélisation n'est possible à grande échelle.

### Proposition et objectifs

Le projet vise d'abord à **construire des pipelines de données robustes et automatisés** pour les trois sources, vers l'entrepôt de données de Tennis Canada (Google BigQuery). Il s'agit de la partie centrale du projet, car chaque source présente des défis techniques propres et nécessite la récupération d'un historique volumineux.

Si le temps le permet, les données seront ensuite exploitées en trois étapes successives : la **centralisation** des sources dans un modèle unifié, des **analyses** exploratoires, puis un **modèle prédictif**.

**Objectifs principaux**

- **O1** — Développer un pipeline d'ingestion automatisé pour les données **WTA**, incluant l'historique.
- **O2** — Développer un pipeline d'ingestion automatisé pour les données **ITF**, incluant l'historique.
- **O3** — Développer un pipeline d'ingestion automatisé pour les données **ATP**, incluant l'historique (sous réserve de l'obtention de l'accès aux données).
- **O4** — Assurer la fiabilité des pipelines : planification automatique, gestion des erreurs, reprise en cas d'échec et contrôles de qualité (complétude, doublons, fraîcheur).
- **O5** — Documenter l'architecture des pipelines et les jeux de données.

**Objectifs secondaires (selon le temps disponible)**

- **O6** — Centraliser les sources dans un modèle de données unifié « joueur », avec rapprochement des identités.
- **O7** — Réaliser des analyses exploratoires sur les données joueurs.
- **O8** — Développer un premier modèle prédictif (ex. prédiction de résultats ou de progression).

**Exemples d'utilisation visés**

- Rapport de carrière d'un joueur canadien, de l'ITF jusqu'au circuit WTA ou ATP : évolution du classement, victoires par surface, niveau des adversaires.
- Comparaison de la trajectoire d'un jeune joueur avec celle des joueurs ayant atteint le top 100.
- Préparation d'un match : historique des confrontations et forme récente de l'adversaire.
- Résumé hebdomadaire automatique des résultats des joueurs canadiens sur tous les circuits.
- Modèle Elo par surface pour prédire l'issue des matchs.

### Méthodologie

Le projet suit une approche itérative, **une source à la fois**. Chaque itération commence par une phase de recherche et de lecture de la documentation de l'API concernée, suivie de la conception, du développement, des tests et de la validation du pipeline. L'architecture et les leçons apprises sont ensuite réutilisées pour la source suivante. Chaque mise en commun est l'occasion de présenter l'avancement de l'itération en cours.

Les sources sont traitées dans l'ordre **WTA → ITF → ATP**. Le pipeline ATP est placé en dernier, car l'accès aux données est en cours d'obtention. Si l'accès n'est pas disponible à temps, cette période sera consacrée aux objectifs secondaires (centralisation et analyses des données WTA et ITF).

Chaque itération suit les mêmes étapes :

1. **Recherche et documentation** — lecture de la documentation de l'API (points d'accès, authentification, pagination, limites d'appels, formats, identifiants), exploration des données disponibles et identification des contraintes.
2. **Conception** — choix des données à extraire, structure des tables cibles, stratégie de chargement (historique et incrémental).
3. **Développement** — ingestion, chargement de l'historique, planification, gestion des erreurs.
4. **Tests et validation** — contrôles de qualité et validation des données chargées.

Déroulement global :

1. **Études préliminaires** — analyse des besoins et conception d'une architecture commune aux pipelines.
2. **Itération 1 : WTA**
3. **Itération 2 : ITF**
4. **Itération 3 : ATP** — ou, à défaut d'accès, centralisation WTA/ITF.
5. **Extensions, si le temps le permet** — centralisation, analyses, puis modèle prédictif.
6. **Bilan** — documentation finale, rapport et présentation.

### Choix technologiques

**Volume de données estimé**

| Source | Volume estimé                              | Statut                    |
|--------|--------------------------------------------|---------------------------|
| WTA    | ~2,6 millions de matchs                    | Accès disponible          |
| ITF    | quelques centaines de milliers à ~1 million de matchs | Accès disponible |
| ATP    | même ordre de grandeur que la WTA          | Licence en négociation    |

Ce volume reste modeste et tiendrait sur un ordinateur portable. Le choix de l'infrastructure repose donc sur le contexte de l'organisation plutôt que sur le volume.

**Pourquoi BigQuery et le cloud**

- **Infrastructure existante** : BigQuery et Google Cloud sont déjà en place chez Tennis Canada et reliés à Power BI. Aucun temps de mise en place n'est requis ; l'effort du projet porte sur les pipelines eux-mêmes.
- **Confidentialité** : les données WTA et ATP sont sous licence et ne peuvent pas être stockées sur un poste personnel. BigQuery permet de contrôler et de tracer les accès.
- **Accès partagé** : plusieurs parties prenantes doivent consulter les données (direction, INS, entraîneurs).
- **Automatisation** : les pipelines doivent se rafraîchir seuls (Cloud Run et Cloud Scheduler), ce qu'un poste local ne permet pas.

Le développement et les tests se font en local avec **DuckDB** : dlt permet de changer de destination par simple configuration, puis de basculer vers BigQuery pour la production.

**Pourquoi SQL plutôt que NoSQL**

Une base NoSQL orientée documents (ex. MongoDB) a été considérée. Les données sont toutefois relationnelles (joueurs, tournois, matchs, classements) et les besoins analytiques : agrégations et jointures entre les trois sources. SQL est mieux adapté, et Power BI s'y connecte nativement. Les réponses JSON des API sont normalisées en tables par dlt.

**Outils et technologies :** Python, dlt, DuckDB (développement local), Google Cloud Run, Cloud Scheduler, BigQuery (SQL), Git/GitHub. Pour les extensions : pandas, scikit-learn, Power BI.

!!! warning "Confidentialité"
    Le dépôt et le site de suivi sont publics : ils ne contiennent aucune donnée ni aucune clé d'accès.

### Validation et Évaluation

- **Exactitude** : comparaison d'échantillons de données chargées avec les sources officielles (résultats, classements, profils).
- **Complétude** : vérification de la couverture historique et du nombre d'enregistrements attendus par source.
- **Qualité** : tests automatisés (doublons, valeurs manquantes, fraîcheur des données) exécutés à chaque chargement.
- **Fiabilité** : suivi des exécutions planifiées (taux de succès, reprise après échec).
- **Utilité** : retours des utilisateurs internes de Tennis Canada (haute performance, INS, entraîneurs) sur les données produites.
- **Extensions** : si le modèle prédictif est réalisé, évaluation par des métriques standards (ex. précision, AUC) sur un jeu de test.

## Échéancier

!!! info
    Le suivi complet est disponible dans la page [Suivi de projet](suivi.md).

| Activités                                | Début         | Fin           | Livrable                                              | Statut   |
|------------------------------------------|---------------|---------------|-------------------------------------------------------|----------|
| Ouverture de projet                      | 1 sept.       | 1 oct.        | Site de suivi + vue d'ensemble                        | En cours |
| Études préliminaires                     | 1 sept.       | 27 sept.      | Analyse des besoins + architecture commune            | Terminé  |
| Recherche et documentation API WTA       | 1 sept.       | 27 sept.      | Notes sur l'API WTA                                   | Terminé  |
| Pipeline WTA                             | 28 sept.      | 30 oct.       | Pipeline WTA + contrôles de qualité                   | En cours |
| **Mise en commun I**                     | 5 oct.        | 9 oct.        | Architecture + choix techniques + début du pipeline WTA | À venir |
| Recherche et documentation API ITF       | 26 oct.       | 6 nov.        | Notes sur l'API ITF                                   | À venir  |
| **Mise en commun II**                    | 2 nov.        | 6 nov.        | Pipeline WTA complet                                  | À venir  |
| Pipeline ITF                             | 2 nov.        | 27 nov.       | Pipeline ITF + contrôles de qualité                   | À venir  |
| **Mise en commun III**                   | 23 nov.       | 27 nov.       | Avancement du pipeline ITF                            | À venir  |
| Pipeline ATP (selon l'accès) ou extensions | 30 nov.     | 11 déc.       | Pipeline ATP, ou centralisation et analyses WTA/ITF   | À venir  |
| Présentation + Rapport                   | <!-- date --> | <!-- date --> | Présentation + Rapport                                | À venir  |
