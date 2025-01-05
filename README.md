Voici un fichier README détaillé adapté au projet que tu m'as décrit :

---

# README - Pipeline de Données Global Flights avec Talend

## Description du projet
Ce projet a pour but de construire un pipeline automatisé pour le traitement des données des aéroports et des routes aériennes à l'échelle mondiale. Il utilise **Talend Studio** pour l’ingestion, le nettoyage, la transformation et le chargement des données dans une base de données relationnelle. 

Les sources de données proviennent du dataset public **OpenFlights** :
- **airports.dat** : liste des aéroports avec leurs coordonnées géographiques.
- **routes.dat** : informations sur les routes aériennes reliant différents aéroports.

L’objectif principal est d’obtenir un dataset enrichi, exploitable pour l’analyse des connexions aériennes.

## Architecture du pipeline
Le pipeline de données est organisé en plusieurs jobs Talend distincts :
1. **Job d’ingestion** : lecture des fichiers CSV bruts.
2. **Job de nettoyage** : filtrage et validation des données.
3. **Job de transformation** : jointure des datasets et ajout de colonnes calculées.
4. **Job de chargement** : insertion des données transformées dans une base de données relationnelle.

## Instructions d'exécution

### Prérequis
- **Talend Studio** installé.
- Une base de données relationnelle (MySQL ou PostgreSQL) configurée.
- Les fichiers sources **airports.dat** et **routes.dat** placés dans le répertoire d’entrée défini.

### Étapes pour exécuter le pipeline
1. **Cloner le projet Talend**  
   Importer les fichiers du projet dans Talend Studio.
   
2. **Configurer les variables de contexte**  
   Adapter les valeurs des variables de contexte selon l’environnement :
   - `context.inputDirectory` : chemin vers les fichiers d’entrée.
   - `context.outputDirectory` : chemin des fichiers de sortie.
   - `context.db_host`, `context.db_user`, `context.db_pass` : informations de connexion à la base de données.

3. **Exécuter les jobs dans l'ordre suivant** :
   1. `IngestFiles` : ingestion des fichiers sources.
   2. `CleanData` : nettoyage et validation des données.
   3. `TransformData` : transformation et enrichissement des données.
   4. `LoadData` : chargement final dans la base de données.

### Résultats attendus
- Fichiers de sortie :
  - **Cleaned_Airports.csv** : données des aéroports nettoyées.
  - **Rejected_Rows.csv** : lignes rejetées avec des erreurs de validation.
  - **Joined_Flights.csv** : dataset enrichi contenant les routes aériennes avec les détails des aéroports.
- Table **flights_enriched** contenant les données finales prêtes à être analysées.

### Gestion des erreurs
Chaque job comporte une gestion des erreurs :
- Les erreurs critiques interrompent le pipeline et écrivent un log détaillé.
- Les erreurs mineures (ex. : données invalides) sont redirigées vers des fichiers de rejet pour une analyse ultérieure.

## Livrables du projet
- Fichiers des jobs Talend (.zip ou .item).
- Script SQL de création de la table cible.
- Documentation utilisateur.
- Fichiers de données nettoyés et enrichis.
