# Depression & Mental Health Risk Prediction

A reproducible end-to-end machine learning project that predicts mental health risk categories (Low / Medium / High) from survey and clinical questionnaire data (PHQ, GAD, Epworth, etc.).  

⚠️ **Disclaimer:** This project is for educational/research use only, not a medical diagnostic tool.

---

## 📑 Table of Contents
- [What I Built](#what-i-built)
- [Dataset](#dataset)
- [Target Definition](#target-definition)
- [Features](#features)
- [Pipeline & Preprocessing](#pipeline--preprocessing)
- [Models & Evaluation](#models--evaluation)
- [Results](#results)
- [Author](#author)

---

## 💡 What I Built
This project:
- Creates a risk label (`mental_health_risk`) from raw survey data,  
- Performs exploratory data analysis (EDA) and feature engineering,  
- Compares Logistic Regression, Random Forest, and XGBoost,  
- Builds a production-ready Scikit-learn pipeline,  
- Saves the trained pipeline (`mh_risk_pipeline_v1.joblib`) with metadata for reuse.

---

## 📊 Dataset
- Data source: [Kaggle - Depression and Anxiety Data](https://www.kaggle.com/datasets/shahzadahmad0402/depression-and-anxiety-data)  
- Local file path in the notebook: `mental_health_data.csv`  

⚠️ Raw dataset is not uploaded here to protect privacy. Please download directly from the source.

---

## 🎯 Target Definition
The target label `mental_health_risk` is rule-based:

- High (2): Suicidal thoughts, or severe depression/anxiety  
- Medium (1): Moderate depression/anxiety or sleepiness  
- Low (0): Otherwise  

---

## 🧾 Features
**Numerical:**
- `age`, `bmi`, `phq_score`, `gad_score`, `epworth_score`

**Categorical:**
- `gender`, `who_bmi`  
- `depression_diagnosis`, `depression_treatment`  
- `anxiety_diagnosis`, `anxiety_treatment`

---

## ⚙️ Pipeline & Preprocessing
- Numeric: Median imputation → StandardScaler  
- Categorical: Most frequent imputation → OneHotEncoder  
- Combined using `ColumnTransformer`  
- Final estimator: Random Forest (best performing model)  

Saved with `joblib`:
- `mh_risk_pipeline_v1.joblib`
- `mh_risk_metadata_v1.joblib`

---

## 🤖 Models & Evaluation
Models compared:
- Logistic Regression
- Random Forest
- XGBoost

Metrics:
- Accuracy  
- F1-score (macro)  
- ROC-AUC (multi-class)  

Random Forest achieved the best balance of accuracy and F1 across classes.

---

## 📈 Results
Example performance summary (check notebook for details):

| Model               | Accuracy | F1-score | ROC-AUC |
|----------------------|----------|----------|---------|
| Logistic Regression | ~0.79    | ~0.73    | ~0.89   |
| Random Forest       | ~0.94    | ~0.88    | ~0.94   |
| XGBoost             | ~0.92    | ~0.86    | ~0.93   |

---

## 🔎 Interpretation

### What the metrics tell us (high-level)
- High overall accuracy and ROC-AUC (Random Forest) indicate the model can separate the broad classes (Low vs High) well on this dataset.  
- Higher F1-score for Random Forest suggests it balances precision and recall better than the Logistic Regression baseline.  
- XGBoost close to Random Forest — gradient boosting provides similar performance and may be preferred after hyperparameter tuning.


### Future Work
- Add SHAP/LIME to explain individual predictions and global feature impacts.
- Use probability thresholds and show uncertainty in UI.
- Validate the rule-based target against clinical labels where possible.
- Improve data quality checks and avoid using features that directly encode the label (label leakage).

### Conclusion
- The pipeline produces a strong proof-of-concept for risk stratification from questionnaire data; ensemble trees (Random Forest / XGBoost) performed best in experiments.
- Important limits: rule-derived labels, potential label leakage, and dataset-specific performance. Do not use this as a clinical decision tool until validated by clinicians and tested on external datasets.
- Next steps: external validation, explainability, threshold tuning for safety, and deployment with monitoring and human oversight.

👤 Author
- Ifeoluwa Boriowo
- 📧 boriowoifeoluwa@gmail.com


