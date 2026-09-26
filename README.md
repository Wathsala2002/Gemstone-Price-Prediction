# 💎 Gemstone Price Prediction

## Machine Learning - Group 09 
Kasun Vishvajith, Isuru Dulakshana, Gayani Wathsala 

## About

This project focuses on predicting gemstone prices by combining real diamond and synthetic cubic zirconia datasets. The project covers data preprocessing, feature engineering, exploratory data analysis, FAMD, clustering, machine learning, hyperparameter tuning and Explainable AI. Clustering methods were used to investigate whether natural groups existed in the data, while several regression and ensemble models were developed and compared for price prediction. CatBoost with Bayesian optimization achieved the strongest test performance, while feature importance and SHAP analysis identified stone type, carat, and physical dimensions as the main influential factors.

## Dataset
- **Data Sources:** Diamond Sales Dataset + Gemstone Price Prediction Dataset from Kaggle
- **Final Observations:** 80,072 (combination of two datasets)
- **Variables:** 12
- **Target Variable:** `LogPrice`

### Variable Description

| Variable | Data Type | Description |
|---|---|---|
| **LogPrice** | Quantitative | Target variable; natural logarithm transformation of diamond prices. |
| **Price** | Quantitative | Price of the cubic zirconia/real diamond. |
| **X** | Quantitative | Length of the cubic zirconia/real diamond in mm. |
| **Y** | Quantitative | Width of the cubic zirconia/real diamond in mm. |
| **Z** | Quantitative | Height of the cubic zirconia/real diamond in mm. |
| **Table** | Quantitative | Percentage representing how large the top surface of the stone is compared to its total width. |
| **Depth** | Quantitative | Height of the cubic zirconia/real diamond, measured from the culet to the table, divided by its average girdle diameter. |
| **Cut** | Qualitative | Describes the cut quality of the cubic zirconia/real diamond. |
| **Color** | Qualitative | Color of the cubic zirconia/real diamond, with D being the best and J the worst. |
| **Clarity** | Qualitative | Refers to the absence of inclusions and blemishes. The levels range from FL (flawless) to I3 (level 3 inclusions), ordered from best to worst. |
| **Carat** | Quantitative | Carat weight of the cubic zirconia/real diamond. |
| **Type** | Qualitative | Type of the stone: Zirconia or Diamond. |

## Project Structure

Gem_Stone_Price_Prediction/
│
├── 📂 data/
│   ├── Final_Dataset.csv
│   ├── Train Dataset with Log Price.csv
│   ├── Test Dataset with Log Price.csv
│   ├── train_df.csv
│   └── test_df.csv
│
├── 📂 notebooks/
│   ├── 01__Data_Preprocessing.ipynb
│   ├── 02__Clusters.ipynb
│   ├── 03__EDA.ipynb
│   └── 04__Model_Fitting.ipynb
│
├── 📄 Gem_Stone_Price_Prediction.pdf
├── 📄 requirements.txt
└── 📄 README.md

## How to run

### 1. Clone the Repository
**git clone https://github.com/YOUR_USERNAME/Gem_Stone_Price_Prediction.git
cd Gem_Stone_Price_Prediction
**
### 2. Install Dependencies
pip install -r requirements.txt

### 3. Run the Notebooks
The project contains four Jupyter notebooks that should be run in the following order,

1. `01__Data_Preprocessing.ipynb` – Data preprocessing
2. `02__Clusters.ipynb` – Clustering analysis
3. `03__EDA.ipynb` – Exploratory data analysis
4. `04__Model_Fitting.ipynb` – Model training and evaluation

Open the notebooks in Google Colab and run the cells in order. The required datasets are in the data folder on the repository.

## Pipeline
 ### 1. Data Preprocessing
* Checked and removed duplicate observations
* Removed unrealistic zero values
* Handled missing Depth values using Random Forest
* Converted cubic zirconia prices to USD
* Created the LogPrice=ln(Price) target variable
* Split the dataset into 80% training and 20% testing data

### 2. Feature Engineering
A new Type variable was created to distinguish between,
* Diamond
* Zirconia

### 3. Cluster Analysis
Cluster analysis confirmed no clear natural cluster structure was identified in the dataset.

