# Machine Learning Pipeline for Predicting IBD Types Using Metabolomics Data

This project develops a machine learning pipeline to classify different types of Inflammatory Bowel Disease (IBD) using metabolomics data.

The pipeline integrates dimensionality reduction, clustering, and supervised classification to identify patterns in metabolite profiles and predict disease categories.

---

# Project Overview

Inflammatory Bowel Disease (IBD) includes several chronic inflammatory disorders of the gastrointestinal tract, primarily:

- Crohn’s Disease (CD)
- Ulcerative Colitis (UC)

Metabolomics data can capture biochemical signatures of these diseases.  
This project builds a machine learning pipeline to classify IBD types based on metabolite profiles.

Dataset characteristics:

- **424 samples**
- **528 variables**
- **522 metabolite features**
- **3 classes**
  - 0: non-IBD
  - 1: Crohn’s Disease
  - 2: Ulcerative Colitis

---

# Machine Learning Pipeline

The workflow follows this pipeline:

EDA → Scaling → UMAP → GMM → XGBoost → SHAP

### 1. Exploratory Data Analysis (EDA)

Exploration of metabolomics dataset including:

- Correlation matrix analysis
- Outlier detection
- Distribution inspection (histograms)

Findings:

- Most metabolite correlations were weak
- Many variables contained outliers
- Feature distributions were highly skewed

---

### 2. Feature Scaling

MinMaxScaler was applied before dimensionality reduction and model training.

Reason:

- Normalises feature ranges
- Improves model stability for tree-based learning

---

### 3. Dimensionality Reduction

UMAP (Uniform Manifold Approximation and Projection) was used to reduce feature dimensionality.

Parameters used:

- `n_components = 2`
- `n_neighbors = 5`
- `min_dist = 0.3`
- `metric = euclidean`

UMAP preserves global data structure while reducing high-dimensional metabolomics data.

---

### 4. Clustering

Gaussian Mixture Model (GMM) was applied to identify latent clusters within the reduced data.

Parameters:

- `n_components = 3`
- `covariance_type = "diag"`

This step allows exploration of metabolomic pattern separation across disease groups.

---

### 5. Classification Model

The final predictive model uses **XGBoost (Extreme Gradient Boosting)**.

Hyperparameters were optimized using:

**10-fold cross-validation with GridSearchCV**

Best parameters:

| Parameter | Value |
|-----------|------|
| colsample_bytree | 0.1 |
| learning_rate | 0.35 |
| max_depth | 1 |
| n_estimators | 160 |
| subsample | 0.8 |
| tree_method | approx |

---

# Model Performance

| Metric | Score |
|------|------|
| Cross-validation accuracy | 0.911 |
| Test accuracy | 0.965 |
| F1 score | 0.964 |

The model demonstrates strong predictive performance for distinguishing IBD subtypes.

---

# Model Explainability

To interpret the model predictions, **SHAP (SHapley Additive Explanations)** was used.

SHAP identifies metabolite features contributing to classification.

Key biomarkers identified:

### non-IBD
- Phosphocholine (34:0)
- Furoylglycine
- Adrenate

### Crohn's Disease
- Butyrate
- Deoxycholate
- Oleoylcarnitine

### Ulcerative Colitis
- Acetylcarnitine
- Ethylglucuronide
- Salicylate

Feature importance varies significantly across disease classes.

---

# Repository Structure
ibd-metabolomics-ml-pipeline
│
├── notebooks
│ └── ibd_metabolomics_ml_pipeline.ipynb
│
├── presentation
│ └── ibd_metabolomics_ml_pipeline.pptx
│
├── requirements.txt
│
└── README.md
