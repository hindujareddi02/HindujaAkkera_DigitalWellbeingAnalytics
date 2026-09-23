# Digital Wellbeing Analytics
## Analyzing the Relationship Between Digital Habits, Lifestyle and Student Productivity

## 1. Project Overview

This project analyzes the relationship between students' digital habits, lifestyle factors, wellbeing indicators, academic behaviors, and productivity.

The project combines two stages:

- Exploratory data analysis, correlation analysis, productivity-group analysis, final-grade analysis, and NumPy-based linear regression.
- Target forensics, target-structure investigation, multiple machine-learning models, feature engineering, productivity classification, and explainable AI.

The analysis uses the **Student Productivity & Digital Distraction Dataset**, containing **20,000 student records and 18 variables**.

---

## 2. Objectives

The main objectives are:

- Analyze students' digital usage patterns.
- Examine relationships between digital habits and productivity.
- Investigate the association of sleep, stress, focus, study hours, and attendance with productivity.
- Compare low-, medium-, and high-productivity students.
- Examine the relationship between productivity-related variables and final grades.
- Investigate the structure of the supplied productivity score.
- Compare multiple regression models.
- Test whether engineered features improve prediction.
- Classify students into Low, Medium, and High productivity groups.
- Explain individual model predictions using feature contributions.

---

## 3. Dataset

**Dataset:** Student Productivity & Digital Distraction Dataset

**Size:** 20,000 records and 18 columns

The dataset contains information related to:

- Age and gender
- Study hours
- Sleep hours
- Phone usage
- Social media usage
- YouTube usage
- Gaming
- Breaks
- Coffee intake
- Exercise
- Assignments completed
- Attendance
- Stress
- Focus
- Final grade
- Productivity score

### Dataset Source

Kaggle:

https://www.kaggle.com/datasets/sehaj1104/student-productivity-and-digital-distraction-dataset

Dataset file used in the project:

`student_productivity_distraction.csv`

---



## 4. Section 1 Workflow

 Section 1 follows this workflow:

1. Dataset loading
2. Data quality assessment
3. Exploratory data analysis
4. Digital usage analysis
5. Correlation analysis
6. Productivity-group analysis
7. Digital behavior analysis
8. Final-grade analysis
9. NumPy-based linear regression
10. Model evaluation
11. Interpretation of results

## 5. Data Quality Assessment

The dataset was checked for:

- Missing values
- Duplicate records
- Data types
- Unique values
- Descriptive statistics

The dataset contains:

- 20,000 records
- 18 variables
- 0 missing values
- 0 duplicate rows

Therefore, no missing-value imputation or duplicate-removal procedure was required.

## 6. Exploratory Data Analysis

The project examines:

- Phone usage
- Social media usage
- YouTube usage
- Gaming
- Phone usage vs sleep
- Phone usage vs focus
- Correlations among numerical variables

## 7. Major Findings

The strongest linear associations with productivity score were:

| Variable | Correlation |
|---|---:|
| Study hours | +0.73 |
| Focus score | +0.41 |
| Sleep hours | +0.34 |
| Phone usage | -0.33 |
| Stress level | -0.20 |
| Attendance | +0.18 |

Social media, YouTube, and gaming hours showed negligible linear associations with productivity.

## 8. Productivity Group Analysis

Students were divided into Low, Medium, and High productivity groups using productivity-score tertiles.

From low to high productivity groups:

- Study hours increased from approximately 2.92 to 7.57 hours/day.
- Sleep increased from approximately 5.79 to 7.24 hours/day.
- Phone usage decreased from approximately 7.40 to 5.10 hours/day.
- Stress decreased from approximately 6.09 to 4.93.
- Focus increased from approximately 55.78 to 73.34.
- Attendance increased from approximately 66.75% to 73.05%.

## 9. Final Grade Analysis

The measured behavioral and productivity variables showed very weak linear associations with final grade.

The correlation between productivity score and final grade was approximately **0.002**.

Therefore, the project does not claim that the productivity score predicts or causes higher academic grades.

## 10. Machine Learning

A NumPy-based multiple linear regression model was implemented.

### Input Features

- Study hours
- Sleep hours
- Phone usage
- Social media hours
- YouTube hours
- Gaming hours
- Breaks
- Coffee intake
- Exercise
- Assignments completed
- Attendance
- Stress
- Focus

### Model Setup

- 80% training data
- 20% testing data
- Random seed: 42
- Training-set standardization
- NumPy least-squares regression

### Results

| Metric | Result |
|---|---:|
| MAE | 0.003 |
| RMSE | 0.003 |
| R² | 1.000 |

The unusually high performance was interpreted cautiously because the supplied productivity score appears highly structured.

---


## 11. Section 2 Workflow

Section  2 extends the project through:

1. Target forensics
2. Data preparation
3. Feature engineering
4. Multiple machine-learning models
5. Cross-validation
6. Productivity classification
7. Explainable AI
8. Integrated interpretation

## 12. Target Forensics

Six variables were investigated in detail:

- `study_hours_per_day`
- `sleep_hours`
- `phone_usage_hours`
- `attendance_percentage`
- `stress_level`
- `focus_score`

Using all six variables, linear regression produced:

- **R² = 0.9999999682**
- **MAE = 0.002487**
- **RMSE = 0.002869**

Removing individual variables caused substantial changes in predictive performance, providing evidence that these six variables contain most of the information needed to reconstruct the supplied productivity score.

## 13. Hidden Formula Investigation

The learned coefficients showed a highly regular relative-weight pattern.

The approximate simplified relationship was:

`Productivity Score ≈ -6.2388 + 4.3164(study hours) + 2.6977(sleep hours) - 1.6186(phone usage) + 0.1619(attendance) - 1.0791(stress) + 0.3237(focus)`

