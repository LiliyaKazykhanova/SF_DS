# SF-DS-Project-3-EDA
## Project: Booking.com reviewer score

*Task*: using the data to build a model that predicts the rating of the hotel

*Data*: csv-file contains 16 features + 1 target (reviewer_score)

*Metrics*: MAPE

*Notes*: 
* This notebook is copied from Kaggle
* Some of the graphs are coded as plotly charts. But they are not showing up in Git
* In order to show plotly (px) charts you can add this code - fig.write_image('fig.png')

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/blob/main/PROJECT_3/project_3/project_3_EDA_LK.ipynb)

### Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_3#Introduction)

[Checking dataset: outliers, duplicates](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_3#Checking-dataset-:-outliers-,-duplicates)

[Feature Engineering](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_3#Feature-Engineering)

[Encoding Features](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_3#Encoding-Features)

[Feature Selection](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_3#Feature-Selection)

[Machine Learning](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_3#Machine-Learning)

#### Introduction
I joined train and test data into one main dataset for the correct feature processing.
- dataset shape: 515738 rows, 18 columns (added sample column in order to distinguish train and test data)
- target value: review_score

#### Cheking dataset: outliers, duplicates
- Number of found duplicates: 336
- Columns with missing values: lat and lng
In order to get correct submission file in Kaggle I did not delete full duplicates.

#### Feature Engineering
- Date of review:
    * converted to datetime type
    * getting 9 new features - year, month, day, day of week, weekend/ not, 4 season
- Days since review:
    * extracting numeric value
    * getting 1 new feature - fresh/ not review
- Hotel address:
    * getting 2 new columns - country, city
    * adding new feature - population in city
- Lat and lng:
    * filling MV by mode value
    * creating new feature - distance to center
- Reviewer nationality:
    * Almost 50% of reviewers are from UK
    * I decided to encode this column as reviewer is from the same country as hotel - 1/0
- Tags:
    * getting new features:
        - stayed nights,
        - trip type (business/ leisure),
        - guest status (solo, couple, friends, family, group)
        - room occupancy (number of sleep place)
        - room with view (0/1)
- Positive and negative review
    * getting 4*2 new columns as a result of sentiment analysis - NLTK model
        - neutrality score
        - positivity score
        - negativity score
        - compound - overall score that summarizes the previous scores
- Total number of reviews
    * updating number corresponds to this dataset
- Average score:
    * updating score corresponds to median value of reviewer score
- Word count in review:
    * getting new feature - proportion of word count in positive review

#### Encoding Features
- leisure trip - 0/1
- business trip - 0/1
- hotel country by One-Hot Encoding
- guest status by One-Hot Encoding

#### Feature Selection
- droped duplicated columns
- droped object columns
- checked correlation between numeric and categorical features (spearman method)
- droped 4 columns:
    * additional_number_of_scoring
    * is_weekend
    * year
    * city_population_k

#### Machine Learning
- Total feature number: 46
- Model: RandomForestRegressor
*Parameters:*
    * n_estimators=100,
    * verbose=1,
    * n_jobs=-1,
    * random_state=42
- MAPE: 12.58869
- Top-5 meaningful features:
    * proportion of positive word count (to total number)
    * p_compound (NLTK)
    * average score (median value)
    * n_compound (NLTK)
    * day since review (fresh / old)

(In earlier version of notebook I got MAPE value 12.53914. But this version is more interesting by feature engineering stage)

:arrow_up:[to content](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_3#Content)
