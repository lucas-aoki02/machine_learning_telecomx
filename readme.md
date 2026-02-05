# 📊 Churn Prediction Project - Telecom

This project aims to identify customers with a propensity to cancel services using Machine Learning techniques.

---

## 🧠 Model Selection and Normalization

### Selected Models

- **KNN (K-Nearest Neighbors):**  
  Chosen for being an intuitive similarity-based model. It identifies patterns by comparing the current customer with their "nearest neighbors" in the data space.

- **Random Forest:**  
  Selected for its high robustness and ability to handle non-linear relationships and complex interactions between variables, using an ensemble of decision trees to reduce variance.

### Normalization Necessity

- **Logarithmic Transformation and Scaling:**  
  It was essential to apply `np.log1p` and `StandardScaler` to variables like `daily_bill` and `account.Charges.Total`, in addition to `MinMaxScaler` on `customer.tenure`.

- **Impact on KNN:**  
  Without this step, KNN would be dominated by variables with larger numerical scales (such as total charges), ignoring binary or smaller variables (such as `SeniorCitizen`), since the Euclidean distance calculation is sensitive to scale.

- **Impact on Random Forest:**  
  Although trees do not strictly require normalization to function, maintaining scaled data ensures consistency in the comparison pipeline between models.

---

## 📈 Performance Evaluation

Based on the final test results:

| Metric | KNN (k=57) | Random Forest |
| :--- | :--- | :--- |
| **Accuracy** | 0.7762 | 0.7624 |
| **Precision** | 0.6125 | 0.5465 |
| **Recall** | 0.4412 | 0.4679 |
| **F1-Score** | 0.5125 | 0.5043 |

### Confusion Matrix (Random Forest)

- **True Negatives (Correct Retention):** 934  
- **False Positives (False Alarm):** 144  
- **False Negatives (Undetected Churn):** 198  
- **True Positives (Detected Churn):** 176  

---

## 🔍 Critical Analysis and Comparison

### Which model performed best?

**KNN (k=57)** showed slightly higher accuracy and F1-score (0.776 vs 0.762). However, **Random Forest** achieved a **higher Recall (0.467 vs 0.441)**. For a Telecom business, Random Forest is preferable as it identifies a larger portion of customers who will actually leave, which is more valuable than raw accuracy.

### Overfitting or Underfitting?

- **KNN:**  
  Demonstrated stability after the $k=57$ adjustment (based on the square root of the training set size).

- **Random Forest:**  
  Showed moderate signs of **overfitting**, as training performance is significantly higher than test performance.  
  **Adjustment:** To mitigate this, it is recommended to limit the tree depth (`max_depth`) or increase the minimum samples per leaf (`min_samples_leaf`).

---

## 📊 Analysis of Relevant Variables

### Factors most influencing churn

1. **Contract Type:** Customers with "Month-to-month" contracts have the highest proximity to the Churn profile in KNN and high importance in Random Forest.
2. **Tenure:** The most critical variable for retention. The shorter the contract time, the higher the chance of churn.
3. **Daily Bill:** High daily costs are a strong trigger for customer exit.
4. **Payment Method:** The use of "Electronic Check" is strongly associated with churn behavior.

---

## 💡 Proposed Retention Strategies

Based on the models, I suggest the following actions:

- **Contract Migration:**  
  Create incentives and discounts for "Month-to-month" customers to migrate to annual or two-year plans, reducing volatility.

- **Early Loyalty:**  
  Focus CS (Customer Success) efforts on the first few months of the contract (`low tenure`), where the risk of exit is statistically higher.

- **Price Alert:**  
  Monitor customers with `daily_bill` above average and offer package upgrades with better cost-benefit before the customer reaches a financial dissatisfaction limit.

- **Payment Incentive:**  
  Offer benefits to customers who migrate from "Electronic Check" to automatic debit or credit cards, methods associated with higher retention.