A simplified weight structure reproduced the supplied target with:

- **R² = 0.9999999677**
- **MAE = 0.002499**
- **RMSE = 0.002892**

This provides strong evidence that the target variable has a highly structured mathematical relationship with the six selected variables.

**Important:** This does not prove that the dataset creator used this exact formula.

## 14. Machine Learning Benchmark

Five-fold cross-validation was used to compare several regression models.

| Model | Test R² | Test MAE | Test RMSE | CV R² |
|---|---:|---:|---:|---:|
| Linear Regression | 1.000000 | 0.002484 | 0.002874 | 1.000000 |
| Ridge | 1.000000 | 0.002605 | 0.003063 | 1.000000 |
| Random Forest | 0.982744 | 1.647887 | 2.108304 | 0.982750 |
| Gradient Boosting | 0.993224 | 1.040231 | 1.321107 | 0.993137 |
| HistGradient Boosting | 0.996390 | 0.761361 | 0.964293 | 0.996501 |

The results show that the linear models closely reconstruct the supplied target, while tree-based models also achieve high predictive performance.

## 15. Feature Engineering

The following engineered features were tested:

- `phone_to_study_ratio`
- `study_to_phone_ratio`
- `focus_per_study_hour`
- `sleep_study_balance`
- `digital_wellbeing_balance`
- `study_focus_index`

The engineered features did not produce a meaningful improvement over the original six variables because the original variables already encode the target extremely closely.

## 16. Productivity Classification

The productivity score was divided into three groups using tertiles:

- Low
- Medium
- High

Distribution:

- Low: 6,672 records (33.36%)
- Medium: 6,664 records (33.32%)
- High: 6,664 records (33.32%)

### Classification Results

| Model | Accuracy | Precision | Recall | F1 |
|---|---:|---:|---:|---:|
| Logistic Regression | 0.9975 | 0.9975 | 0.9975 | 0.9975 |
| Random Forest | 0.9250 | 0.9259 | 0.9250 | 0.9253 |
| Gradient Boosting | 0.9200 | 0.9226 | 0.9200 | 0.9207 |
| HistGradient Boosting | 0.9517 | 0.9525 | 0.9517 | 0.9520 |

These classification results should also be interpreted cautiously because the class labels are derived directly from the same productivity score that is almost perfectly reconstructible from the input variables.

## 17. Explainable AI

Logistic Regression was used to examine individual student predictions.

For an example student, the model calculated:

- Actual productivity group
- Predicted productivity group
- Class probabilities
- Standardized feature values
- Feature-level contributions

The contribution calculation was based on the standardized feature value multiplied by the logistic-regression coefficient.

These contributions describe **model behavior** and should not be interpreted as causal effects.

---

## 18. Key Integrated Findings

The combined section 1 and section 2 analysis shows that:

- Study hours have a strong positive association with the supplied productivity score.
- Focus and sleep also show positive associations.
- Phone usage and stress show negative associations.
- Attendance has a positive association.
- The supplied productivity score is extremely easy to reconstruct from six variables.
- Multiple regression models produce unusually high performance on this dataset.
- Engineered features add almost no predictive information.
- Productivity classification achieves high accuracy because the class labels are derived from the same highly structured target.
- Productivity score has a very weak linear relationship with final grade in the supplied data.

---

## 19. Limitations

- Correlation and regression analysis do not establish causation.
- The supplied productivity score appears highly structured.
- The unusually high model performance may reflect how the target variable was constructed.
- Classification labels are derived from the productivity score and therefore are not independent real-world outcomes.
- The findings should not be generalized to all students without validation on an independently collected dataset.
- Final grade has a very weak linear relationship with productivity score in this dataset.
- The analysis describes patterns in the supplied dataset and does not establish real-world causal relationships.

---

## 20. Conclusion

This project demonstrates an end-to-end data analytics and machine-learning workflow for studying digital habits, lifestyle, wellbeing, academic behavior, and student productivity.

Version 1 establishes the exploratory and statistical analysis, while Version 2 extends the work through target forensics, formula-pattern investigation, machine-learning benchmarking, feature engineering, classification, and explainable AI.

The most important analytical finding is that the supplied productivity score is highly structured and can be reconstructed extremely closely from six variables. This explains the unusually high predictive performance observed across several models and is an important consideration when interpreting the results.

---

## 21. How to Run the Project

### Step 1: Install Python

Install Python 3.x on your system.

### Step 2: Open the Project Folder

Place the following files in the same folder:

-  HindujaAkkera_DigitalWellbeingAnalytics.ipynb
-  student_productivity_distraction.csv
-  README.md
-  requirements.txt

### Step 3: Install Required Libraries

Open a terminal in the project folder and run:

```bash
pip install -r requirements.txt
```

If using a virtual environment, activate it before installing the requirements.

### Step 4: Run the Notebook

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open:

`HindujaAkkera_DigitalWellbeingAnalytics.ipynb`

Run the notebook cells from top to bottom.

### Step 5: Run the Python Source File

The combined source file can also be executed using:

```bash
python HindujaAkkera_DigitalWellbeingAnalytics.ipynb
```

Make sure the dataset is located in the same project folder.

---

## 22. Project Files

-  HindujaAkkera_DigitalWellbeingAnalytics.ipynb
-  README.md
-  requirements.txt 
-  student_productivity_distraction.csv 
-  HindujaAkkera_ProjectReport.docx

---

## 23. Dataset Reference

**Student Productivity & Digital Distraction Dataset — Kaggle**

https://www.kaggle.com/datasets/sehaj1104/student-productivity-and-digital-distraction-dataset
