# SF-DS-Project-6
DS Project 6: Customer segmentation based on their purchasing power: Gift Shop

*Business Task*
To group customers with similar purchasing power together.

*Technical Task*: Using the data to build a clusterization model based on customers` purchasing power, order quantity and statute of limitations for last purchase. Define profile of each cluster.

*Data*: The csv file contains 541 909 records and 8 columns

*Type of ML task*: Clusterization -> Classification

*Metrics*: Accuracy score

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/blob/main/PROJECT_6/project/project_6_Clusterization_LK.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#Introduction)

[Checking dataset: outliers, duplicates](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#Checking-dataset-:-outliers-,-duplicates)

[Exploratory Data Analysis (EDA). Feature Engineering](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#Exploratory-Data-Analysis-(EDA).-Feature-Engineering)

[RFM-customers segmentation. Part I](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#RFM-customers-segmentation.-Part-I)

[RFM-customers segmentation. Part II](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#RFM-customers-segmentation.-Part-II)

[RFM-customers segmentation. Part II](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#RFM-customers-segmentation.-Part-II)

[RFM-customers segmentation. Part III. Classification model](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#RFM-customers-segmentation.-Part-III.-Classification-model)

## Introduction
- Dataset's shape: 541_909 rows, 8 columns
    * *InvoiceNo*
    * *StockCode*
    * *Description of product*
    * *Quantity*
    * *InvoiceDate*
    * *UnitPrice*
    * *CustomerID*
    * *Country*

## Cheking dataset: outliers, duplicates
- Columns with missing values: Description and CustomerID (~25% data)
- Number of found duplicates: 5225 (after deleting rows with missing values)

## EDA. Feature Engineering
***Creating new features:***
- Column: QuantityCancelled - quantity of cancelled orders
- Time feautures:
    * purchases_month - month of purchasing
    * purchases_hour - hour of purchasing
    * purchases_day_of_week - day of the week on which the customer make purchases
    * Date

***Deleting missing values and duplicates***

## RFM-customers segmentation. Part I
- Create table with 3 features, grouped by Customer ID
    * Recency
    * Frequency
    * Monetary
- Cleaning data from outliers by quantile 0.95
- Clustering stage
    * Dimensionality Reduction methods: PCA
    * Clusterization method: k-means with n_clusters=3
    * Create profile for 3 customers' segments (Radar Chart)

## RFM-customers segmentation. Part II
- Clustering stage
    * Dimensionality Reduction methods: t-SNE
    * Clusterization method: k-means with n_clusters=7
    * Create profile for 7 customers' segments (Radar Chart)

## RFM-customers segmentation. Part III. Classification model
- Models:
    * Ensembles: Random Forest, Gradient Boosting

- Metric: Accuracy score

The best result:
* *Model*: Ensembles - Random Forest Classifier
* *Accuracy score on test data*: 0.985

:arrow_up:[to content](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_6#Content)