### 4. Exploratory Data Analysis
Key EDA findings,
* Carat directly increase diamond price
* Type is a dominant driver of price
* Dimensions (X,Y,Z) increases diamonds price
* High clarity stones decreases diamond price which is unrealistic for rael world and we can say this can be happen due to the high clarity stones get smaller carat weight.

### 5. Model Comaparison
#### Fitted Models

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

 #### Hyperparameter Tuning
Selected models were further optimized by adjusting their hyperparameters to improve predictive performance.

| Model | Version | Train_R2 | Train_MSE | Train_MAPE(%) | Test_R2 | Test_MSE | Test_MAPE(%) |
|---|---|---:|---:|---:|---:|---:|---:|
| XGBoost | Tuned | 0.999612 | 0.002160 | 0.631571 | 0.999066 | 0.005164 | 0.984758 |
| CatBoost | Tuned | 0.999387 | 0.003414 | 0.814332 | 0.998993 | 0.005567 | 1.033080 |
| CatBoost | Baseline | 0.999104 | 0.004994 | 0.998067 | 0.998882 | 0.006182 | 1.102665 |
| XGBoost | Baseline | 0.999049 | 0.005300 | 1.030571 | 0.998835 | 0.006444 | 1.144645 |
| HistGradientBoosting | Tuned | 0.998823 | 0.006556 | 1.157901 | 0.998648 | 0.007475 | 1.248487 |
| HistGradientBoosting | Baseline | 0.998422 | 0.008793 | 1.396531 | 0.998395 | 0.008875 | 1.423879 |


#### Bayesian Optimization
Bayesian optimization was used to efficiently search for improved hyperparameter combinations.

| Model | Version | Train_R2 | Test_R2 | Train_MSE | Test_MSE | Train_MAPE(%) | Test_MAPE(%) |
|---|---|---:|---:|---:|---:|---:|---:|
| CatBoost | Baseline | 0.999104 | 0.998882 | 0.004994 | 0.006182 | 0.998067 | 1.102665 |
| CatBoost | Tuned | 0.999387 | 0.998993 | 0.003414 | 0.005567 | 0.814332 | 1.033080 |
| CatBoost | Tuned (Bayesian) | 0.999695 | 0.999187 | 0.001697 | 0.004497 | 0.551630 | 0.867376 |
| XGBoost | Baseline | 0.999049 | 0.998835 | 0.005300 | 0.006444 | 1.030571 | 1.144645 |
| XGBoost | Tuned | 0.999612 | 0.999066 | 0.002160 | 0.005164 | 0.631571 | 0.984758 |
| XGBoost | Tuned (Bayesian) | 0.999278 | 0.998913 | 0.004021 | 0.006012 | 0.885593 | 1.101673 |
| HistGradientBoosting | Baseline | 0.998422 | 0.998395 | 0.008793 | 0.008875 | 1.396531 | 1.423879 |
| HistGradientBoosting | Tuned | 0.998823 | 0.998648 | 0.006556 | 0.007475 | 1.157901 | 1.248487 |
| HistGradientBoosting | Tuned (Bayesian) | 0.998784 | 0.998654 | 0.006775 | 0.007445 | 1.180706 | 1.252677 |

#### Reduced vs Full Models 
Feature importance showed that Cut, Depth, and Table had relatively low importance. Therefore a reduced model was tested by removing these variables and finally we got the CatBoost full model as the optimal best model for predicting price of gemstones.

| **Model** | **Test R²** | **Test MSE** | **Test MAPE** |
|---|---:|---:|---:|
| 🏆 **Full CatBoost** | **0.999187** | **0.004497** | **0.8674** |
| **Reduced CatBoost** | 0.998987 | 0.005602 | 0.9923 |
| **Reduced XGBoost** | 0.998764 | 0.006835 | 1.1618 |

## Requirements

See [`requirements.txt`](requirements.txt). Main libraries: `pandas`, `numpy`, `scipy`, `statsmodels`, `matplotlib`, `scikit-learn`, `xgboost`, `catboost`, `optuna`, `shap`, `prince`, `umap-learn`, `kmodes`, `gower`, `scikit-posthocs`, `joblib`, `tqdm`, `jupyter`, `ipykernel`.





