# 📊 CatalogueR -- Catalogue interne de données pour la DREAL

**CatalogueR** est une application **Shiny** conçue pour faciliter l'accès, la navigation et l'exploitation des données de la DREAL, tout en améliorant la qualité des métadonnées associées.

Ce prototype a été développé avec **R Shiny** et s'appuie sur un serveur de base de données **PostgreSQL/PostGIS**, connecté via le package `RPostgreSQL`.


## Objectif

-   Faciliter la découverte du patrimoine de données de la DREAL avec un outil simple d'utilisation 🎯
-   Améliorer la qualité des données et des métadonnées 🚀
-   Proposer des indicateurs sur le patrimoine de données 📈

## Fonctionnalités

-   Rechercher : utiliser le moteur de recherche plein texte 🔍
-   Explorer : parcourir les bases, schémas et tables du SGBD 📚
-   Découvrir : afficher les métadonnées, les données attributaires voire un aperçu des données spatiales d'une table 📍

## Technologies utilisées

Le développement de **CatalogueR** repose sur :

-   🔓 Adoption d'une solution **open source**
-   💻 Mise en place d'une fonctionnalité d'**exploration du contenu** des bases de données internes
-   👨‍💻 Développement d'une **application locale** avec **R Shiny**, déployée sur le serveur interne **Dataviz**
-   ⌛ **Actualisation automatique et quotidienne** des données affichées dans le catalogue

## Déploiement

L'application **CatalogueR** est hébergée sur le serveur interne **Dataviz**. Le fichier de données `datamart_catalogue.RData` est mis à jour et déployé automatiquement chaque jour grâce à un système automatisé :

-   Une **tâche planifiée Windows** exécute le script `script_routine.R` chaque nuit.
-   Ce script génère le datamart `datamart_catalogue.RData` à l'aide de `datamartage.R`, puis déclenche `deploiement_automatique.R`
-   Le **déploiement du fichier `.RData`** s'effectue via **FTP**, grâce au package **RCurl.**
-   Tous les **logs** sont enregistrés dans `logs/script_routine.log` pour assurer le suivi

## Installation local

Pour exécuter **CatalogueR** en local :

### Prérequis

-   R & RStudio
-   Les packages suivants : [`datalibaba`](https://gitlab-forge.din.developpement-durable.gouv.fr/dreal-pdl/csd/datalibaba), [`shinygouv`](https://github.com/spyrales/shinygouv/tree/main), shiny, , shinyjs, dplyr, DBI, DT, leaflet, mapview, sf, etc.

### Etapes :

**1. Cloner le dépôt :**

``` bash
git clone https://gitlab-forge.din.developpement-durable.gouv.fr/dreal-pdl/csd/catalogueR.git

cd catalogueR
```

**2. Installer les packages nécessaires :**

``` bash
install.packages(c("shiny", "shinyjs", "dplyr", "DBI", "DT", "leaflet", "mapview", "sf", "RCurl", "logging", "readr"))

# install.packages("remotes")

remotes::install_github("spyrales/shinygouv")

remotes::install_gitlab('dreal-pdl/csd/datalibaba', host = "gitlab-forge.din.developpement-durable.gouv.fr")
```

**3. Lancer l'application :**

``` bash
shiny::runApp()
```

## Schéma de flux de mise à jour

Ce schéma illustre le processus automatisé de mise à jour quotidienne du datamart et le déploiement de l'application ![Schéma de flux de mise à jour](www/flux_de_mise_a_jour.png) 

[_Créé avec app.diagrams.net_](https://app.diagrams.net/#G1jS4hU0H-dD0DlOqSZZdMJu5VOfYUgc4B#%7B%22pageId%22%3A%22jUiN6-0aC5laFbHm_blw%22%7D)

## Schéma de la structure de données

Ce schéma représente l'organisation des tables et des relations dans la base de données alimentant le catalogue. ![Schéma de structure des données](www/schema_catalogueR.png)
