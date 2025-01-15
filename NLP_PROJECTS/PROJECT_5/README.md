# SF-DS-NLP-Project-5
### by Liliya Kazykhanova
Question Answering

**Case Description**:
In this notebook we fine-tune one of the 🤗 Transformers model (DeBERTa) to a Question Answering (QA) task, which is the task of extracting the answer to a question from a given context. This model selects a span of the input passage as the answer, does not generate new text!.

**Task**
* Extracting the answer to a question with QA transformer model.

**Type of ML/DL task**
* NlP task - Question Answering

**Data:**
* It is a [SberQuAD](https://arxiv.org/pdf/1912.09723) (Sberbank Question Answering Dataset).


**NOTES**:
* I run it based on Kaggle resources (GPU) - [version 12](https://www.kaggle.com/code/liliyak/project-5-question-answering/notebook)

Attention!!! We use only part of the dataset in order to save time to training and GPU resources and memory.

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_5/project/project-5-question-answering.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_5#Introduction)

[Model training](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_5#Model-training)

[Some observations](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_5#Some-observations)


## INTRODUCTION
Our dataset is SberQuAD with:
- 45328 in **training** set
- 5036 in **validation** set
- 23936 in **test** set

Each of them has several important fields:
- **answers**: the starting location of the answer token and the answer text.
- **context**: background information from which the model needs to extract the answer.
- **question**: the question a model should answer.

If we use the whole dataset we'll lose a lot of time at the training stage - around 4 hours!!!
It will be better to use small part of the dataset in order to look how optuna hyperparams optimization works. I get only 8000 training examples and 2000 for validation/test sets.

Preprocessing steps particular to question answering tasks:
* To deal with longer sequences, **truncate only the context** by setting *truncation="only_second"*.
* Map the **start and end positions of the answer** to the original context by setting *return_offset_mapping=True*
* Use the *sequence_ids* method to find which part of the offset corresponds to the question and which corresponds to the context.

`I'll use different functions to preprocess training and validation sets. And preprocessing the validation data will be slightly easier as we don’t need to generate labels. Also we won’t be able to use compute_metrics function to get regular evaluation results during training. We will only use it at the end of training to check the results`

## **MODEL TRAINING**
- Metric for computation: squad
- Training model with base hyperparameters
    - Parameters
        - number of epochs - 5
        - learning_rate - 2e-5
        - optimizer - adamw_torch
        - weight decay - 0.01
    - Model: Improving DeBERTa - "timpal0l/mdeberta-v3-base-squad2"
    - Prediction based on the test set
        {'exact_match': 62.05, **'f1': 81.24**}

- Getting the best hyperparameters by optuna (automatic hyperparameter optimizations)
    - Parameters:
        - Learning rate minimum and maximum (ceiling) named LR_MIN (2e-5) and LR_CEIL (0.01)
        - Weight decay minimum and ceilling named WD_MIN (4e-5) and WD_CEIL (0.01)
        - Warmup minimum and ceilling named WR_MIN (0.01) and WR_CEIL (0.2)
        - Gradient Accumulation minimum and ceilling named MIN_GRAD_ACC (1) and MAX_GRAD_ACC (5)
        - Minimum and maximum epochs named MIN_EPOCHS (2) and MAX_EPOCHS (5)
        - Per device evaluation batch sizes for the training (10) and evaluation sets (10)
        - Number of Optuna trials to implement (3)
    - Model: Improving DeBERTa. `Getting the best hyperparams based on the 0.1 part of the dataset_part (total: 800 train/ 200 val)`
    - The best hyperparams:
        - learning rate ~ 0.00004
        - weight decay ~ 0.003
        - warmup ratio ~ 0.01
        - gradient accumulation step - 1
        - epoch - 4

- Training model with the best hyperparameters
    - Parameters: the best hyperparams (we got them at the previous stage)
    - Model: Improving DeBERTa
    - Prediction based on the test set
        {'exact_match': 61.35, **'f1': 80.77**}

## **SOME OBSERVATIONS**
As you can see, there is no any rapidly changes between metrics as the result of training model based on the base hyperparams VS hyperparams getting from automatic hyperparameter optimizations.

In order to improve the results it will be better to use more data for getting best hyperparams and training model if you have enough resources (time and GPU/CPU memory).