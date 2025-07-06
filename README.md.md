
# Capstone Project – IE University  
### Predictive Packaging Quality Control System  
**Group 3**  
- Enrico Miguel Cordero Tajanlangit (<enricotajanlangit@student.ie.edu>)  
- Paul Morcos Douaihy (<paul.morcos@student.ie.edu>)  
- Joy Zhong (<joy.zhong@student.ie.edu>)  
- Maria Brito e Abreu (<mariabritoeabreu@student.ie.edu>)  
- Sarina Ratnabhas (<sarina.ratnabhas@student.ie.edu>)  

---

## 📦 Project Overview

This project delivers a predictive quality control framework for proactively identifying defective packaging units in a fashion supply chain. It leverages historical reports, product attributes, and supplier performance metrics to train a machine learning model capable of early defect detection. The ultimate business objective is to reduce operational risk and manual reinspection costs by flagging likely failures in advance of shipment.

---

## 🗂️ Data Architecture

The data architecture consists of three structured directories:

```
data/
├── raw/           # Original CSV/XLSX files from vendors and internal sources
├── processed/     # Cleaned and intermediate datasets (after parsing, formatting, filtering)
└── merged/        # Final integrated datasets with engineered features (main input for modeling)
```

- The **merged dataset** (e.g., `merged_df.csv`) represents the central modeling repository.
- All cleaning, feature engineering, and modeling efforts are built upon the merged layer.

---

## ⚙️ Workflow Summary

### 1. Data Cleaning (`Data_Cleaning.ipynb`)
- Removed redundant columns and standardized missing values.
- Parsed date fields and standardized naming conventions.
- Imputed incident-related null values using domain-specific logic (e.g., filling zeros for unresolved entries).

### 2. Feature Engineering & EDA (`EDA.ipynb`)
- Created supplier-level and product-level defect rate metrics.
- Constructed binary flags: `is_high_risk_supplier`, `is_low_delivery_perf`, `is_bad_incident_history`.
- Extracted calendar features: report month, quarter, day-of-week, weekend indicator.
- Ordinal encoding applied to categorical variables for tree-based model compatibility.
- Irrelevant and high-correlation features removed to reduce noise and leakage.

### 3. Modeling (`Modeling.ipynb`)
- Evaluated: XGBoost, CatBoost, LightGBM, Random Forest, Logistic Regression.
- Tuned with 5-fold stratified cross-validation.
- Customized scoring via `make_scorer(recall_score, pos_label=1)` to prioritize recall on minority class (`Bad` = 1).
- Final model: **XGBoost**, with `learning_rate=0.01`, `max_depth=5`, `n_estimators=100`.

---

## 📈 Performance Metrics (Test Set)

| Model                | Precision (Bad) | Recall (Bad) | F1 Score (Bad) | Accuracy | ROC AUC |
|---------------------|------------------|---------------|----------------|----------|---------|
| XGBoost (Selected)  | 0.32             | 0.70          | 0.44           | 0.64     | 0.7252  |
| CatBoost            | 0.32             | 0.70          | 0.44           | 0.65     | 0.7257  |
| LightGBM            | 0.32             | 0.70          | 0.44           | 0.64     | 0.7252  |
| Random Forest       | 0.32             | 0.68          | 0.44           | 0.65     | 0.7252  |
| Logistic Regression | 0.32             | 0.69          | 0.44           | 0.65     | 0.7250  |

Focus metric: **Recall (Bad)** — aligned with business-critical risk avoidance strategy.

---

## 🔍 Explainability (SHAP Analysis)

- `BadPackagingRatePct` and `product_bad_rate` are the most impactful predictors of defective packaging.
- Operational load (`PackagesHandled`) and high-cost incident histories contribute to risk.
- Categorical flags such as `Material_Wool` and `ProposedFoldingMethod` reveal design-level vulnerabilities.
- SHAP force plots provide local interpretability for individual predictions.

---

## 🎯 Threshold Sensitivity

- Recall ranged from 1.00 at low thresholds (0.2) to 0.40 at high thresholds (0.6).
- Default threshold (0.5) achieves strong balance: Recall = 0.70, with moderate precision.
- Threshold tuning remains available depending on inspection capacity and tolerance for false positives.

---

## 🗃️ Project Structure

```
project-root/
├── data/
│   ├── raw/                   # Raw input files (supplier sheets, product specs, etc.)
│   ├── processed/             # Intermediate preprocessed files
│   └── merged/                # Final engineered datasets
│       └── merged_df.csv
├── Data_Cleaning.ipynb        # Full cleaning and standardization pipeline
├── EDA.ipynb                  # Exploratory data analysis and feature engineering
├── Modeling.ipynb             # Model training, tuning, SHAP explanations
└── README.md                  # Project documentation
```

---

## 🧪 Environment Setup

### Requirements

- Python 3.8+
- Jupyter
- pandas, numpy
- scikit-learn
- xgboost, catboost, lightgbm
- shap
- matplotlib, seaborn

### Running the Pipeline

1. Clone this repository or upload to Google Colab.
2. Execute `Data_Cleaning.ipynb` to prepare datasets.
3. Execute `EDA.ipynb` to engineer features and save `merged_df.csv`.
4. Execute `Modeling.ipynb` to train and evaluate the final model.

---
