---
title: Suivi du projet
---

# Suivi du projet

## Mise à jour du 18 novembre 2026

Ce point reprend les résultats WTA et l’avancement de l’extraction ITF.

### Réalisé

- **Cloud Monitoring :** alerte par courriel en cas d’échec du job.
- **Idempotence :** deux exécutions successives, volumes inchangés et aucun doublon sur les clés naturelles dans le test réalisé.
- **Pagination corrigée :** nouveau chargement historique, d’environ 488 000 à 2,6 millions de lignes dans `match_results`.
- **Correspondance ITF / WTA :** liens trouvés uniques, sans ambiguïté observée. Cela ne garantit pas une correspondance pour chaque joueuse.
- **Documentation :** descriptions des tables et colonnes.

### Avancement ITF

**L’extraction des données ITF a commencé**, conformément à l’échéancier de novembre.

### Difficulté principale : la pagination

L’API pouvait renvoyer une page vide avant la fin, remettre le nombre de pages à zéro ou annoncer trop peu de pages. Le traitement conserve désormais la métadonnée de la première page, la compare au nombre calculé à partir du total d’enregistrements et poursuit malgré les pages vides. Sans métadonnées, il utilise une page courte comme signal de fin.

**Leçon : une exécution réussie et un test d’idempotence ne prouvent pas que l’historique est complet.**

### Limites relevées

- Résultats peu fournis avant 2000 et majorité de tournois ITF féminins dans la source WTA.
- Aucune donnée retournée par l’endpoint de statistiques de saison lors des vérifications.
- Fiches détaillées limitées à 2 107 joueuses actives, avec un historique depuis juillet 2026.
- Champs peu renseignés, dates en texte et certaines périodes incomplètes.

## Étapes précédentes

| Période | Travail réalisé |
|---|---|
| Septembre | Analyse des besoins, étude de l’API WTA et choix techniques. |
| Octobre | Déploiement WTA, chargement historique et planification hebdomadaire. |
| Début novembre | Correction de pagination, vérification du dataset et préparation de la mise en commun II. |

## Suite du trimestre

| Période | Objectif |
|---|---|
| Novembre | Traiter les anomalies et définir les filtres d’analyse. Avancer sur l’historique ITF selon les accès. |
| 30 novembre–11 décembre | ATP selon la licence, ou analyses avec les données disponibles. |
| 11–17 décembre | Présentation finale en présentiel : 25 minutes, questions incluses. Créneau à confirmer. |
| Date à confirmer | Remise du rapport final. |

La présentation finale nécessite la présence du superviseur. Au moins trois créneaux de préférence doivent être proposés après vérification de ses disponibilités.

**Accès externes :** une relance ITF est confirmée, sans réponse au 19 octobre. L’accès ATP dépend de la licence. Ces statuts restent à actualiser selon les retours des fournisseurs.
