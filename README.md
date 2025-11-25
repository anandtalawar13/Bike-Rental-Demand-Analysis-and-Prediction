# 🚲 Bike Rental Demand Analysis and Prediction

## Project Overview
This project analyzes bike rental demand and builds machine learning models to predict daily rental counts based on environmental and seasonal factors.  
The goal is to uncover key drivers of demand and provide accurate forecasts that can help rental companies optimize operations.

---

##  Dataset
We use the **Bike Sharing Dataset** (hourly and daily data) with the following features:

- **instant**: record index  
- **dteday**: date  
- **season**: season (1: spring, 2: summer, 3: fall, 4: winter)  
- **yr**: year (0: 2011, 1:2012)  
- **mnth**: month (1–12)  
- **hr**: hour (0–23, only in hourly dataset)  
- **holiday**: whether day is holiday  
- **weekday**: day of the week  
- **workingday**: 1 if day is neither weekend nor holiday  
- **weathersit**: weather situation (1: clear, 2: mist, 3: light snow/rain, 4: heavy rain/snow)  
- **temp**: normalized temperature (Celsius ÷ 41)  
- **atemp**: normalized feeling temperature (Celsius ÷ 50)  
- **hum**: normalized humidity (÷ 100)  
- **windspeed**: normalized wind speed (÷ 67)  
- **casual**: count of casual users  
- **registered**: count of registered users  
- **cnt**: total rental bikes (casual + registered)

---

## Methodology
1. **Data Preprocessing**
   - Handling missing values  
   - Feature scaling and normalization  
   - Encoding categorical variables  

2. **Exploratory Data Analysis (EDA)**
   - Seasonal and monthly trends  
   - Correlation analysis  
   - Impact of weather and working days  

3. **Modeling**
   - Linear Regression
   - Lasso Regression
   - Ridge Regression  
   - Random Forest  
   - XGBoost  
   - LightGBM  
   - CatBoost  
   - ElasticNet  
   - Stacking Regressor  

4. **Evaluation Metrics**
   - RMSE (Root Mean Squared Error)  
   - MAE (Mean Absolute Error)  
   - R² Score  

---

##  Results
- **Random Forest, XGBoost, and CatBoost** performed best with high accuracy and low error.  
- Seasonal and weather conditions were strong predictors of demand.  
- Clear recruiter‑friendly visualizations (correlation heatmaps, feature importance plots, prediction vs. actual charts) are included in the notebook.

---

## Tech Stack
- **Python**  
- **Pandas, NumPy** for data processing  
- **Matplotlib, Seaborn, Plotly** for visualization  
- **Scikit-learn, XGBoost, LightGBM, CatBoost** for modeling  
- **Jupyter Notebook** for analysis and presentation  

---

##  How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/Bike-Rental-Demand-Analysis-and-Prediction.git