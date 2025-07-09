# Customer Churn Analysis Project

This project analyzes customer churn behavior using a telecom dataset to uncover patterns, predict churn probability, and identify actionable insights. It demonstrates end-to-end analytics capabilities including exploratory analysis, feature engineering, predictive modeling, and customer segmentation using Python and Tableau. The goal is to help businesses proactively reduce churn and retain valuable customers by identifying at-risk segments and understanding churn drivers. The dataset is taken from Kaggle: https://www.kaggle.com/datasets/blastchar/telco-customer-churn?resource=download

---

### Problem Statement
Customer churn is a major challenge in subscription-based businesses, especially in telecom. The cost of acquiring a new customer often exceeds that of retaining an existing one. This project aims to:

* Identify which customers are most likely to churn.
* Understand the key factors contributing to churn.
* Provide actionable insights to reduce churn and improve customer retention.

---

### Dataset Description
The dataset comes from a fictional telecom company and includes information about 7,043 customers. It contains:

* Demographics: Gender, Senior Citizen, Partner, Dependents
* Account information: Tenure, Contract Type, Payment Method, Monthly and Total Charges
* Services signed up: Internet Service, Online Security, Streaming TV, etc.
* Target Variable: Churn (Yes/No)

---

### Project Structure

- `data` – Cleaned CSV used for modeling and Tableau (churn_predictions_with_segments.csv)
- `python` – Churn modeling and clustering using sklearn (churn.ipynb) 
- `tableau` – Visual dashboards (churn breakdown, clusters) (Customer Churn Dashboard.twb)
- `README.md` – Project documentation

---

### Project Objectives
The main objectives of this Customer Churn Analysis project are to:

* Predict Customer Churn: Use machine learning models to identify which customers are likely to leave the telecom service.
* Understand Key Drivers: Analyze patterns in customer behavior (e.g., contract type, tenure, payment method) to uncover factors contributing to churn.
* Segment Customers: Apply K-Means clustering to group customers based on similarities in tenure, charges, and behavior.
* Visualize Insights: Build an interactive Tableau dashboard to communicate churn risk and customer segment profiles effectively.
* Provide Actionable Recommendations: Suggest targeted strategies to reduce churn and improve customer retention.

---

### Python: Churn Prediction & Segmentation

To better understand churn behavior and build predictive insights, started by cleaning and preparing the dataset and then used both classification and clustering techniques to explore the data more deeply.

#### Data Cleaning & Preprocessing
Began by dropping customerID, as it had no analytical value. The TotalCharges column had some parsing issues, so fixed the data type and handled any resulting nulls. Then  converted several columns like Churn, Partner, Dependents, PaperlessBilling, and gender into binary format (e.g., Yes → 1, No → 0, Male → 1, Female → 0).

For other categorical columns such as InternetService, Contract, PaymentMethod, etc., used one-hot encoding so that the model could interpret them. By the end of this step, had a clean, model-ready DataFrame.

#### Exploratory Insights

Before modeling, took a closer look at the data:

* Churn Rate: About 26.5% of customers had churned.
* Tenure: Customers with shorter tenure were far more likely to churn.
* Monthly Charges: Churned customers generally had higher monthly bills.
* Contract Type: Month-to-month users showed the highest churn.
* Payment Method: Electronic checks had the highest churn rate.

These insights gave a better sense of which features might matter most in modeling.

#### Predictive Modeling

Split the data into training and test sets using an 80/20 split. Then, trained three models:

* Logistic Regression – Performed best with an AUC of 0.832
* Decision Tree – AUC of 0.670
* Random Forest – AUC of 0.818

Selected Logistic Regression as the final model because of its strong performance and ease of interpretation. Also generated churn probabilities to use later in Tableau.

#### Customer Segmentation (K-Means Clustering)

To add more depth to the analysis, I used clustering to identify patterns in customer behavior. Scaled tenure, MonthlyCharges, and TotalCharges to bring them to the same range. Using the Elbow Method, found that k=4 was the best choice for the number of clusters. Each customer was assigned to one of four clusters using K-Means, based on their tenure, monthly charges, and total charges. These segments revealed meaningful behavioral patterns:

* **Cluster 0: Low Risk (High Tenure, Low Monthly Charges)**  
  Long-term customers who pay less per month. These users are likely stable and satisfied hence minimal churn risk.

* **Cluster 1: Churn Risk (Low Tenure, High Monthly Charges)**  
  Newer customers paying a premium. This group had the **highest churn rate** possibly due to dissatisfaction or price sensitivity.

* **Cluster 2: Medium Risk (Medium Tenure, Medium Charges)**  
  These are average users with moderate tenure and spend. These customers are steady but might require engagement to prevent churn. These are average users with moderate tenure and spend

* **Cluster 3: High Usage (High Tenure, High Total Charges)**  
  Long-term, high-value customers. Though their monthly bills are high, their overall loyalty makes them less likely to churn.  

These clusters were later visualized in Tableau to help tailor retention strategies for each segment. 

---

### Tableau Dashboard & Insights 


#### Churn by Contract Type
- **Description**: A stacked bar chart showing churn probability by contract length (month-to-month, one year, two year).
- **Insight**: Customers on **month-to-month contracts** have significantly higher churn. Retention campaigns should focus on converting them to longer-term contracts.


#### Churn Vs Payment Method
- **Description**: Compares churn rates across different payment methods.
- **Insight**: **Electronic check users** have the highest churn. Automatic payments (e.g., credit card) are associated with **lower churn** — encouraging these could improve retention.

#### Churn Vs Tenure  by Segment
- **Description**: Bar chart showing average churn probability across tenure groups and segments.
- **Insight**: Customers with **shorter tenure** are much more likely to churn. First 6–12 months are critical for engagement and onboarding.

  
#### Customer Segment Size vs Churn Risk (Treemap)
- **Description**: Visualizes customer segment size and churn rate simultaneously.
- **Insight**: Some smaller segments (like “Churn Risk”) contribute disproportionately to churn. Focused retention offers could reduce overall churn impact.


#### Churn Probability Heatmap (Tenure × Monthly Charges)
- **Description**: Heatmap showing churn likelihood based on tenure and charges.
- **Insight**: **Low-tenure, high-charge** customers show the highest churn — prioritize retention here.

#### Churn Vs Monthly Charges by Segment
- **Description**: Shows churn probability across monthly charge bins, broken down by segment.
- **Insight**: Customers with **higher monthly charges are more likely to churn**. Bundled service discounts or loyalty incentives may help reduce churn in this segment.














