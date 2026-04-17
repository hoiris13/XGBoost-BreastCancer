# 🩺 Breast Cancer Classification using XGBoost

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/XGBoost-Classifier-orange?logo=xgboost" />
  <img src="https://img.shields.io/badge/Scikit--Learn-Pipeline-f7931e?logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen" />
</p>
<p align="center"><i>Classifying breast tumors as Malignant or Benign using gradient boosting on real-world clinical data.</i></p>

📌 Project Overview
This project applies the XGBoost (Extreme Gradient Boosting) algorithm to the Breast Cancer Wisconsin (Diagnostic) dataset to classify tumors as Malignant (M) or Benign (B), based on features computed from digitized images of fine needle aspirate (FNA) of breast masses.

📊 Dataset at a Glance
PropertyDetailSourceBreast Cancer Wisconsin (Diagnostic) DatasetTotal Samples569Features30 numericTargetdiagnosis — Benign (B) or Malignant (M)Class SplitBenign: 357 (62.7%) · Malignant: 212 (37.3%)
The 30 features capture mean, standard error, and worst (largest) values of 10 cell nucleus measurements: radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry, and fractal dimension.

⚙️ Methodology
1. Preprocessing
The id column was dropped and the target variable was label-encoded (B → 0, M → 1).
2. Train-Test Split
The data was split 80/20 with stratified sampling to preserve class distribution.
3. Model — XGBClassifier
HyperparameterValuen_estimators100max_depth5learning_rate0.1subsample0.8colsample_bytree0.8

🏆 Results
MetricScoreAccuracy~97%AUC-ROC~99%
The notebook also generates:

✅ Classification Report (Precision, Recall, F1 per class)
✅ Confusion Matrix
✅ ROC Curve
✅ Top 10 Feature Importances
