# SF-DS-Project-7
### by Liliya Kazykhanova
DS Final project (after 1-year): Resume recommender system

**Business Task**:
To create a recommender system that recommends the best-matched resumes to vacancy.

*Description of business situation*: it is a big company. There are a lot of open vacancies (corresponds to different job positions) and pull of resumes (HR specialist has already collected them). Now HR specialist needs to find the best candidate for vacancy from these pull of resumes.

**Technical Task**
* Using Natural Language Processing (NLP) techniques to process resumes and job listings and sort resumes by similarity score in descending order, to create this ultimate resume screening tool.

**Type of ML task**
* Recommender System based on similarity score
* Dimensionality reduction by SVD/ TSNE (for visualization) + Clustering (Kmeans, DBSCAN, Agglomerative clustering) + Recommender System based on similarity score
* Topic modeling (NMF) + Recommender System based on similarity score

**Metrics:**
* Recommender System: cosine similarity 
* Clustering: Silhouette coefficient, Gap statistic - to get optimal number of clusters
* Topic modeling (NMF): coherence score - to evaluate the best number of topics

**Data:** The dataset was found on Kaggle, with a total of 8,653 entries of applicant experiences and ~80K job listings (before dataset cleaning stage)

**NOTES**:
* I run it based on Kaggle resources (without accelerator)
* Git has limit: 100 MB. That's why some of the files are pushed as zip.file
* This project (input and output data) is available on Kaggle by the link (version 5): https://www.kaggle.com/code/liliyak/final-project-updated/notebook

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/blob/main/PROJECT_final/project/Final_project_1st_year_LK.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Introduction)

[Checking dataset: outliers, duplicates](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Checking-dataset-:-outliers-,-duplicates)

[Feature engineering: Text preprocessing](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Feature-engineering:-Text-preprocessing)

[Resume recommendation based on similarity score](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Resume-recommendation-based-on-similarity-score)

[Resume recommendation based on clusters](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Resume-recommendation-based-on-clusters)

[Resume recommendation based on topics](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Resume-recommendation-based-on-topics)

[Further research: Bonus](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Further-research:-Bonus)

## INTRODUCTION
- Datasets. It's given 5 datasets
    * "Combined_Jobs_Final.csv": 84,090 rows, 23 columns
    * "Positions_Of_Interest.csv": 6,560 rows, 4 columns
    * "job_data.csv": 84,090 rows, 3 columns
    * "Experience.csv": 8,653 rows, 13 columns
    * "Job_Views.csv": 12,370 rows, 14 columns

*In this project I use only 2 datasets:*
- Combined_Jobs_Final.csv - with full information about vacancies
- Experience.csv - with full information about resumes

*Vacancy dataset*. We could divide all Columns/features into 4 groups:
- job description (Job.ID, title, description, salary, etc.)
- candidate requirements (job requirements, education level)
- location (city, address, etc.)
- non-informative features (status, Created.At, etc.)

*Resume dataset*. We could divide all Columns/features into 3 groups:
- applicant information (id)
- work experience (position, job experience description, duration of a job, etc)
- employer location (city, state.name, etc.)
- non-informative features (Created.At, Updated.At)

## **CHECKING DATASET: outliers, duplicates**
* Vacancies dataset:
    - Columns with more than 40% of missing values:
        - Industry
        - Requirements
        - Salary
        - Address
After checking explicit and implicit missing values I choose only 3 columns for further study:
- Job_Id, Job_position and Job_description
* Resumes dataset. After checking explicit and implicit missing values I choose only 3 columns for further study:
- Applicant_Id, Job_title and Job_description

## **FEATURE ENGINEERING: Text preprocessing**
- I concatenate Job_position and Job_description information into one column in Vacancies datasets
- I merged all job experiences by applicant ID

***Text preprocessing:***

It's necessary to preprocess text data for using in algorithm:
- tokenization — convert sentences to words
- converting the text to lower case
- stopwords removal - frequent words which have not any semantic sense
- removing punctuation, numerical values, some extra examples
- part-of-speech tagging - removing noninformative POS
- lemmatization (WordNetLemmatizer()) - convert the word into a root word
- vectorization - numerically representation of text (TfidfVectorizer())

## RESUME RECOMMENDATION based on similarity score
- Similarity score: linear_kernel

## RESUME RECOMMENDATION based on CLUSTERS
- Clustering stage
    * Dimensionality Reduction methods: TruncatedSVD -> TSNE for visualisation
    * Clusterization methods: K-means with n_clusters = 45
- Build recommendation based on the clusters and similarity score value

## RESUME RECOMMENDATION based on TOPICS
- Topic modeling stage
    * Topic modeling method: NMF with n_topics=15
- Build recommendation based on the clusters and similarity score value
- Create dataframe with top-10 candidates to each vacancy_id.

## FURTHER RESEARCH
- Data:
    * Get more informative dataframe/ use web scraping to get resumes and vacancies full of information in the next segments: education level, industry, requirenments. It's possible to use *industry* feature as class label and build recommender system based on classification models (LSV, NB, etc. + ensembles). Also if we have any *requirenments* in vacany's postings it will be useful to get information about total years of applicant's work experience from start and end date, for example.
    * Manually check the same job positions with different variation of title name and replace it to one "more popular" example
- Text preprocessing:
    * Expanding abbreviations
    * Use the other type of regex to clean text from information about company's site, merged words, etc.
    * Using another type of algorithm for vectorization (word2vec - Skip-Gram or BERT)
    * Using another method to get part-of-speech (with high level of correct tagging).
- Model:
    * Use topic modeling as LSA or LDA. These methods are more suited in domains where data is in "semantic units" like words.
    * Create classification models in order to predict new resumes to corresponded topics.
    * Explore the other approaches of Recommender System in case when we have no any labeled data.
- **BONUS**: I run sentence transformer model to check group of job positions. It could be used as instrument to create "real" classes of job titles.

:arrow_up:[to content](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/PROJECT_final#Content)