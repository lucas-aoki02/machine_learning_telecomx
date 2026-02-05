# 📊 Churn Prediction Project – TelecomX

## 🎯 Project Purpose and Objective

The main purpose of this project is to **predict customer churn** in a telecom company using Machine Learning techniques.  
Customer churn refers to customers who cancel their services, and predicting this behavior allows the company to take **proactive retention actions**.

**Primary objective:**
- Predict customer churn based on demographic, contractual, and financial variables.
- Compare different Machine Learning models and evaluate their performance.
- Extract business insights to support retention strategies.

---

## 📁 Project Structure
- base_telecomx.csv # Raw dataset provided for the analysis
- ml_telecomx.ipynb # Main notebook with EDA, preprocessing, modeling, and evaluation
- readme.md # Project documentation


All stages of the analysis — data preparation, exploratory analysis, modeling, and evaluation — are performed inside the main notebook (`ml_telecomx.ipynb`).

---

## 🧹 Data Preparation and Preprocessing

### Variable Classification

The dataset contains both **categorical** and **numerical** variables:

- **Categorical variables:**
  - Gender
  - SeniorCitizen
  - Contract type
  - Payment method
  - Internet and phone service options
  - Churn (target variable)

- **Numerical variables:**
  - Customer tenure
  - Daily bill
  - Total charges

This classification guided the choice of encoding and normalization techniques applied during preprocessing.

---

### Encoding and Normalization

- **Categorical Encoding:**
  - Categorical features were converted into numerical representations using encoding techniques suitable for Machine Learning algorithms.

- **Normalization and Scaling:**
  - Logarithmic transformation (`np.log1p`) was applied to skewed monetary variables.
  - `StandardScaler` was used for variables with large variance.
  - `MinMaxScaler` was applied to the tenure variable.

**Justification:**
- Distance-based models such as **K-Nearest Neighbors (KNN)** are highly sensitive to feature scale.
- Normalization prevents variables with large magnitudes from dominating distance calculations.
- Although **Random Forest** does not require normalization, a standardized pipeline ensures consistency across models.

---

### Train-Test Split

- The dataset was split into **training** and **test** sets.
- The training set was used for model fitting and hyperparameter tuning.
- The test set was reserved exclusively for final evaluation to avoid data leakage.

---

## 🤖 Modeling Choices and Justifications

### Selected Models

- **K-Nearest Neighbors (KNN):**
  - Chosen for its simplicity and interpretability.
  - Useful for understanding customer similarity and churn proximity.

- **Random Forest Classifier:**
  - Selected for its robustness and ability to model non-linear relationships.
  - Capable of capturing complex interactions between variables.
  - Provides feature importance insights for business interpretation.

### Rationale for Model Selection

- KNN offers transparent, distance-based predictions.
- Random Forest generally performs well on structured business data.
- Comparing both models balances interpretability and predictive performance.

---

### Churn Distribution and Behavioral Analysis

An initial exploratory analysis was conducted to understand the distribution of churn and how key numerical variables behave across churn and non-churn customers.

#### Churn vs No Churn

The class distribution shows a clear imbalance between churned and non-churned customers.  
Most customers did not churn, while a smaller but significant portion canceled the service.

This imbalance reinforces the importance of evaluating metrics such as **recall** and **F1-score**, rather than relying solely on accuracy during model evaluation.

---

#### Tenure by Churn Status

The boxplot comparing **customer tenure by churn status** reveals a strong relationship between tenure and churn:

- Customers who **did not churn** tend to have significantly higher tenure.
- Churned customers are concentrated in the early months of the contract.
- The median tenure of churned customers is much lower, indicating that churn is more frequent among newer customers.

This pattern suggests that the **early lifecycle stage** is the most critical period for customer retention efforts.

---

#### Total Charges by Churn Status

The distribution of **total charges** also shows clear differences between churned and non-churned customers:

- Non-churned customers generally have higher total charges, which is expected due to longer tenure.
- Churned customers present lower total charges but with noticeable variability.
- Several outliers among churned customers indicate that even high-value customers may churn under certain conditions.

This insight highlights that churn is not exclusively driven by low revenue customers and reinforces the need for targeted retention strategies beyond simple revenue thresholds.

---

#### Key EDA Takeaways

- Churn is strongly associated with **short tenure**.
- Customers with longer relationships are significantly more likely to stay.
- Revenue-related variables must be analyzed jointly with tenure to avoid misleading conclusions.
- These findings guided feature selection and influenced the modeling strategy adopted in this project.


---

## 📈 Model Performance Evaluation

### Classification Metrics

| Metric | KNN (k=57) | Random Forest |
|------|------------|---------------|
| Accuracy | 0.7762 | 0.7624 |
| Precision | 0.6125 | 0.5465 |
| Recall | 0.4412 | 0.4679 |
| F1-Score | 0.5125 | 0.5043 |

---

## 🧮 Confusion Matrix – Random Forest

The confusion matrix below summarizes the Random Forest model predictions on the test dataset:

- **True Negatives (TN – Correct Retention):** 934  
- **False Positives (FP – False Alarm):** 144  
- **False Negatives (FN – Missed Churn):** 198  
- **True Positives (TP – Correct Churn Detection):** 176  

### Interpretation

- The model performs well in identifying customers who will **not churn**.
- The main limitation lies in **false negatives**, representing churners that were not detected.
- From a business perspective, reducing false negatives is critical, as they represent lost opportunities for proactive retention actions.
- Despite slightly lower accuracy than KNN, the higher recall makes Random Forest more suitable for churn-oriented decision-making.

---

## 🚀 How to Run the Project

### Requirements

Install the required Python libraries:

```bash
pip install pandas numpy scikit-learn plotly

### Execution Steps

1. Clone or download the repository.
2. Open the `ml_telecomx.ipynb` notebook.
3. Make sure the file `base_telecomx.csv` is located in the same directory as the notebook.
4. Run all cells sequentially to reproduce the data analysis, modeling, and evaluation results.