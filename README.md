# 🏆 Data Tour Hub 2025 | Credit Scoring Predictor (Top 5% National)

[![ML Pipeline](https://img.shields.io/badge/Pipeline-AutoML%20%26%20Ensembling-blue.svg)](#)
[![Rank](https://img.shields.io/badge/Rank-9th%20%2F%20195%20%20(Top%205%25)-goldenrod.svg)](#)
[![Region](https://img.shields.io/badge/Representing-DR%20Congo%20%F0%9F%87%A8%F0%9F%87%AC-red.svg)](#)

Ce dépôt héberge l'architecture de Machine Learning de bout en bout développée pour le prestigieux hackathon panafricain **Data Tour Hub 2025**. Le projet se concentre sur le **scoring de crédit bancaire**, un cas d'usage critique pour atténuer le risque de défaut tout en favorisant l'inclusion financière.

### 🎯 Faits Marquants & Performance
* **Classement :** **9ème place sur 195 équipes** nationales inscrites (Top 5%).
* **Rôle :** Représentant officiel de la République Démocratique du Congo (RDC) 🇨🇩.
* **Métrique Métier & Technique :** Optimisation stricte du **ROC-AUC** sur un dataset massif de **192 000 lignes et 59 features**.

---

## 💼 Problématique Métier & Enjeux
Accorder un crédit implique une évaluation précise du profil de risque de l'emprunteur. Un modèle trop conservateur freine la croissance de la banque ; un modèle trop laxiste engendre des créances douteuses. 

L'objectif de ce projet était de concevoir un algorithme capable de classifier les demandes de crédit avec une haute fidélité, capable de maintenir ses performances en production (généralisation face à la variance).

---

## 🛠️ Approche Technique & Architecture du Pipeline

L'ingénierie de ce projet a été segmentée en deux phases distinctes, simulant un cycle de R&D jusqu'à la mise en production :

### Phase 1 : Exploration & Tuning Fin (Baseline)
* **Modèle :** LightGBM (Light Gradient Boosting Machine).
* **Framework d'Optimisation :** Recherche d'hyperparamètres bayésienne via **Optuna** (`num_leaves`, `learning_rate`, `max_depth`).
* *Limitation identifiée :* Un modèle unique, même parfaitement optimisé, atteint un biais algorithmique structurel.

### Phase 2 : Industrialisation & Ensembling (`FINAL_PIPELINE.ipynb`)
Pour sécuriser le Top 5% du classement, le pipeline a basculé vers une approche d'**AutoML robuste avec AutoGluon** :
1. **Multi-layer Stacking :** Entraînement et empilement vertical de plusieurs familles d'algorithmes (XGBoost, CatBoost, LightGBM, Random Forests).
2. **K-Fold Bagging Intégré :** Élimination du risque de surapprentissage (*overfitting*) sur le jeu de validation.
3. **Analyse de Calibration :** Post-traitement rigoureux avec tracé de la distribution des probabilités prédites (`y_pred_proba`) pour ajuster dynamiquement le seuil de décision métier.
4. **Gestion de la Mémoire :** Utilisation intensive de garbage collection (`gc.collect()`) pour garantir la stabilité du pipeline sur des infrastructures contraintes.

---

## 📦 Structure du Projet

```text
├── FINAL_PIPELINE.ipynb       # Pipeline final de production (AutoML & Ensembling)
├── SUBMISSION_CAN_2025.ipynb  # Laboratoire d'expérimentation et tuning (Optuna + LightGBM)
├── requirements.txt           # Fichier d'environnement pour la reproductibilité
└── README.md                  # Documentation du projet

🚀 Installation et Utilisation

Pour cloner le projet et installer toutes les dépendances nécessaires, exécutez les commandes suivantes dans votre terminal :

* **bash**
git clone [https://github.com/Michel-Bahala/Scoring-de-credit-bancaire-Clallenge-Data-tour-Hub-2025.git](https://github.com/Michel-Bahala/Scoring-de-credit-bancaire-Clallenge-Data-tour-Hub-2025.git)
cd Scoring-de-credit-bancaire-Clallenge-Data-tour-Hub-2025
pip install -r requirements.txt
