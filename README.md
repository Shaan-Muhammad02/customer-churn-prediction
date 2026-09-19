# Customer Churn Prediction

## Project Overview

Customer churn was analyzed in the telecommunications industry using the **IBM Telco Customer Churn dataset**.

The objective of the project was to develop a machine learning approach capable of identifying customers who are at higher risk of leaving. By recognizing these customers earlier, retention strategies can be applied more proactively.

The project included exploratory data analysis, data preprocessing, statistical feature selection, class-imbalance handling with SMOTE, machine learning model development, hyperparameter tuning, and model evaluation.

Several classification models were compared, with the final model selected based on its ability to identify actual churners rather than accuracy alone.

## Business Problem

Customer churn can create significant revenue loss for telecommunications companies.

The goal was to identify customers who are more likely to leave before churn occurs so that retention efforts can be focused on higher-risk customers.

Particular emphasis was placed on **recall**, since failing to identify an actual churner may result in a missed retention opportunity.

The analysis was designed to support:

- Early identification of high-risk customers
- More targeted retention strategies
- Improved customer support interventions
- Better understanding of churn drivers
- Data-driven decision-making

## Dataset

The project uses the **IBM Telco Customer Churn dataset**.

The dataset contains:

- **7,043 customer records**
- **21 initial variables**
- Customer demographic information
- Account information
- Contract information
- Payment methods
- Service subscriptions
- Monthly and total charges
- Customer tenure

**Target Variable:** `Churn`

The target is binary:

- `Yes` - Customer churned
- `No` - Customer remained

The original dataset was imbalanced, with approximately:

- **73.42% No Churn**
- **26.58% Churn**

<img width="862" height="735" alt="churn_distribution" src="https://github.com/user-attachments/assets/a14fb081-fc81-4a6d-819c-5ec152679d0c" />


## Exploratory Data Analysis

Exploratory data analysis was performed to identify patterns associated with customer churn.

Several important relationships were observed.

### Contract Type

Customers with **month-to-month contracts** showed substantially higher churn compared with customers on one-year or two-year contracts.

Longer contracts were associated with greater customer stability.

### Internet Service

Customers using **Fiber Optic internet** showed higher churn compared with DSL customers.

### Support Services

Customers without services such as:

- Tech Support
- Online Security
- Device Protection

were more likely to churn.

### Customer Tenure

Churn risk was particularly high among customers in the early stages of their relationship with the company.

A noticeable drop-off was observed during approximately the first **1-5 months** of customer tenure.

### Payment Method

Customers using **Electronic Check** showed a stronger association with churn.

<!-- Add tenure / churn drivers screenshot here later -->

## Methodology

### 1. Data Cleaning and Preparation

The dataset was cleaned and prepared before model development.

The following steps were completed:

- Missing values in `TotalCharges` were identified
- 11 records with missing `TotalCharges` values were removed
- `TotalCharges` was converted to a numerical format
- Outliers were addressed using the IQR method
- Categorical variables were encoded
- Numerical and categorical features were prepared for machine learning

### 2. Train-Test Split

The dataset was divided into:

- **80% Training Data**
- **20% Testing Data**

The split was completed before applying oversampling techniques in order to reduce the risk of data leakage.

### 3. Feature Selection

**Chi-Square testing** was used to evaluate relationships between categorical variables and customer churn.

Features with p-values greater than `0.05` were considered statistically insignificant and removed from the modeling process.

Two variables were removed:

- `PhoneService`
- `gender`

Other variables such as contract type, online security, tech support, internet service, payment method, and several service-related features showed stronger relationships with churn.

### 4. Class Imbalance Handling

The dataset contained considerably fewer churned customers than non-churned customers.

To address this imbalance, **SMOTE (Synthetic Minority Over-sampling Technique)** was applied.

SMOTE was applied **only to the training dataset** after the train-test split.

This created a more balanced training sample and improved the ability of the models to identify actual churners.

<!-- Add SMOTE workflow screenshot here later -->

## Machine Learning Models

Four classification models were evaluated:

