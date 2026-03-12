# Machine Learning Pipeline for Predicting IBD Types Using Metabolomics Data

This project develops a machine learning pipeline to classify inflammatory bowel disease (IBD) types using metabolomics data.

## Dataset
- 424 samples
- 528 variables (522 metabolites)
- Classes:
  - 0: non-IBD
  - 1: Crohn's Disease
  - 2: Ulcerative Colitis

## Machine Learning Pipeline

MinMaxScaler → UMAP → GMM → XGBoost

### Steps

1. Exploratory Data Analysis
   - Correlation matrix
   - Outlier detection
   - Distribution analysis

2. Dimensionality Reduction
   - UMAP

3. Clustering
   - Gaussian Mixture Model

4. Classification
   - XGBoost

Hyperparameters were optimized using **10-fold GridSearchCV**.

## Results

| Metric | Value |
|------|------|
| Cross-validation accuracy | 0.911 |
| Test accuracy | 0.965 |
| F1-score | 0.964 |

## Feature Importance

SHAP analysis identified key metabolites for each disease class.

Example biomarkers:

- Crohn’s Disease: Butyrate, Deoxycholate
- Ulcerative Colitis: Acetylcarnitine
- non-IBD: Phosphocholine (34:0)

## Tech Stack

Python  
Scikit-learn  
XGBoost  
UMAP  
SHAP  
Pandas / NumPy

## Project Structure
