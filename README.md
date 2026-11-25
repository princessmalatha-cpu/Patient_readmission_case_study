# Patient_readmission_case_study
# Hospital Readmission Prediction

## Project Overview
This project predicts whether a patient will be readmitted to hospital using demographic and clinical data. The goal is to help hospitals identify high-risk patients early so they can provide follow-up care and reduce avoidable readmissions.

## Dataset
- 3000 patient records
- Target variable: Readmitted (Yes / No)
- Features: Age, Gender, Blood Pressure, Blood Sugar Levels, Length of Stay, Number of Diagnoses, Previous Admissions, Admission Type

## Methods
1. **Data Cleaning and EDA:** Checked for missing values, duplicates, and class imbalance. Visualised readmission rates by age, length of stay, and clinical factors.
2. **Data Splitting and Balancing:** Split data into 70% train / 30% test with stratification. Applied SMOTE to the training set to balance the classes.
3. **Baseline Model:** Random Forest Classifier with default threshold of 0.5.
4. **Model Improvement:** Threshold tuning and Random Forest with class_weight='balanced_subsample'.
5. **Model Comparison:** Compared Random Forest vs Logistic Regression.
6. **Feature Importance:** Analysed which factors drive readmission.

## Results

### Model Comparison

| Model | Recall for Yes | Precision for Yes | Accuracy | Missed Readmissions |
| --- | --- | --- | --- | --- |
| Baseline Random Forest (Threshold 0.5) | 0.08 | 0.22 | 0.65 | 159 |
| Threshold Tuned Random Forest (Threshold 0.25) | 0.76 | 0.29 | 0.40 | 42 |
| **Final Model: Random Forest + class_weight (Threshold 0.35)** | **0.92** | **0.29** | **0.33** | **13** |
| Logistic Regression (Threshold 0.5) | 0.48 | 0.28 | - | 90 |

Logistic Regression was rejected because at thresholds below 0.5 it predicted Yes for all patients, achieving 100% recall but providing no discrimination.

### Feature Importance - Final Model

| Rank | Feature | Importance |
| --- | --- | --- |
| 1 | Blood Sugar Levels | 22.50% |
| 2 | Blood Pressure | 19.03% |
| 3 | Age | 17.16% |
| 4 | Length of Stay | 16.63% |
| 5 | Number of Diagnoses | 9.73% |
| 6 | Previous Admissions | 7.29% |
| 7 | Gender and Admission Type | < 3% each |

The top 4 features together account for over 75% of the model's decisions.

## Conclusion
This project aimed to predict hospital readmission using patient demographic and clinical data. The baseline Random Forest model achieved 65% accuracy but only 8% recall for readmitted patients, missing 159 of 173 readmissions, which made it unsuitable for clinical use. Through threshold tuning and the use of class_weight='balanced_subsample', the final model improved recall to 92%, reducing missed readmissions to just 13, although this came at the cost of lower accuracy (33%) and precision (29%) due to a high number of false positives. Feature importance analysis showed that readmission was driven primarily by Blood Sugar Levels (22.5%), Blood Pressure (19.0%), Age (17.2%), and Length of Stay (16.6%), which together accounted for over 75% of the model's decisions. The model is therefore best used as a screening tool to flag high-risk patients for follow-up, rather than as a standalone discharge decision tool, and future work should explore richer data such as medication history and comorbidities to improve precision.

## How to Run
1. Open the notebook in Databricks.
2. Click Run All.
3. Check the final model outputs for threshold 0.35 and feature importance.

## Tools Used
- Python, Pandas, Scikit-learn, Matplotlib
- Databricks
