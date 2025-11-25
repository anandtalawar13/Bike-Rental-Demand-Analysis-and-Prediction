# Bike Rental Demand Prediction – Report
---
## 1. Project Overview
The goal of this project is to **predict daily bike rental demand** using historical data from a bike-sharing system (2011–2012).  

Accurate demand prediction helps to:
- Optimize **bike availability**
- Improve **customer satisfaction**
- Reduce **operational costs**
- Support **data-driven decisions** for planning and marketing
---

## 2. Dataset Description
Two datasets were used:
* **day.csv** — daily rental data (731 observations)
    * Period: 2011–2012
    * Instances: ~731 rows (daily records)
    * Features: 13 input variables + rental counts
* **hour.csv** — hourly rental data
    * Period: 2011–2012
    * Instances: ~17,389 rows (hourly records)
    * Features: 13 input variables + rental counts
* No missing values.
* Contains weather features:
  * `temp`, `atemp`, `hum`, `windspeed` (normalized)
* Contains date features:
  * `dteday`, `season`, `mnth`, `weekday`, `workingday`, `holiday`
* Target variables:
  * `casual`
  * `registered`
  * **`cnt` (total rentals)** → used as prediction target.
---

## 3. Exploratory Data Analysis (EDA)

### 3.1 Structure & Uniqueness
- `instant` and `dteday` → **731 unique values** → confirms no duplicate days
- Data is **complete and clean** with **no missing values**
- Seasons (`season`) and months (`mnth`) cover all parts of the year
---
### 3.2 Patterns & Relationships
- Rentals generally **increase in warmer months** (summer & fall).
- 2012 shows **higher demand** than 2011 → growth in bike usage.
- **Working days vs holidays/weekends** show different rental patterns.
- `temp` / `atemp` → **positively correlated** with `cnt`  
- `hum` and `windspeed` → **slightly negative impact** on rentals  
- `yr` → strong positive correlation with `cnt` (higher demand in 2012)

## 4. Data Preprocessing
To prepare the data for modeling, we performed:

- **Feature transformation**
  - Extracted date-related features where needed
  - Ensured correct data types
- **Handling of categorical features**
  - Encoded features such as `season`, `weathersit`, etc.
- **Train-test split**
  - Data was split into **training and testing sets** to evaluate generalization
- **Scaling**
  - Some models required feature scaling; tree-based models did not
---

## 5. Models Built
We experimented with a wide range of models:

### 5.1 Linear & Regularized Models
- **Linear Regression**
- **Ridge Regression**
- **Lasso Regression**
- **ElasticNet Regression**

These models provide a good **baseline** and help understand **linear relationships** between features and rentals.

---

### 5.2 Tree-Based & Ensemble Models
- **Random Forest Regressor**
- **XGBoost Regressor**
- **LightGBM Regressor**
- **CatBoost Regressor**
- **Stacking Regressor** (combining multiple models)

For some models, **hyperparameter tuning** (e.g., GridSearch/RandomizedSearch) was applied to improve performance, especially for:

- Random Forest  
- XGBoost  
- LightGBM  
- CatBoost  
---

## 6. Evaluation Metrics
We evaluated all models using:

- **R² (Coefficient of Determination)** – how much variance is explained  
- **RMSE (Root Mean Squared Error)** – penalizes large errors  
- **MAE (Mean Absolute Error)** – average absolute prediction error  

### Model Performance Comparison
| Model                 | RMSE    | MAE     | R²      |
|-----------------------|---------|---------|---------|
| **CatBoost (Tuned)**  | **552.77** | **353.75** | **0.9238** |
| LightGBM (Tuned)      | 573.29  | 393.09  | 0.9180  |
| CatBoost              | 581.49  | 367.64  | 0.9157  |
| XGBoost (Tuned)       | 587.75  | 398.00  | 0.9138  |
| Stacking Regressor    | 617.89  | 434.27  | 0.9048  |
| XGBoost               | 620.69  | 417.80  | 0.9039  |
| LightGBM              | 653.59  | 444.41  | 0.8935  |
| ElasticNet            | 672.41  | 479.95  | 0.8872  |
| Lasso Regression      | 673.89  | 479.65  | 0.8867  |
| Ridge Regression      | 677.16  | 483.09  | 0.8856  |
| Linear Regression     | 679.75  | 485.48  | 0.8848  |
| Random Forest (Tuned) | 687.59  | 468.17  | 0.8821  |
| Random Forest         | 688.40  | 468.75  | 0.8818  |

---

## 7. Best Performing Model

From the experimental results:

>  **CatBoost Regressor (with hyperparameter tuning)** emerged as the **best-performing model**.

### Why CatBoost Performed the Best
- Handles **categorical features** efficiently  
- Requires **minimal preprocessing**  
- Captures **non-linear patterns** in the data  
- Achieved **higher R²** and **lower RMSE/MAE** than other models on the test set  
---

## 8. Model Explainability with SHAP (CatBoost)

To make the model more interpretable, we used **SHAP (SHapley Additive exPlanations)** on the **CatBoost model**.

- Provides **feature-level explanations** for each prediction  
- Shows how each feature **increases or decreases** the predicted rental count  
- Helps to **validate** that the model is learning meaningful relationships  
- Improves **trust** and transparency in the model

### 8.1 SHAP Key Insights
From SHAP plots (summary, dependence etc.):

- **Temperature (`temp`)**  - Higher temperatures → **higher rentals** (up to a comfort point)
- **Year (`yr`)**  - 2012 generally has higher SHAP values than 2011 → **growth trend**
- **Weather situation (`weathersit`)**  
  - Clear weather → **positive impact**
  - Rainy/misty conditions → **negative impact**
- **Humidity (`hum`)**  - Very high humidity → **reduces rentals**
- **Windspeed**  - Higher windspeed → slightly fewer rentals

> Ideal rental conditions are **clear, warm, moderately dry days**, especially in **later years** where adoption increased.

---

## 9. Saving & Loading Models
To make the solution reusable and deployable, all important models were:

- **Saved** using `joblib.dump(...)`
- **Loaded back** using `joblib.load(...)`

This allows:
- Reusing trained models without retraining  
- Integrating them into an **API**, **web app**, or **dashboard**

---

## 11. Conclusion
- Built a complete **end-to-end ML pipeline**:
  - Data understanding → Preprocessing → Modeling → Tuning → Evaluation → Explainability
- Compared **multiple models**:
  - Linear, regularized, tree-based, boosting, and stacking
- **CatBoost** delivered the **best performance** and balanced:
  - Accuracy  
  - Robustness  
  - Interpretability (with SHAP)

>  The project demonstrates how machine learning can effectively model and predict **bike rental demand** using weather, seasonality, and calendar features.
---