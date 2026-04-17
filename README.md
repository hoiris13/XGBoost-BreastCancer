# 🩺 Breast Cancer Classification using XGBoost

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/XGBoost-Classifier-orange?logo=xgboost" />
  <img src="https://img.shields.io/badge/Scikit--Learn-Pipeline-f7931e?logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen" />
</p>
<p align="center"><i>Classifying breast tumors as Malignant or Benign using gradient boosting on real-world clinical data.</i></p>

📌 Project Overview
Breast cancer is one of the most common cancers worldwide, and early accurate diagnosis is critical for effective treatment. This project applies the XGBoost (Extreme Gradient Boosting) algorithm — a powerful ensemble learning method based on decision trees — to the Breast Cancer Wisconsin (Diagnostic) dataset. The goal is to build a binary classifier that can accurately distinguish between Malignant (M) and Benign (B) tumors using 30 numeric features derived from digitized images of fine needle aspirate (FNA) of breast masses.
XGBoost was chosen for this task because of its well-known strengths in handling structured/tabular data, its built-in regularization that helps prevent overfitting, and its ability to capture complex non-linear relationships between features — all of which make it a strong candidate for medical classification problems.

📊 Dataset Description
PropertyDetailSourceBreast Cancer Wisconsin (Diagnostic) DatasetTotal Samples569Features30 numericTarget Variablediagnosis — Benign (B) or Malignant (M)Class DistributionBenign: 357 (62.7%) · Malignant: 212 (37.3%)Missing ValuesNone
Feature Breakdown
The features are computed from digitized images of FNA biopsies and describe characteristics of cell nuclei present in the image. For each of the following 10 real-valued measurements, three statistics are provided — mean, standard error (SE), and worst (mean of the three largest values) — resulting in 30 features total:
#MeasurementDescription1RadiusMean distance from center to points on the perimeter2TextureStandard deviation of gray-scale values3PerimeterTotal perimeter of the cell nucleus4AreaTotal area of the cell nucleus5SmoothnessLocal variation in radius lengths6CompactnessPerimeter² / Area − 1.07ConcavitySeverity of concave portions of the contour8Concave PointsNumber of concave portions of the contour9SymmetrySymmetry of the cell nucleus10Fractal Dimension"Coastline approximation" − 1 (a measure of boundary complexity)
The dataset is relatively clean with no missing values, making it well-suited for direct modeling without heavy preprocessing.

⚙️ Methodology
1. Preprocessing
Since the dataset is already well-structured, minimal preprocessing was required:

The id column was dropped, as it is a unique identifier with no predictive value.
The diagnosis target column was label-encoded using scikit-learn's LabelEncoder: Benign (B) → 0, Malignant (M) → 1.
All 30 feature columns are already numeric, so no additional encoding or transformation was needed.

2. Train-Test Split
The data was split into 80% training and 20% testing sets using train_test_split with stratify=y to ensure that the class distribution (62.7% B / 37.3% M) is preserved in both the training and testing sets. A fixed random_state=42 was used for reproducibility.
SetSamplesBenignMalignantTraining455~286~169Testing114~71~43
3. Model — XGBClassifier
XGBoost (Extreme Gradient Boosting) is a gradient-boosted decision tree algorithm that builds an ensemble of weak learners (shallow trees) sequentially, where each new tree corrects the errors of the previous ones. It is widely regarded as one of the most effective algorithms for structured/tabular data.
The following hyperparameters were used:
HyperparameterValuePurposen_estimators100Number of boosting rounds (trees)max_depth5Maximum depth of each tree — controls complexitylearning_rate0.1Step size shrinkage to prevent overfittingsubsample0.8Fraction of samples used per tree (adds randomness)colsample_bytree0.8Fraction of features used per tree (adds randomness)eval_metricloglossLogarithmic loss for binary classificationrandom_state42Ensures reproducibility
The subsample and colsample_bytree parameters introduce stochastic elements that help the model generalize better and reduce overfitting, which is especially important on a relatively small dataset of 569 samples.

🏆 Results
Overall Performance
MetricScoreAccuracy~97%AUC-ROC~99%
Classification Report
PrecisionRecallF1-ScoreBenign (0)~0.97~0.99~0.98Malignant (1)~0.98~0.95~0.96
Visualizations Generated
The notebook produces three key visualizations side by side:
✅ Confusion Matrix — A heatmap showing the counts of true positives, true negatives, false positives, and false negatives. This makes it easy to see where the model is making correct predictions and where it is making mistakes.
✅ ROC Curve — A plot of the True Positive Rate (sensitivity) against the False Positive Rate (1 − specificity) at various classification thresholds. The area under this curve (AUC) quantifies the model's overall ability to discriminate between the two classes. An AUC of ~0.99 indicates near-perfect separation.
✅ Top 10 Feature Importances — A horizontal bar chart showing which features contributed the most to the model's predictions. This provides interpretability and helps validate that the model is relying on clinically meaningful features.
