Predicting 30-day Hospital Readmission Risk using Databricks
---
Sponsor: Databricks
Organisers: Indian Data Club (IDC) & Codebasics

Hashtags:

ResumeProjectChallenge #DatabricksWithIDC #Codebasics

#📌Overview
---
Hospital readmissions within 30 days significantly increase healthcare costs
and indicate gaps in post-discharge care.
This project builds an end-to-end AI-powered decision support system that
predicts whether a diabetic patient is at high risk of hospital readmission
within 30 days at the time of discharge.
The solution is designed and implemented entirely on Databricks using
Medallion Architecture, Delta Lake, MLflow, and SQL analytics.

#📽️ Project Walkthrough
---
▶️ Video (10 mins, unlisted):

#📊 Presentation Deck
-----
The presentation used in the walkthrough is available here: ( https://docs.google.com/presentation/d/1tEoerKcLLAVYkV2i6tJSdwvKNGdOtniR/edit?usp=sharing&ouid=104979890987984862628&rtpof=true&sd=true )
----
## 🚀 Live Dashboard Access
🔗 **Healthcare Readmission AI – Interactive Dashboard:**  
👉 <https://healthcare-readmission-app-fvdrqj4vgjnvdp2qxfjje7.streamlit.app/#healthcare-readmission-dashboard-analysis>
---

> An executive-ready dashboard built on Databricks that visualizes patient readmission risk, utilization patterns, and clinical drivers to support proactive healthcare decisions.
---
#Problem Statement
---
Hospitals struggle to identify which patients are likely to be readmitted
within 30 days after discharge.

The challenge is to:
- Predict 30-day readmission risk accurately
- Avoid data leakage
- Translate predictions into actionable risk categories
- Enable proactive care decisions instead of reactive treatment
#Why AI (Instead of Rule-Based Systems)
---
Rule-based systems fail to capture complex patient behavior and interactions
between multiple clinical and utilization factors.

Machine Learning is required to:
- Learn patterns from historical patient data
- Generalize risk beyond fixed thresholds
- Adapt to complex, non-linear relationships
#Dataset Description


---

# README: Diabetes 130-US Hospitals (1999–2008)

## 📌 Dataset Overview
- **Source**: UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008) 
- **Donated on**: May 2, 2014  
- **Domain**: Health and Medicine  
- **Instances**: 101,766 patient records  
- **Features**: 47 attributes (categorical + integer)  
- **Time Period**: 1999–2008  
- **Hospitals**: 130 US hospitals and integrated delivery networks  

This dataset represents **ten years of clinical care** for patients diagnosed with diabetes. Each record corresponds to a hospital admission (inpatient encounter) where laboratory tests and medications were administered, with a stay between **1–14 days**.

---

## 🎯 Objective
The primary goal is to **predict early readmission within 30 days of discharge**.  
This is important because:
- Poor diabetes management increases hospital costs.  
- Readmissions affect patient morbidity and mortality.  
- Proper glycemic control and preventive care can reduce complications.  

---

## 📂 Meta Data
- **diabetic_data.csv (18.3 MB)** → Main dataset  
- **IDS_mapping.csv (2.5 KB)** → Mapping of categorical IDs to descriptive values  

---

## 🧾 Data Characteristics
- **Type**: Multivariate  
- **Tasks**: Classification, Clustering  
- **Sensitive Attributes**: Age, Gender, Race  

### Example Features
| Feature | Type | Description |
|---------|------|-------------|
| encounter_id | ID | Unique identifier of encounter |
| patient_nbr | ID | Unique identifier of patient |
| race | Categorical | Caucasian, Asian, African American, Hispanic, Other |
| gender | Categorical | Male, Female, Unknown |
| age | Categorical | Grouped in 10-year intervals |
| admission_type_id | Categorical | Emergency, urgent, elective, newborn, etc. |
| discharge_disposition_id | Categorical | 29 values (home, expired, etc.) |
| time_in_hospital | Integer | Number of days admitted |
| num_lab_procedures | Integer | Number of lab tests performed |
| HbA1c_result | Categorical | Glycated hemoglobin test result |
| num_medications | Integer | Number of medications prescribed |

---

## ⚠️ Missing Values
- Some attributes (e.g., race, weight) contain missing values.  
- Preprocessing is required before applying ML models.  

---

## 📖 Reference Paper
- **Impact of HbA1c Measurement on Hospital Readmission Rates: Analysis of 70,000 Clinical Database Patient Records**  
  Authors: Beata Strack, Jonathan DeShazo, Chris Gennings, Juan Olmo, Sebastian Ventura, Krzysztof Cios, John Clore  
  Published: *BioMed Research International*, 2014  

---

## ✅ Usage Notes
- Recommended splits: Train/Test or Train/Validation/Test.  
- Suitable for tasks like **predictive modeling**, **risk stratification**, and **healthcare analytics**.  
- Handle sensitive attributes responsibly (age, race, gender).  

---
# Solution Architecture (Medallion Design)
----
Bronze Layer
- Raw, unchanged dataset ingestion
- Source of truth

