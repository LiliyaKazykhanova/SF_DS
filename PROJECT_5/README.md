# SF-DS-Project-5
DS Project 5: New York City Taxi Trip Duration

*Business Task*
A typical taxi company faces a common problem of efficiently assigning the cabs to passengers so that the service is smooth and hassle free. One of main issue is determining the duration of the current trip so it can predict when the cab will be free for the next trip.

The data set contains the data regarding several taxi trips and its duration in New York City. 

*Technical Task*: Using the data to build a model that predicts the total ride duration of taxi trips in New York City.

*Data*: The csv file contains about 1.5 mln rows and 11 columns (10 + 1 target)

*Type of ML task*: Regression

*Metrics*: RMSLE (Root Mean Squared Log Error)

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/blob/main/PROJECT_5/project_5/project_5_Regression_LK.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_5#Introduction)

[Checking dataset: outliers, duplicates](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_5#Checking-dataset-:-outliers-,-duplicates)

[Eda. Feature Engineering](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_5#Eda.-Feature-Engineering)

[Feature Selection](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_5#Feature-Selection)

[Machine Learning Models](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_5#Machine-Learning-Models)

## Introduction
Work on this project based on the next 6 datasets:
* taxi_data - dataset for training
* test_data - dataset for prediction
* osrm_train - osrm for train part (*OSRM (Open Source Routing Machine) is an open-source router (compute the shortest path)*)
* osrm_test - osrm for test part
* holiday_data - dataset with holiday informatio
* weather_data - weather dataset


- train dataset's shape: 1_458_644 rows, 11 columns
- target value: *trip duration*

## Cheking dataset: outliers, duplicates
- Number of found duplicates: 0
- Columns with missing values: 0

## EDA. Feature Engineering
***Creating new features:***

- Time feautures:
    * pickup_date - date of turning on the meter / start of the trip (without time)
    * pickup_hour - hour of turning on the counter
    * pickup_day - day of the week on which the counter was enabled
    * pickup_holiday
- Geographic Information:
    * total_distance - the shortest path (in meter) from start to end
    * total_travel_time - minimum travel time (in sec) from start to end
    * number_of_steps -number of driver's discrete steps (turn left / turn right / go straight)
    * haversine_distance
    * direction
    * create 10 geo_clusters by kmeans method based on latitude and longitude coordinates
- Weather data:
    * temperature
    * visibility
    * wind speed - wind average speed
    * precip - rainfall
    * events - weather conditions

***Filling missing values by median or None values***

***Cleaning data from outliers***

## Feature Selection
- delete non-informative features and variables with data leakage:
    * id
    * dropoff_datetime
- encoding categorical features:
    * vendor_id and store_and_fwd_flag - binary encoding
    * pickup_day, geo_cluster, events, pickup_timezone - One-Hot Encoding ((get dummies))
- getting 25 meaningful features by SelectKBest method
- feature normalization by MinMaxScaler

## Machine Learning Models
- Total feature number: 25
- Models:
    * Logistic Regression, Logistic Regression with Polynomial features, Logistic Regression + Poly + L2
    * Decision Tree,
    * Ensembles: Random Forest, Gradient Boosting, XGBoost

- Metric: RMSLE

The best result:
* *Model*: Ensembles - XGBoost
* *RMSLE score on valid data*: 0.39

- Top-3 meaningful features:
    * haversine_distance
    * dropoff_latitude
    * pickup_longitude

:arrow_up:[to content](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_5#Content)