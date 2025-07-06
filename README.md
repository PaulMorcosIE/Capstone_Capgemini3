# Capstone Project – IE University - Capgemini 3 
## 📦 Predictive Packaging Quality Control System for FashionWorld  
**Group 3 – Capgemini 3**  
- Enrico Miguel Cordero Tajanlangit (<enricotajanlangit@student.ie.edu>)  
- Paul Morcos Douaihy (<paul.morcos@student.ie.edu>)  
- Joy Zhong (<joy.zhong@student.ie.edu>)  
- Maria Brito e Abreu (<mariabritoeabreu@student.ie.edu>)  
- Sarina Ratnabhas (<sarina.ratnabhas@student.ie.edu>)  

---
[ Dashboard Demo Video](https://www.youtube.com/watch?v=er7b_SyiuPA)
[Power BI Dashboard](https://app.powerbi.com/links/kf1jbQbuE7?ctid=4a39c578-6df0-42b9-a7e0-e9eac6d91816&pbi_source=linkShare&bookmarkGuid=bc6f87e5-b479-4d70-8455-23fb5ae7dff4)

---

## 📖 Executive Summary

This project delivers an enterprise-ready solution to proactively detect defective packaging in FashionWorld’s global supply chain. The system integrates automated data cleaning, exploratory analysis, predictive modeling, and business dashboards. It replaces manual quality checks with AI-driven inspection triggers and gives operational stakeholders real-time visibility into packaging quality.

**Business objectives achieved:**
- Minimize packaging defects via early identification
- Reduce manual inspection costs and delays
- Benchmark supplier performance using ML-driven KPIs
- Enable transparent, real-time oversight

---

## 🗂️ Repository Structure

```
project-root/
├── data/
│   ├── raw/           # Vendor-supplied packaging reports, product attributes, supplier metrics
│   ├── processed/     # Cleaned datasets (post-cleaning, pre-EDA)
│   └── merged/        # Final feature-engineered dataset for modeling (merged_df.csv)
├── Data_Cleaning.ipynb    # Raw-to-clean transformation pipeline
├── EDA.ipynb              # Exploratory insights and visual analytics
├── Modeling.ipynb         # Full modeling lifecycle (prep, training, tuning, SHAP)
└── README.md              # Documentation
```

---

## 🧹 1. Data Cleaning (`Data_Cleaning.ipynb`)

Comprehensive harmonization of four primary datasets:
- **Density Report**:
  - Standardized product and supplier identifiers.
  - Removed anomalous entries and null values.
- **Supplier Scorecard**:
  - Cleaned headers and standardized supplier naming.
- **Product Attributes**:
  - Passed data validation checks.
- **Historical Incidents**:
  - Cleaned references and unified naming across sources.

---

## 📊 2. Exploratory Data Analysis (`EDA.ipynb`)

Key insights:
- Certain folding methods and layouts correlate with higher failure rates.
- Product type and material influence defect risk (e.g., wool, linen).
- Normalized bad packaging rates are more reliable than raw incident counts.

Features engineered:
- Binary risk indicators (supplier, product history)
- Temporal markers (month, weekday)
- Dimensionality reduction through feature filtering

---

## 🤖 3. Modeling Pipeline (`Modeling.ipynb`)

### Objective
Predict whether a package is **Good (0)** or **Bad (1)** before arrival, prioritizing early detection of defects.

### Strategy
- Combined structured product, supplier, and incident data into a unified modeling dataset.
- Categorical encoding and feature engineering applied.
- Evaluated several models using cross-validation and recall-focused metrics.
- Final model selected based on sensitivity to defective cases and operational fit.

### Explainability
Used SHAP analysis to validate key drivers of packaging risk:
- Historical defect rates
- Product-specific vulnerability
- Operational volume

---

## ⚙️ Running the Pipeline

### Requirements
```bash
Python 3.8+
pandas, numpy, matplotlib, seaborn
scikit-learn, xgboost, lightgbm, catboost
shap, jupyter
```

### Instructions
1. Open `Data_Cleaning.ipynb` → run all cells → output: `processed/` data.
2. Open `EDA.ipynb` → generate insights → output: `merged_df.csv`.
3. Open `Modeling.ipynb` → train/evaluate model and interpret results.

---

## 📬 Contact

For technical inquiries or collaboration opportunities, reach out via student emails above.
