---
title: Synthèse
---

# Synthèse

## Choix retenus

- **WTA en premier :** historique accessible au démarrage.
- **BigQuery :** infrastructure déjà utilisée chez Tennis Canada.
- **Python et dlt :** extraction, structuration et chargement avec `merge`.
- **Cloud Run et Cloud Scheduler :** exécution hebdomadaire, avec alertes Cloud Monitoring.

## Ce qui a fonctionné

Le pipeline est déployé et les relances testées ne créent pas de doublons sur les clés naturelles. Les tables sont documentées et une correspondance ITF / WTA est en place.

## Ce qui a changé après vérification

La correction de pagination a fait passer `match_results` d’environ **488 000 à 2,6 millions de lignes**. Le traitement peut réussir techniquement tout en récupérant un historique incomplet : la surveillance des exécutions doit donc s’accompagner de vérifications des données.

La source WTA inclut surtout des résultats ITF féminins. La couverture historique et les champs disponibles imposent des filtres et des limites aux analyses.

## Travail restant

L’extraction ITF a commencé. La suite consiste à poursuivre cette intégration, traiter les anomalies WTA et préciser le périmètre des analyses. Le rapport final présentera les résultats et leurs limites.
