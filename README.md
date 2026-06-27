# 🏆 Data Tour Hub 2025 | Credit Scoring Predictor (Top 5% National)

[![ML Pipeline](https://img.shields.io/badge/Pipeline-AutoML%20%26%20Ensembling-blue.svg)](#)
[![Rank](https://img.shields.io/badge/Rank-9th%20%2F%20195%20%20(Top%205%25)-goldenrod.svg)](#)
[![Region](https://img.shields.io/badge/Representing-DR%20Congo%20%F0%9F%87%A8%F0%9F%87%AC-red.svg)](#)

Ce dépôt héberge l'architecture de Machine Learning de bout en bout développée pour le prestigieux hackathon panafricain **Data Tour Hub 2025**. Le projet se concentre sur le **scoring de crédit bancaire**, un cas d'usage critique pour atténuer le risque de défaut tout en favorisant l'inclusion financière.

### 🎯 Faits Marquants & Performance
* **Classement :** **9ème place sur 195 équipes** nationales inscrites (Top 5%).
* **Rôle :** Représentant officiel de la République Démocratique du Congo (RDC) 🇨🇩.
* **Métrique Technique :** Optimisation stricte de l'**Area Under the ROC Curve (ROC-AUC)**, atteignant un score de validation d'environ **0.786**.
* **Volume de Données :** Gestion d'un volume massif à l'échelle industrielle (Big Data).

---

## 🎯 Objectif du Projet & Enjeux Métier
Accorder un crédit implique une évaluation précise du profil de risque de l'emprunteur. Un modèle trop conservateur freine la croissance de la banque ; un modèle trop laxiste engendre des créances douteuses (*Non-Performing Loans*). 

L'objectif principal était de concevoir un algorithme robuste capable de classifier les demandes de crédit en temps réel (Classification binaire : Solvable `0` vs Insolvable `1`), tout en maintenant ses performances de généralisation face à la variance de l'environnement de production.

---

## 🛠️ Approche Technique & Pipeline d'Ingénierie

L'ingénierie de ce projet a été scindée en phases stratégiques, simulant un cycle complet de R&D jusqu'à la mise en production sur des infrastructures contraintes.

### 1. Préparation de la Donnée & Gestion du "Class Imbalance"
* **Échelle des données :** Le jeu d'entraînement comptait plus d'un million de lignes, et le jeu de test final s'élevait à **3 572 662 lignes pour 60 caractéristiques**.
* **Stratégie d'Under-sampling :** Face à un fort déséquilibre des classes (les cas d'insolvabilité étant minoritaires) et pour éviter les plantages de mémoire vive (`Out Of Memory`), un échantillonnage rigoureux à **50/50** a été appliqué :
  ```python
  train[train["flag"] == 0].sample(120000, random_state=42)  # Classe Majoritaire
  train[train["flag"] == 1].sample(120000, random_state=42)  # Classe Minoritaire
  Cela a permis d'entraîner les algorithmes sur un sous-ensemble parfaitement équilibré de 240 000 entrées, garantissant un apprentissage impartial des motifs de défaut de paiement.

Feature Engineering & Réduction de dimension : Prétraitement avancé des variables catégorielles, imputation des valeurs manquantes et application d'une Analyse en Composantes Principales (PCA) pour capturer la variance essentielle sans surcharger les modèles.

# 2. Phase d'Exploration & Tuning Fin (Baseline)
Modèle : LightGBM (Light Gradient Boosting Machine).

Framework d'Optimisation : Recherche d'hyperparamètres bayésienne via Optuna (num_leaves, learning_rate, max_depth, min_child_samples).

Limitation : Un modèle unique, même parfaitement optimisé, atteint un biais algorithmique structurel.

# 3. Phase d'Industrialisation & Stacking Multi-niveaux (FINAL_PIPELINE.ipynb)
Pour sécuriser notre place au Top 5% du classement, le pipeline a basculé vers une approche d'AutoML robuste exploitant le framework AutoGluon :

Multi-layer Stacking (Architecture Multi-niveaux) : Entraînement et empilement vertical de plusieurs familles d'algorithmes complémentaires :

Modèles d'Arbres : LightGBM, CatBoost, XGBoost, Random Forests.

K-Fold Bagging Intégré : Élimination du risque de surapprentissage (overfitting) en entraînant des variantes de modèles sur différentes partitions des données.

Gestion de la Mémoire : Utilisation intensive de la libération manuelle de mémoire (gc.collect()) pour traiter efficacement l'inférence des 3,57 millions de lignes de test sur une infrastructure standard.

# 📈 Résultats et Métriques
Le modèle final combine la puissance des architectures d'arbres de décision et des réseaux de neurones profonds. En optimisant directement la métrique ROC-AUC, le système garantit :

Une excellente distinction entre un client sain et un client à risque (Score de Validation : ~0.786).

Une stabilité parfaite lors du passage à l'échelle face à des millions de requêtes d'inférence (Jeu de test validé avec succès).

# 📦 Structure du Projet
Plaintext
├── FINAL_PIPELINE.ipynb      # Pipeline final de production (AutoML, Inférence Big Data & Ensembling)
├── SUBMISSION_CAN_2025.ipynb  # Laboratoire d'expérimentation, échantillonnage et tuning (Optuna + LightGBM)
├── requirements.txt          # Fichier d'environnement pour assurer la reproductibilité absolue
└── README.md                 # Documentation complète du projet
🚀 Installation et Utilisation
Pour cloner le projet et installer toutes les dépendances nécessaires, exécutez les commandes suivantes dans votre terminal :

Bash
# Clonage du dépôt
git clone [https://github.com/Michel-Bahala/Scoring-de-credit-bancaire-Clallenge-Data-tour-Hub-2025.git](https://github.com/Michel-Bahala/Scoring-de-credit-bancaire-Clallenge-Data-tour-Hub-2025.git)

# Accès au répertoire
cd Scoring-de-credit-bancaire-Clallenge-Data-tour-Hub-2025

# Installation des dépendances (Pandas, NumPy, Scikit-learn, LightGBM, Optuna, AutoGluon, PyTorch, etc.)
pip install -r requirements.txt

  
