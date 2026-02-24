# Moteur de Recherche #CultureChezNous (Apache Solr)

Ce projet a été réalisé dans le cadre du cours **"Indexation sémantique et recherche d'information" (Master 2 Langue & Informatique)** à **Sorbonne Université** pour l'année universitaire 2025-2026.

L'objectif est de construire un moteur de recherche performant basé sur **Apache Solr** pour explorer les ressources culturelles numériques françaises issues du corpus gouvernemental `#CultureChezNous`.

---

## 📁 Structure du dépôt

* **Culture.csv** : Le corpus enrichi et nettoyé (1149 ressources culturelles).
* **managed-schema** : Configuration des champs Solr (types de données, indexation morphologique française).
* **solrconfig.xml** : Configuration du `SearchHandler`, incluant les paramètres EDisMax et les définitions des facettes.
* **velocity/** : Dossier contenant les templates personnalisés pour l'interface utilisateur (UI).
* **Rapport.pdf** : Rapport détaillé expliquant la méthodologie et les résultats.
* **Présentation.pdf** : Support de présentation du projet.

---

## 🛠️ Méthodologie et Prétraitement

Le corpus initial provenant de *data.gouv.fr* a été enrichi via un script Python pour répondre aux exigences techniques de Solr :
* **Normalisation des dates** : Conversion au format ISO `YYYY-MM-DDTHH:MM:SSZ`.
* **Enrichissement sémantique** : Création de champs booléens (`is_for_kids`, `long_duration`, `is_accessible`).
* **Géolocalisation** : Extraction et nettoyage des coordonnées latitude/longitude pour la recherche spatiale.

---

## 🔍 Fonctionnalités du Moteur de Recherche

Le moteur propose une exploration multi-critères grâce à plusieurs types de facettes configurées dans `solrconfig.xml` :

* **Field Facets** : Filtrage par thématique (Musées, Histoire, etc.), type de ressource et ville.
* **Query Facets** : Filtres rapides pour les contenus adaptés aux enfants ou accessibles aux handicapés.
* **Range Facets** : Navigation par intervalles de durée (ex: 0-30 min) et par année de publication.
* **Pivot Facets** : Croisement dynamique entre les communes et les types de ressources.
* **Interface Velocity** : Personnalisation des labels et du rendu des dates pour une meilleure expérience utilisateur.

---

## 🚀 Installation et Configuration

### Prérequis
* Apache Solr (testé sur la version 8.11.2).
* Un noyau (core) nommé `culture`.

### Mise en place
1. Créez un nouveau core Solr : `bin/solr create -c culture`.
2. Remplacez les fichiers `managed-schema` et `solrconfig.xml` dans le répertoire `server/solr/culture/conf/` par ceux de ce dépôt.
3. Copiez le contenu du dossier `velocity/` dans le répertoire correspondant de votre instance Solr.
4. Redémarrez Solr et indexez le fichier `Culture.csv` via l'interface Solr Admin (section Documents, format CSV, séparateur `;`).



