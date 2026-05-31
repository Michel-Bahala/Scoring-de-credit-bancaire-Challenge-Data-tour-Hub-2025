# 🏆 Data Tour Hub 2025 | Credit Scoring Predictor (Top 5% Global)



Ce dépôt héberge l'architecture de Machine Learning de bout en bout développée pour le prestigieux hackathon panafricain **Data Tour Hub 2025**. Le projet se concentre sur le **scoring de crédit bancaire**, un cas d'usage critique pour atténuer le risque de défaut tout en favorisant l'inclusion financière.

### 🎯 Faits Marquants & Performance
* **Classement :** **9ème place sur 195 équipes** nationales inscrites (Top 5%).
* **Rôle :** Représentant officiel de la République Démocratique du Congo (RDC) 🇨🇩.
* **Métrique Métier & Technique :** Optimisation stricte du **ROC-AUC** sur un dataset massif et équilibré de **192 000 lignes et 59 features**.

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

### Phase 2 : Industrialisation & Ensembling de Haut Niveau (`HIGH_LEVEL_FINALY_(1).ipynb`)
Pour sécuriser le Top 5% du classement, le pipeline a basculé vers une approche d'**AutoML robuste avec AutoGluon** :
1.  **Multi-layer Stacking :** Entraînement et empilement vertical de plusieurs familles d'algorithmes (XGBoost, CatBoost, LightGBM, Random Forests ).
2.  **K-Fold Bagging Intégré :** Élimination radicale du risque de surapprentissage (*overfitting*) sur le jeu de validation.
3.  **Analyse de Calibration :** Post-traitement rigoureux avec tracé de la distribution des probabilités prédites (`y_pred_proba`) pour ajuster dynamiquement le seuil de décision métier.
4.  **Gestion de la Mémoire :** Utilisation intensive de garbage collection (`gc.collect()`) pour garantir la stabilité du pipeline sur des infrastructures contraintes.

---

## 📦 Structure du Projet

```text
├── HIGH_LEVEL_FINALY_(1).ipynb  # Pipeline final de production (AutoML & Ensembling)
├── SUBMISSION_CAN_2025.ipynb   # Laboratoire d'expérimentation et tuning (Optuna + LightGBM)
├── requirements.txt            # Fichier d'environnement pour la reproductibilité
└── README.md                   # Documentation du projet


git clone https://github.com/Michel-Bahala/Scoring-de-credit-bancaire-Clallenge-Data-tour-Hub-2025.git
pip install -r requirements.txt
