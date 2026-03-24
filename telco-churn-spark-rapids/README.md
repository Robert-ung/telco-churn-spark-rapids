# Prédiction du Churn Client avec Apache Spark & RAPIDS GPU

## 📌 Présentation du Projet
L’objectif du projet est de construire un pipeline Spark complet pour prédire le churn (départ des clients) à partir des données d’usage d’un service Telco. Ce projet a été réalisé pour illustrer le cycle complet d'un projet de Machine Learning. Il s'inscrit dans une logique métier forte liée à la fidélisation, la rétention et l'analyse de la valeur client.

## 📊 Jeu de données
* Le dataset utilisé est le "Telco Customer Churn" disponible sur [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn/data).
* Il contient 7043 clients et de nombreuses variables catégorielles.
* La variable cible (Churn) présentait un fort déséquilibre : 73% de clients restés contre 27% de clients partis.

## 🛠️ Outils et Technologies
* **Pipeline principal :** PySpark et Spark MLlib.
* **Accélération GPU :** RAPIDS (cuDF, cuML).
* **Environnement :** Google Colab.

## ⚙️ Méthodologie
1. **Préparation des données :** Nettoyage des valeurs vides dans la colonne des charges totales et conversion de la variable cible en format binaire.
2. **Feature Engineering :** Création d'un pipeline Spark utilisant `StringIndexer`, `OneHotEncoder` et `VectorAssembler` pour vectoriser 46 dimensions.
3. **Gestion du déséquilibre :** Application d'une méthode de sur-échantillonnage (oversampling) sur la classe minoritaire pour forcer le modèle à mieux apprendre les cas de.
4. **Modélisation :** Entraînement et comparaison d'une Régression Logistique et d'un Random Forest.
5. **Optimisation :** Recherche des meilleurs hyperparamètres pour le Random Forest via Cross-Validation (numTrees=100, maxDepth=7).

## 🏆 Résultats et Performances
* Le meilleur modèle est le Random Forest entraîné sur le dataset équilibré.
* Il obtient une Accuracy de 0.784 et un AUC de 0.861.
* L'équilibrage des données a permis d'augmenter significativement le taux de détection (Recall) des clients réels sur le point de partir.

## 💡 Insights Business
L'analyse de l'importance des variables (Feature Importance) a révélé les principaux leviers d'action :
* **Engagement :** Les clients avec un contrat sans engagement (Month-to-month) sont les plus volatils. Proposer des remises sur des engagements annuels peut réduire ce risque.
* **Ancienneté :** Les nouveaux clients (faible tenure) sont moins fidèles. Un meilleur accompagnement (onboarding) est recommandé.
* **Services additionnels :** L'absence d'options de sécurité en ligne augmente fortement le risque de départ. Offrir quelques mois gratuits sur ce service pourrait limiter les résiliations.

## 🚀 Bonus : Accélération GPU avec RAPIDS
Un test a été mené avec la suite RAPIDS pour comparer les performances avec Spark.
* L'entraînement du Random Forest sur GPU a pris environ 2.58 secondes.
* Cette approche est 15 à 30 fois plus rapide que sur Spark CPU.
* Les performances prédictives (AUC = 0.818) sont légèrement inférieures car seules les variables numériques ont été exploitées pour ce test.