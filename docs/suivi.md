---
title: Suivi du projet
---

<style>
    @media screen and (min-width: 76em) {
        .md-sidebar--primary {
            display: none !important;
        }
    }
</style>

# Suivi de projet

---

## Semaines 1 à 4 (1er – 27 septembre)

### Objectifs de la période
- Définir et faire approuver le mandat
- Analyser les besoins avec Tennis Canada
- Explorer les solutions et définir l'architecture commune des pipelines
- Étudier l'API WTA
- Mettre en place le site de suivi et rédiger la vue d'ensemble

### Travail réalisé

!!! abstract "Avancement"
    - [x] Mandat « player data » approuvé
    - [x] Analyse des besoins
        - Discussions avec mon directeur à Tennis Canada sur les objectifs et les priorités
        - Identification des parties prenantes et de leurs besoins : direction, Sylvain Gaudet (INS, équipe haute performance) et entraîneurs
    - [x] Exploration des solutions
        - Étude des outils d'ingestion (dlt) et d'exécution planifiée (Cloud Run, Cloud Scheduler)
        - Comparaison stockage local et cloud, SQL et NoSQL
        - Définition d'une architecture commune aux trois pipelines
    - [x] Recherche et documentation de l'API WTA
        - Points d'accès, authentification, pagination, limites d'appels, formats et identifiants
        - Exploration des données disponibles et estimation des volumes
    - [x] Site de suivi créé à partir du gabarit du DIRO et publié sur GitHub Pages
    - [x] Vue d'ensemble rédigée et soumise

### Décisions et ajustements

!!! info "Décisions"
    - Priorité aux pipelines de données (WTA, ITF, puis ATP), les analyses et le modèle prédictif venant ensuite si le temps le permet
    - Pipeline ATP placé en dernier, car la licence de données est encore en négociation

### Difficultés rencontrées

!!! warning "Difficultés"
    - Dépendance externe : l'accès aux données ATP dépend de la conclusion de la licence

---

## Semaine 5 (28 septembre – 4 octobre)

### Objectifs de la période
- Répondre à la rétroaction sur la vue d'ensemble
- Ajuster l'échéancier
- Commencer le pipeline WTA
- Préparer la mise en commun de la semaine du 5 octobre

### Travail réalisé

!!! abstract "Avancement"
    - [x] Réponse à la rétroaction du superviseur
    - [x] Vue d'ensemble mise à jour : parties prenantes, volumes estimés, choix technologiques et exemples d'utilisation
    - [ ] Début du développement du pipeline WTA

### Décisions et ajustements

!!! info "Décisions"
    - BigQuery maintenu malgré un volume modeste
        - Environnement Google Cloud déjà en place chez Tennis Canada et relié à Power BI
        - Données WTA et ATP sous licence et confidentielles, qui ne peuvent pas être stockées sur un poste personnel
        - Accès nécessaire pour plusieurs parties prenantes (direction, INS, entraîneurs)
        - Rafraîchissement automatique des pipelines
    - Développement et tests en local avec DuckDB via dlt, puis bascule vers BigQuery
    - SQL retenu plutôt que NoSQL (MongoDB), car les données sont relationnelles et les besoins analytiques
    - Échéancier allongé pour les pipelines : 4 à 5 semaines pour WTA et 4 semaines pour ITF ; l'ATP et les extensions partagent les deux dernières semaines
    - Aucune donnée ni clé d'accès dans le dépôt GitHub, qui est public