Silver Layer
- Data cleaning and preprocessing
- Leakage removal
- Feature engineering
- ML-ready dataset

Gold Layer
- Business-focused features
- Risk segmentation (High / Medium / Low)
- Decision-ready tables

ML Layer
- Logistic Regression model
- MLflow experiment tracking

Analytics Layer
- Databricks SQL dashboards
- Risk and utilization insights
# Technology Stack
---
- Databricks Community Edition
- Delta Lake (ACID, versioning)
- PySpark
- MLflow
- Databricks SQL
- Streamlit (Web deployment)
---
# Feature Engineering Highlights
---
Key engineered features include:
- Age buckets for interpretability
- Hospital utilization score combining visit counts
- Treatment change flag indicating instability
- Leakage-free target label (readmit_30d)
---
# Machine Learning Approach
- Problem Type: Binary Classification
- Model Used: Logistic Regression
- Reason: Explainability, reliability, healthcare suitability
- Evaluation Metric: AUC (handles class imbalance)
---
# Experiment Tracking with MLflow
MLflow is used to:
- Track model parameters
- Log evaluation metrics
- Maintain reproducibility
- Enable model comparison
---
# Analytics & Dashboard
Databricks SQL dashboards provide:
- Risk distribution across patients
- Risk by age group
- Relationship between utilization and readmission
- Executive-level summary insights
---
# Buisness Impact
This system enables hospitals to:
- Identify high-risk patients early
- Prioritize post-discharge care
- Reduce avoidable readmissions
- Optimize resource planning
---
#📂 Project Structure
Healthcare_Readmission_AI
│

├── 00_DOCS

├── 01_bronze_ingestion

├── 02_silver_processing

├── 03_gold_features

├── 04_ml_mlflow

├── 05_sql_analytics

├── 06_jobs_orchestration

├── Dashboard

└── README.md

---
# Model Evaluation
The moderate AUC score reflects the inherent complexity and noise in real-world healthcare data, reinforcing the importance of combining ML outputs with domain-driven decision rules.
<img width="1920" height="1080" alt="Screenshot (176)" src="https://github.com/user-attachments/assets/8e1710a9-248a-4fff-b3d5-4ca0adf2c36d" />


*Results:*
- ROC-AUC: ~0.60
- Accuracy: ~0.89
All experiments, parameters, and metrics were tracked using MLflow to ensure reproducibility and auditability.
---
# AI Decision System (Beyond Just Prediction)
Instead of stopping at raw prediction probabilities, this project implements a decision layer on top of the ML model.

Model outputs are transformed into actionable risk categories:
- *Low Risk*: No immediate intervention required
- *Medium Risk*: Follow-up monitoring recommended
- *High Risk*: Proactive care planning suggested

Risk buckets are derived using quantile-based thresholds on predicted readmission probability, ensuring stable and interpretable segmentation.

This approach bridges the gap between machine learning outputs and real-world clinical decision-making, enabling healthcare teams to prioritize patients effectively rather than interpreting raw model scores.


#Orchestration

The pipeline is automated using Databricks Jobs with task dependencies:
Bronze → Silver → Gold → ML Training

---

#Challenge Requirements Compliance
---
This project was developed as part of the Codebasics Resume Project Challenge, sponsored by Databricks and organised by Indian Data Club (IDC) and Codebasics.

This project satisfies all challenge requirements by:
- Framing a real-world healthcare decision problem
- Designing a Medallion-based data architecture
- Implementing ML with experiment tracking
- Translating predictions into business actions
- Delivering dashboards and documentation
---
# 🔮 Future Improvements 

This project establishes a strong end-to-end foundation for hospital readmission risk prediction.  
Future enhancements can further improve accuracy, scalability, and real-world adoption:

- **Advanced Models**: Experiment with tree-based models (Random Forest, XGBoost) or ensemble methods to capture non-linear patient risk patterns.

- **Feature Expansion**: Incorporate additional clinical signals such as lab trends, diagnosis history, and medication sequences for richer patient profiling.

- **Time-Aware Modeling**: Move from static features to temporal models that account for patient history across multiple encounters.

- **Threshold Optimization**: Tune decision thresholds based on hospital capacity, cost sensitivity, or patient risk tolerance.

- **Model Explainability**: Integrate SHAP or feature attribution techniques to provide clinician-friendly explanations for predictions.

- **Continuous Training**: Enable scheduled retraining using Databricks Jobs to keep the model updated with new data.

- **Governance & Monitoring**: Add model drift detection, data quality checks, and audit logging for production-grade reliability.

- **Clinical Workflow Integration**: Embed predictions into hospital systems or care management tools for real-time discharge decision support.
---

## 👤 Author & Project Owner

**Shouvik Sarkar**  
Aspiring Data Engineer | Data Scientist  
Specialization: Healthcare Readmission AI, Databricks, ML Pipelines  

🔗 **LinkedIn Profile:**  
www.linkedin.com/in/shouvik-sarkar-619782279

📩 Open to collaboration, feedback, and opportunities in Data Engineering & AI-driven Healthcare Analytics.

---
