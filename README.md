# Credit Risk Modeling & Loan Approval Classification using XGBoost (Banking Sector)

This project presents an end-to-end **credit risk modeling pipeline** for predicting multi-class loan approval categories (P1–P4) using real banking customer and bureau data. The objective is to perform **statistically driven feature selection, risk segmentation, and model validation** using machine learning classifiers with a strong focus on **probability-based risk interpretation**.

---

## Objective
- Analyze banking customer and credit bureau data to understand drivers of loan approval risk.
- Perform statistically sound feature selection using **Chi-Square, VIF, and ANOVA**.
- Build multi-class classification models to predict loan approval buckets (P1–P4).
- Compare multiple models and select the most stable risk predictor.
- Evaluate model performance using **accuracy, precision, recall, and F1-score**.

---

## Dataset Description
The project uses two real-world banking datasets:

- **case_study1.xlsx** – Customer demographic and application-level variables  
- **case_study2.xlsx** – Credit behavior, bureau history, and financial attributes  

Key properties:
- Target variable: `Approved_Flag` (P1, P2, P3, P4)
- Unique Key: `PROSPECTID`
- Missing values encoded as `-99999` and handled using rule-based cleaning
- Final dataset obtained through **inner join on PROSPECTID**

---

## Data Cleaning & Preprocessing
- Removed rows with invalid sentinel values (`-99999`) from key numerical fields.
- Dropped columns with excessive missing sentinel values.
- Ensured clean numeric distributions before statistical testing.
- Converted categorical variables into machine-readable format using:
  - Ordinal encoding for `EDUCATION`
  - One-hot encoding for marital status, gender, and product enquiry features.
- Applied feature scaling (StandardScaler) to selected numerical attributes.

---

## Statistical Feature Selection
To ensure **model stability and interpretability**, statistical techniques were applied before modeling:

### 1. Chi-Square Test (Categorical Features)
Used to test dependency between categorical variables and `Approved_Flag`:
- `MARITALSTATUS`
- `EDUCATION`
- `GENDER`
- `last_prod_enq2`
- `first_prod_enq2`

Only statistically significant variables (p-value ≤ 0.05) were retained.

### 2. VIF (Variance Inflation Factor)
Used to detect and remove **multicollinearity** among numerical predictors.  
All variables with **VIF > 6** were iteratively removed to reduce redundancy and instability.

### 3. ANOVA (Numerical Feature Significance)
Performed one-way ANOVA across approval classes (P1–P4) to retain only those numerical features that showed **statistically significant variation across risk classes**.

---

## Final Feature Set
The final modeling dataset consists of:
- Statistically significant numerical predictors (after VIF + ANOVA)
- Statistically significant categorical predictors (after Chi-Square)
- Target variable: `Approved_Flag`

All predictors are fully numeric after encoding.

---

## Models Implemented
Three supervised learning models were trained and evaluated:

1. **Random Forest Classifier**
2. **Decision Tree Classifier**
3. **XGBoost Classifier (Primary Model)**

The task is a **multi-class classification problem** with four approval categories (P1–P4).

---

## Model Training & Validation
- Data split: **80% Training / 20% Testing**
- Stratified sampling used to preserve class distribution.
- Performance evaluated using:
  - Accuracy
  - Class-wise Precision
  - Recall
  - F1-score

---

## Model Performance
- **Best Model:** XGBoost Classifier  
- **Best Test Accuracy:** **0.78**
- Strong class-wise precision and recall across all approval categories.
- XGBoost selected as final model due to superior predictive stability and generalization.

---

## Hyperparameter Tuning
A manual grid search was performed on XGBoost using combinations of:

- `colsample_bytree`
- `learning_rate`
- `max_depth`
- `alpha`
- `n_estimators`

Both **training and test accuracy** were recorded for each configuration to detect:
- Overfitting
- Underfitting
- Best generalizing parameter set

---

## Key Learnings
- Practical application of **statistical feature validation before machine learning**.
- Understanding the impact of multicollinearity using VIF.
- Multi-class credit risk modeling using tree-based ensemble methods.
- Translating model outputs into **probability-based risk segments**.
- Importance of **signal validation using class-wise metrics**, not just accuracy.

---

## Business & Financial Applications
- Retail banking loan approval systems
- Credit underwriting and risk grading
- Customer risk segmentation
- Regulatory risk modeling support
- Portfolio-level default risk assessment

---

## Tools & Technologies
- Python
- Pandas, NumPy
- Scikit-learn
- XGBoost
- SciPy, Statsmodels
- Matplotlib

---
