# SF-DS-NLP-Project-2
### by Liliya Kazykhanova
Text Classification (sentiment)

**Case Description**:
Text Sentiment classification is the automated process of identifying and classifying emotions in text as positive sentiment, negative sentiment, or neutral sentiment based on the opinions expressed within. It helps determine the nature and extent of feelings conveyed using Natural Language Processing (NLP) to understand what people say or feel about different cases.

**Technical Task**
* Using the data to build a model that predicts text sentiment.

**Type of ML/DL task**
* NLP: Classify texts with RNN

**Metrics:**
* Accuracy

**Data:**
* Train dataset with *Text* description and *Sentiment*,
* Test dataset with *Text* description and *id* number.


**NOTES**:
* I run it based on Kaggle resources (GPU)

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_2/project/project-2-text-classification.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_2#Introduction)

[Feature engineering: Text preprocessing](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_2#Feature-engineering:-Text-preprocessing)

[Model training: RNNs in different variants](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_2#Model-training:-RNNs-in-different-variants)

[Results](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_2#Results)

[Recommendations](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_2#Recommendations)


## INTRODUCTION
- Train dataset: 41159 examples
- Test dataset: 3798 examples

## **FEATURE ENGINEERING: Text preprocessing**
***Text preprocessing:***

It's necessary to preprocess text data for using in algorithm:
- tokenization — convert sentences to words
- converting the text to lower case
- stopwords removal - frequent words which have not any semantic sense
- removing punctuation, numerical values, some extra examples
- lemmatization (WordNetLemmatizer()) - convert the word into a root word

*Using Language Detector (sparknlp) model to check text language*

## **MODEL TRAINING: RNNs in different variants**
*Compute class weight to control unbalanced data*
- Simple RNN model with Keras tokenizer
- LSTM with word embeddings (GloVe vectors):
    - 2 LSTM layers + Simple RNN
- GRU with word embeddings (GloVe vectors):
    - GRU + Simple RNN
- Bi-Directional RNN's with word embeddings (GloVe vectors)

## **RESULTS**

| Model | Accuracy (train) | Accuracy (val) |
| :-: | :-: | :-: |
| **Simple RNN** | 0.88 | 0.69 |
| <font color='LightSeaGreen'>**LSTM**</font> | 0.69 | 0.7 |
| **GRU** | 0.66 | 0.65 |
| **Bi-Directional RNN** | 0.65 | 0.65 |
|  |  |  |

**RECOMMENDATIONS for further work:**
* Data preprocessing:
    - recheck rare words. If there are word counts less than 2 it has a sense to delete them as outliers.
    - recheck text language. If our dataset contains of examples with different languages and we use it for model training (if our task is not *translating*). After we will get model with poor predictive model. In this project I showed how it's possible to use Language Detector model.
* Text vectorization:
    - Using another type of algorithm for vectorization (word2vec - Skip-Gram or BERT from Transformers)
* NN model:
    - Hyperparameter tuning for previously discussed examples: increasing epochs number, use more complex architecture, change batch size, choose optimal optimizer with accordnig learning rate
    - Or I can use BERT Transformers which learns contextual relations between words in a sentence/text.