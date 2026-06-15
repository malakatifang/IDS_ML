
# Système de Détection d'Intrusions Réseau (IDS) par Machine Learning

##  Présentation du Projet

Ce projet implémente un Système de Détection d'Intrusions (IDS) basé sur des techniques de Machine Learning afin de détecter et de classifier automatiquement les comportements malveillants sur un réseau. Le système est entraîné et évalué à l'aide du dataset standard **NSL-KDD**, une version optimisée du célèbre jeu de données KDD Cup 1999, largement reconnue dans la recherche en cybersécurité.

Le pipeline complet intègre le prétraitement des données, l'encodage des variables, l'équilibrage des classes, ainsi que l'évaluation comparative de plusieurs algorithmes d'apprentissage supervisé afin de distinguer efficacement le trafic sain des activités malveillantes.

---

##  Objectifs

* **Automatisation : Détecter les intrusions au sein du trafic réseau en temps réel.
* **Classification : Identifier et catégoriser précisément les différents types d'attaques.
* **Analyse Comparative : Évaluer et comparer les performances de plusieurs algorithmes de Machine Learning.
* **Optimisation : Améliorer la sensibilité de détection à l'aide de techniques avancées de prétraitement et d'équilibrage de données.

---

##  Jeu de Données (Dataset)

Le projet s'appuie sur le dataset **NSL-KDD**, composé des fichiers suivants :

* `KDDTrain+.txt` (Données d'entraînement)
* `KDDTest+.txt` (Données de test)

Chaque enregistrement de connexion réseau est catégorisé selon son état :

* **Trafic Normal** (Flux légitime)
* **Déni de Service (DoS)**
* **Sondage (Probe)**
* **User to Root (U2R)**
* **Remote to Local (R2L)**

---

##  Structure du Projet

```text
IDS_ML/
│
├── data/
│   ├── KDDTrain+.txt        # Données d'entraînement brutes
│   └── KDDTest+.txt         # Données de test brutes
│
├── notebooks/
│   └── ids_ml.ipynb         # Pipeline complet (Analyse, SMOTE, Modélisation)
│
├── README.md                # Documentation du projet (ce fichier)
└── requirements.txt         # Liste des dépendances Python indispensables

```
---

##  Prétraitement des Données

Le pipeline de préparation des données intègre les étapes indispensables suivantes :

### 1. Nettoyage des Données

* Suppression de la colonne `difficulty` (non pertinente pour la classification).
* Détection et traitement des valeurs manquantes.

### 2. Encodage des Variables (Feature Encoding)

Les attributs catégoriels (textuels) ont été transformés à l'aide d'un encodage numérique pour être interprétables par les modèles.
*Variables concernées :* `protocol_type`, `service`, `flag`.

### 3. Alignement des Données

Alignement strict des ensembles d'entraînement et de test pour garantir un espace de caractéristiques (*features*) parfaitement identique.

### 4. Équilibrage des Classes

Face au fort déséquilibre des classes du dataset NSL-KDD, l'algorithme **SMOTE** (*Synthetic Minority Oversampling Technique*) a été appliqué (configuré avec `k_neighbors=1`) afin de générer des données synthétiques pour les attaques ultra-rares (telles que `spy`) et éviter les biais d'entraînement.

---

## 📉 Visualisation des Données

Plusieurs analyses graphiques ont été menées pour explorer le dataset :

* Projection géométrique du trafic réseau par Réduction de Dimensionnalité (**PCA**).
* Carte de chaleur (*Heatmap*) des valeurs manquantes.
* Distribution des classes **avant** et **après** l'application du SMOTE.

---

##  Algorithmes de Machine Learning Implémentés

Trois architectures de classification ont été implémentées et mises en concurrence :

### 1. Régression Logistique

Un modèle linéaire classique utilisé comme référence (*Baseline*).

### 2. Arbre de Décision (Decision Tree)

Un classificateur non linéaire performant, capable de capturer des règles de décision complexes et imbriquées.

### 3. Forêt Aléatoire (Random Forest)

Une méthode d'apprentissage par ensemble combinant plusieurs arbres de décision afin de maximiser la robustesse de la détection et limiter le surapprentissage (*overfitting*).

---

##  Métriques d'Évaluation

Les performances des modèles ont été rigoureusement mesurées à l'aide des indicateurs suivants :

* Précision globale (*Accuracy*)
* Rapport de classification (*Classification Report*) : Précision, Rappel (*Recall*), F1-Score
* Matrice de Confusion
* Courbe ROC et son score AUC (Aire Sous la Courbe)

---

##  Résultats

Après évaluation comparative sur les données de validation :

* La **Régression Logistique** a servi de point de départ (indiquant les limites des séparateurs linéaires avec un score AUC global de 0.61).
* Le modèle **Random Forest** a démontré les meilleures performances globales (Précision, Rappel et AUC maximisés) et a été sélectionné comme modèle final pour l'IDS.

---

## Technologies Utilisées

* **Langage :** Python
* **Manipulation de données :** Pandas, NumPy
* **Machine Learning :** Scikit-learn, Imbalanced-learn (SMOTE)
* **Visualisation :** Matplotlib, Seaborn
* **Environnement :** Jupyter Notebook / Google Colab

---

##  Installation et Utilisation

### 1. Cloner le dépôt

```
git clone https://github.com/malakatifang/IDS_ML.git
cd IDS_ML

```

### 2. Installer les dépendances

```
pip install -r requirements.txt

```

### 3. Exécuter le projet

Lancez l'interface Jupyter :

```
jupyter notebook

```

Ouvrez ensuite le fichier suivant pour exécuter les cellules de code : `notebooks/ids_ml.ipynb`. Une version est également accessible directement sur Google Colab.
