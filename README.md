# Medical Insurance Claim Prediction and Risk Segmentation
### Big Data & Databases Project (KNIME)

This repository contains a **big data analytics project** focused on predicting medical insurance claims and identifying policyholder risk segments using a large, real-world healthcare dataset.

The project was implemented entirely in **KNIME**, combining data preparation, feature engineering, supervised learning, and unsupervised clustering to support insurance risk assessment, pricing, and managerial decision-making.

---

## 🎯 Project Objectives

The analysis addresses three core insurance questions:

1. **Claim occurrence**  
   Can we predict whether a policyholder will file at least one claim?

2. **Claim severity**  
   Can we predict how much a policyholder will claim in total?

3. **Risk segmentation**  
   Can we identify distinct groups of policyholders with different risk and utilization profiles?

---

## 📊 Dataset

- **Source**: Medical Insurance Cost Prediction dataset (Kaggle)
- **Size**: ~100,000 policyholders, 50+ variables
- **Data types**:
  - Demographics (age, sex, income, household size)
  - Health indicators (BMI, blood pressure, chronic conditions)
  - Lifestyle factors (smoking, alcohol use)
  - Utilization history (visits, hospitalizations)
  - Insurance characteristics (deductible, copay, plan type)

### Target Variables
- `filed_claim` (binary): whether at least one claim was filed  
- `total_claims_paid` (continuous): total annual claim amount (USD)

---

## 🧹 Data Preparation & Quality Assurance

Key preprocessing steps:
- Automated type casting and data validation
- Missing-value and duplicate checks (none detected)
- Outlier analysis using boxplots and IQR criteria
- Retention of high-cost outliers (expected in insurance data)
- Creation of the `filed_claim` target using rule-based logic

Special care was taken to **prevent data leakage**:
- Variables derived from claims or post-event information were removed
- Features unavailable at prediction time were excluded
- Separate feature sets were used for regression and classification

---

## 🧠 Modeling Approach

### Regression (Claim Severity)
Goal: Predict `total_claims_paid`

Models tested:
- Linear Regression (baseline)
- Tweedie GLM (frequency–severity modeling)
- Random Forest Regression
- Gradient Boosting Regression

Evaluation metrics:
- RMSE, RMSLE, R²

**Key result**:  
Gradient Boosting achieved the best overall performance, although all models struggled with rare, extreme high-cost claims due to heavy-tailed distributions.

---

### Classification (Claim Occurrence)
Goal: Predict `filed_claim`

Models tested:
- Logistic Regression
- Random Forest Classification
- Gradient Boosting Classification

Evaluation metrics:
- Accuracy
- Precision / Recall / F1
- AUC (ROC)

**Key result**:  
Gradient Boosting provided the strongest discrimination between claimants and non-claimants, though performance remained moderate due to class imbalance and nonlinear risk patterns.

---

## 🔍 Unsupervised Learning: Risk Segmentation

To uncover hidden structure in the data:
- Features were standardized
- **PCA** was applied to reduce dimensionality
- **K-Means clustering (k = 2)** identified:
  - A low-risk majority cluster
  - A smaller, high-risk cluster with higher age, BMI, and chronic condition prevalence

These clusters support targeted pricing, preventive care, and efficient resource allocation.

---

## 📈 Key Insights

- Claim behavior is highly nonlinear and dominated by rare, extreme events
- Linear models offer interpretability but limited predictive accuracy
- Tree-based models improve performance but still underpredict extreme costs
- Health status and utilization history dominate demographic predictors
- False negatives (missed claimants) are more costly than false positives in insurance settings

---   

## 📁 Repository Structure

''' text
├── data/
│   └── medical_insurance.csv
├── report/
│   └── Big_Data_&_Databases_Group_01_Presentation.pdf
└── README.md

---

## 🔗 KNIME Workflow

Download KNIME workflow (code.knwf)

Due to GitHub file size limitations, the KNIME workflow file is hosted externally.

👉 Download link:
https://drive.google.com/uc?id=1rYFW4BIPJPnemPzkDRG-3aNhyZGbcSbL&export=download

How to run the workflow:
1. Download code.knwf
2. Place it in your KNIME workspace
3. Open it using KNIME Analytics Platform
4. Execute the workflow from start to finish