- **Random Forest**
- **XGBoost**
- **LightGBM**
- **Support Vector Classifier (SVC)**

### Random Forest

Random Forest was used as a baseline model because of its ability to handle mixed features and provide a strong benchmark for classification performance.

### XGBoost

XGBoost was evaluated as a gradient-boosting model capable of capturing complex nonlinear relationships in the data.

### LightGBM

LightGBM was also evaluated as a high-performance gradient-boosting model.

### Support Vector Classifier

SVC was evaluated because of its ability to perform well with high-dimensional classification problems.

Hyperparameter tuning was performed using **GridSearchCV** and **Stratified K-Fold Cross-Validation**.

The selected SVC parameters were:

- `C = 10`
- `gamma = 0.01`
- `kernel = rbf`

## Model Results

### Support Vector Classifier - Selected Model

The SVC model was selected as the final model because of its stronger ability to identify actual churners.

Performance included:

- **ROC-AUC:** 82.51%
- **Overall Accuracy:** 73.35%
- **Churn Recall:** 77%

The model successfully identified approximately **77% of customers who actually churned**.

### Random Forest Baseline

Random Forest achieved:

- **ROC-AUC:** 80.59%
- **Overall Accuracy:** 76.69%
- **Churn Recall:** 57%

Although Random Forest achieved slightly higher overall accuracy, its lower churn recall meant that more actual churners were missed.

Because customer retention was the primary business objective, the SVC model was considered more useful.

### Effect of SMOTE

SMOTE increased churn recall from approximately:

**48% → 77%**

This substantially improved the model's ability to detect customers at risk of leaving.

<!-- Add model results screenshot here later -->

## Key Findings

Several important findings were identified:

- Month-to-month customers had substantially higher churn risk
- Fiber Optic customers showed higher churn than DSL customers
- Customers without Tech Support or Online Security were more likely to leave
- Early-tenure customers represented an important churn-risk group
- Electronic Check users showed a stronger association with churn
- The original dataset contained significant class imbalance
- SMOTE substantially improved churn detection
- Recall was more important than overall accuracy for the business objective
- SVC provided the strongest balance for identifying actual churners

## Business Recommendations

Based on the analysis, several retention strategies can be considered:

1. **Focus on month-to-month customers**

   Customers with flexible month-to-month contracts showed higher churn risk and may benefit from targeted retention offers.

2. **Support customers during their first months**

   Customers in approximately their first 1-5 months showed elevated churn risk, making early engagement particularly important.

3. **Encourage longer-term contracts**

   Incentives could be used to encourage customers to move from month-to-month plans toward longer-term contracts.

4. **Promote support services**

   Customers without Tech Support or Online Security were more likely to churn, suggesting that these services may contribute to customer retention.

5. **Prioritize high-risk customers identified by the model**

   Churn predictions can help direct retention efforts toward customers who are more likely to leave.

6. **Investigate Fiber Optic customer experience**

   Since Fiber Optic customers showed higher churn, service quality, pricing, and customer support for this segment should be investigated further.

## Future Improvements

Several improvements could strengthen future versions of the project:

- Combine multiple models using ensemble stacking
- Incorporate customer service logs
- Include customer complaints and support tickets
- Introduce additional customer satisfaction variables
- Periodically retrain the model using updated customer data
- Monitor possible label contamination when previously high-risk customers are successfully retained

Additional behavioral and customer-service information may improve the model's ability to distinguish between churners and non-churners.

## Repository Structure

```text
customer-churn-prediction/
│
├── notebooks/
│   └── customer_churn_prediction.ipynb
│
├── presentations/
│   ├── Customer_Churn_Poster.pptx
│   └── customer_churn_presentation.pptx
│
├── .gitignore
├── README.md
└── requirements.txt
```

## Tools and Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- XGBoost
- LightGBM
- Support Vector Classifier
- Random Forest
- SMOTE
- GridSearchCV
- Stratified K-Fold Cross-Validation
- Chi-Square Feature Selection
- Exploratory Data Analysis
- Machine Learning
- Classification
- Jupyter Notebook
