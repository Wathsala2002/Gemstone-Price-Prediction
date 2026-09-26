<img width="845" height="349" alt="image" src="https://github.com/user-attachments/assets/f0913d87-a038-49e5-ad6b-fa7c0fb1bfa1" /># 💎 Gemstone Price Prediction

## Machine Learning - Group 09  - Kasun Vishvajith, Isuru Dulakshana, Gayani Wathsala ##

## 📌 About

This project focuses on predicting gemstone prices by combining real diamond and synthetic cubic zirconia datasets. The project covers data preprocessing, feature engineering, exploratory data analysis, FAMD, clustering, machine learning, hyperparameter tuning and Explainable AI. Clustering methods were used to investigate whether natural groups existed in the data, while several regression and ensemble models were developed and compared for price prediction. CatBoost with Bayesian optimization achieved the strongest test performance, while feature importance and SHAP analysis identified stone type, carat, and physical dimensions as the main influential factors.

## Dataset

💎 Data Sources :	Diamond Sales Dataset + Gemstone Price Prediction Dataset from Kaggle
📦 Final Observations	80,072 (combination of two datasets)
🔢 Variables	12
🎯 Target Variable	LogPrice

 ## 1. Data Preprocessing
🔎 Checked and removed duplicate observations
❌ Removed unrealistic zero values
🩹 Handled missing Depth values using Random Forest
💱 Converted cubic zirconia prices to USD
📈 Created the LogPrice=ln(Price) target variable
✂️ Split the dataset into 80% training and 20% testing data

## 2. Feature Engineering
A new Type variable was created to distinguish between,
Diamond
Zirconia

 ## Engineered Variables
Type	       - Identifies Diamond or Zirconia
LogPrice	   - Log-transformed gemstone price
Carat	       - Weight of the gemstone
X	           - Length 
Y	           - Width
Z	           - Height
Cut	         - Cut quality
Color	       - Color grade
Clarity	     - Clarity grade
Depth	       - Depth measurement
Table	       - Table measurement

## 3. Cluster Analysis
Cluster analysis confirmed no clear natural cluster structure was identified in the dataset.

## 4. Exploratory Data Analysis
Key EDA findings,
* Carat directly increase diamond price
* Type is a dominant driver of price
* Dimensions (X,Y,Z) increases diamonds price
* High clarity stones decreases diamond price which is unrealistic for rael world and we can say this can be happen due to the high clarity stones get smaller carat weight.

## Model Comaparison
### 📊 Fitted Models

| **Model** | **Train R²** | **Test R²** | **Train MSE** | **Test MSE** | **Train MAPE (%)** | **Test MAPE (%)** |
|---|---:|---:|---:|---:|---:|---:|
| 🏆 **CatBoost** | 0.999104 | **0.998882** | 0.004994 | **0.006182** | 0.998067 | **1.102665** |
| **XGBoost** | 0.999049 | **0.998835** | 0.005300 | **0.006444** | 1.030571 | **1.144645** |
| **RandomForest** | 0.999783 | 0.998515 | 0.001208 | 0.008212 | **0.488573** | 1.296243 |
| **HistGradientBoosting** | 0.998422 | 0.998395 | 0.008793 | 0.008875 | 1.396531 | 1.423879 |
| **Ridge** | 0.996588 | 0.996651 | 0.019014 | 0.019014 | 2.109776 | 2.102266 |
| **Linear Regression** | 0.996588 | 0.996651 | 0.019014 | 0.018518 | 2.109750 | 2.102241 |
| **ElasticNet** | 0.996548 | 0.996624 | 0.019234 | 0.018671 | 2.121337 | 2.113961 |
| **Lasso** | 0.996507 | 0.019465 | 0.019465 | 0.018671 | 2.131287 | 2.125186 |

> **Note:** Higher **R²** indicates better explanatory performance, while lower **MSE** and **MAPE** indicate lower prediction error.






