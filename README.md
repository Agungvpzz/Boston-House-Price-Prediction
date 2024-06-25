# Boston-House-Price-Prediction
Boston House Price Prediction


> [!NOTE]
> If you encounter an error with the Jupyter Notebook on GitHub, please use the following links below:<br>
> [1. EDA](https://nbviewer.org/github/Agungvpzz/Boston-House-Price-Prediction/blob/main/Boston%20House%20EDA.ipynb) <br>
> [2. Predictive Modeling](https://nbviewer.org/github/Agungvpzz/Boston-House-Price-Prediction/blob/main/Boston%20House%20Predictive%20Modeling.ipynb) <br>

## Introduction

## Data Understanding
[Download dataset](https://www.kaggle.com/datasets/vikrishnan/boston-house-prices) <br>
Each record in the database describes a Boston suburb or town. The data was drawn from the Boston Standard Metropolitan Statistical Area (SMSA) in 1970. The attributes are deﬁned as follows (taken from the UCI Machine Learning Repository1)
- CRIM: per capita crime rate by town
- ZN: proportion of residential land zoned for lots over 25,000 sq.ft.
- INDUS: proportion of non-retail business acres per town
- CHAS: Charles River dummy variable (= 1 if tract bounds river; 0 otherwise)
- NOX: nitric oxides concentration (parts per 10 million)
- RM: average number of rooms per dwelling
- AGE: proportion of owner-occupied units built prior to 1940
- DIS: weighted distances to ﬁve Boston employment centers
- RAD: index of accessibility to radial highways
- TAX: full-value property-tax rate per \$10,000
- PTRATIO: pupil-teacher ratio by town 
- B: 1000(Bk−0.63)^2 where Bk is the proportion of blacks by town
    - Shows non-linear formula, when the higher difference from (Bk−0.63) results higher B value.
    - In intuitive way, not all blacks are from the lower class, so the larger black population also indicates a more comfortable place for black people from the upper class (imply higher MEDV) when racial issues matter in society.
- LSTAT: \%lower status of the population
- MEDV: Median value of owner-occupied homes in $1000s

## Business Goals
- Better understanding of how social, demographic, and geographic contexts affect people's house-buying behavior.

## Methodology
- Feature Classification:
    - Categorical Features: Features with fewer than 10 unique values.
    - Numerical Features: Features with 10 or more unique values.
- Numerical Features Skewness Check:
    - We examine the skewness of numerical features to identify distribution asymmetry.
- Numerical Transformation Techniques:
    - Various distribution transformation techniques are applied to minimize the mean skewness values of numerical features.
    - The Yeo-Johnson power transformation technique produced the lowest mean skewness, making it our chosen method for predictive modeling.
    - The target feature is also transformed using this technique to enhance model accuracy.
- Outlier Imputation:
    - Outliers are imputed using the Winsorizing technique to prepare data for predictive modeling.
- Model Scoring:
    - R² score is the primary metric for evaluating model performance.
- Base Model Building:
    - We use base models without parameter tuning, including:
        - LinearRegression
        - SVR (Support Vector Regression)
        - XGBoost
    - KFold Cross-Validation with 5 folds is used to validate the model's scores.
- Model Selection with PyCaret:
    - PyCaret is utilized to identify the best model based on performance metrics.
- Final Model Selection:
    - The CatBoost model is selected due to its superior performance on cross-validation, test data, and unseen data.
Model Evaluation:
- The PyCaret model evaluation method is employed for quick and effective model assessment.

## Results and Analysis

### Features Characteristics
- There are two categorical features, 'CHAS' and 'RAD', each with fewer than 10 unique values.
- For numerical features, there are:
    - 5 features have high skewed values (skew > 1):
        - CRIM
        - ZN
        - DIS
        - B
        - MEDV (target value)
    - 5 features have moderately skewed values (skew 0.5-1.0):
        - NOX
        - AGE
        - TAX
        - PTRATIO
        - LSTAT
    - 2 features have near-zero skewed values:
        - INDUS
        - RM

### Features Correlation to Target MEDV
![image](https://github.com/Agungvpzz/Boston-House-Price-Prediction/assets/48642326/699d36c3-9942-4c4b-b750-ed06812bb2d8)
- Features with negative correlations indicate factors that tend to decrease housing prices (e.g., high crime rate, pollution, lower status population).
- Features with positive correlations suggest factors that contribute to higher housing prices (e.g., larger lots, more rooms, proximity to the Charles River).

### Predictive Modeling

#### PyCaret Models Comparisons
![image](https://github.com/Agungvpzz/Boston-House-Price-Prediction/assets/48642326/652df81c-5829-4620-809f-a55d1cf9b0d9)

Catboost Model Test and Validation
- cross-val mean r2: 0.8441
- data-test r2: 0.8492
- data-unseen r2: 0.8288
- cross-val mean mean absolute error: 1.9880
- data-test mean absolute error: 2.1285
- data-unseen mean absolute error: 1.9143

![image](https://github.com/Agungvpzz/Boston-House-Price-Prediction/assets/48642326/1259ac9f-7513-42dc-969b-c54ef9eba2ad)

![image](https://github.com/Agungvpzz/Boston-House-Price-Prediction/assets/48642326/40a5eb98-07e5-4bae-891e-71f1f4da5ace)


## Conclusion
