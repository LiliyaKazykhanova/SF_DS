# SF-DS-Project-4
DS Project 4: Bank Marketing Campaign

*Business Task*
Banks often need to run a marketing campaign in order to sell a product to potential customers.
Our task to define customer characteristics which one is ready to open deposit.

*Technical Task*: Using the data to build a model that predicts whether the client will open a deposit

*Data*: csv-file contains 16 features + 1 target (deposit)

*Task*
* Binary classification

*Metrics*: F1_score

### Content
[Introduction](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Introduction)

[Checking dataset: outliers, duplicates](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Checking-dataset-:-outliers-,-duplicates)

[Feature Engineering](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Feature-Engineering)

[Feature Encoding](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Feature-Encoding)

[Feature Selection](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Feature-Selection)

[Classification ML models: Logistic Regression and Decision Tree](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Classification-ML-models:-Logistic-Regression-and-Decision-Tree)

[Classification ML models: Ensembles](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Classification-ML-models:-Ensembles)

#### Introduction
- dataset shape: 11162 rows, 17 columns
- target value: *deposit*

#### Cheking dataset: outliers, duplicates
- Number of found duplicates: 0
- Columns with missing values:
    * explicit: *balance*
    * implicit: *unknown* value in the next columns - *contact*, *poutcome*, *education*, *job*
- Filling/replacing MV:
    * *balance* - median value
    * *job*, *education* - mode
- Deleting Outliers in *balance* column (by Tukey’s method)

#### Feature Engineering
Our classes are balanced. The ratio of clients without a deposit to those with a deposit is 54 to 46. 
- Age:
    * creating age groups:
        - '<30';
        - '30-40';
        - '40-50';
        - '50-60';
        - '60+'
- Month:
    * getting 1 new feature - season

#### Feature Encoding
- education, age - Ordinal Encoding
- housing, loan, default, deposit - binary encoding - 0('no') / 1('yes')
- job, marital, contact, month, poutcome, season - One-Hot Encoding (get dummies)

#### Feature Selection
- checked correlation between features (spearman method)
- dropped 1 column:
    * pdays
- getting 20 meaningful features by SelectKBest method + adding 3 feautures to final data
    - education level
    - marital status (single, divorced)
- feature normalization by MinMaxScaler

#### Machine Learning Model
- Total feature number: 23
- Models:
    * Logistic Regression, Decision Tree,
    * Ensembles: Random Forest, Gradient Boosting, Stacking
- Metric: F1_score
The best result:
*Model*: Ensembles
*F1_score on test data*: 0.83

- Top-3 meaningful features:
    * duration,
    * contact_unknown
    * poutcome_success

:arrow_up:[to content](https://github.com/LiliyaKazykhanova/SF-DS-Project-4/blob/main/README.md#Content)
