# SF-DS-NLP-Project-1
### by Liliya Kazykhanova
Text Vectorization and Word Embedding

**Case Description**:
Marketplace's clients want to get possibility to check the same product position from different sellers. Our instrument sholud help them to get product cards by product id in online stores based on their descriptions.

**Technical Task**
* Getting Vector representations of text data
* Using these represenations to get recommendation of similar product.

**Type of ML task**
* NLP (getting word embeddings) + Recommendation based on cosine similarity value

**Metrics:**
* Recommender System: cosine similarity

**Data:** sample_data file contains 500 unique ids. Columns:
* id number,
* field with text description - product name and product description

**NOTES**:
* I run it based on Kaggle resources (without accelerator)

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_1/project/nlp-1-project.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_1#Introduction)

[Feature engineering: Text preprocessing](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_1#Feature-engineering:-Text-preprocessing)

[Vectorization: TF-IDF Vectorizer](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_1#Vectorization:-TF-IDF-Vectorizer)

[Vectorization: Word2Vec](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_1#Vectorization:-Word2Vec)


## INTRODUCTION
- Datasets. It's given sample_data csv-file:
    * Columns: id (product unique number) and description (product name + description)
    * 500 unique ids

## **FEATURE ENGINEERING: Text preprocessing**
***Text preprocessing:***

It's necessary to preprocess text data for using in algorithm:
- tokenization — convert sentences to words
- converting the text to lower case
- stopwords removal - frequent words which have not any semantic sense
- removing punctuation, numerical values, some extra examples
- part-of-speech tagging - removing noninformative POS
- lemmatization (WordNetLemmatizer()) - convert the word into a root word

## **VECTORIZATION: TF-IDF VECTORIZER**
- vectorization - numerically representation of text (TfidfVectorizer()), statistical method.

-> Getting pairs with cosine similarity score > than 0.8

## **VECTORIZATION: WORD2VEC**
Word2vec is a technique in NLP for obtaining vector representations of words. These vectors capture information about the meaning of the word and their usage in context. The word2vec algorithm estimates these representations by modeling text in a large corpus.

-> Getting pairs with cosine similarity score > than 0.95