# SF-DS-NLP-Project-5
### by Liliya Kazykhanova
Question Answering

**Case Description**:
In this notebook we will train a Question Answering model using DeBERTa.

**Technical Task**
* Using the data to build a Question Answering model.

**Type of ML/DL task**
* Token Classification (NER)

**Data:**
* It is a [SberQuAD](https://arxiv.org/pdf/1912.09723) (Sberbank Question Answering Dataset).


**NOTES**:
* I run it based on Kaggle resources (GPU) - [version 7](https://www.kaggle.com/code/liliyak/project-5-question-answering)

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
It will be better to use small part of the dataset in order to look how optuna hyperparams optimization works. I get only 5000 training examples and 1250 for validation.

Preprocessing steps particular to question answering tasks:
* To deal with longer sequences, **truncate only the context** by setting *truncation="only_second"*.
* Map the **start and end positions of the answer** to the original context by setting *return_offset_mapping=True*
* Use the *sequence_ids* method to find which part of the offset corresponds to the question and which corresponds to the context.

`I'll use the same function to preprocess training and validation sets in order to check metrics as exact match (EM) and F1 score during training and validation stage`

## **MODEL TRAINING**
- Metric for computation: squad
- Training model with base hyperparameters
    - Parameters
        - batch size - 12
        - number of epochs - 5
        - learning_rate - 3e-5
        - optimizer - adamw_torch
        - weight decay - 0.01
        - gradient accumulation - 8
        - warmup - 0.1
    - Model: Improving DeBERTa - "timpal0l/mdeberta-v3-base-squad2"
    - Result: 
        | Step | Training Loss | Validation Loss | F1 |  Exact Match |
        | :-: | :-: | :-: | :-: | :-: |
        | 50 | 2.537400 | 1.784241 | 0.844313 | 0.652000 |
        | 100 | 1.595600 | 1.680552 | 0.834757 | 0.647200 |
        |  |  |  |  |  |
    - Evaluate on the full test set:
        {**'eval_loss': 7.6507954597473145**,
        **'eval_f1': 0.037796401565128666**,
        **'eval_exact_match': 0.0**,
        'eval_runtime': 562.6968,
        'eval_samples_per_second': 42.538,
        'eval_steps_per_second': 1.774,
        'epoch': 4.976076555023924}

- Getting the best hyperparameters by optuna (automatic hyperparameter optimizations)
    - Parameters:
        - Learning rate minimum and maximum (ceiling) named LR_MIN (4e-5) and LR_CEIL (0.01)
        - Weight decay minimum and ceilling named WD_MIN (4e-5) and WD_CEIL (0.01)
        - Warmup minimum and ceilling named WR_MIN (0.01) and WR_CEIL (0.2)
        - Gradient Accumulation minimum and ceilling named MIN_GRAD_ACC (1) and MAX_GRAD_ACC (5)
        - Minimum and maximum epochs named MIN_EPOCHS (2) and MAX_EPOCHS (5)
        - Per device evaluation batch sizes for the training (10) and evaluation sets (10)
        - Number of Optuna trials to implement (3)
    - Model: Improving DeBERTa. `Getting the best hyperparams based on the 0.1 part of the dataset_part (total: 500 train/ 125 val)`
    - The best hyperparams:
        - learning rate - 8.224316278391225e-05
        - weight decay - 0.0016061074719990397
        - warmup ratio - 0.01372725577861470
        - gradient accumulation step - 5
        - epoch - 5

- Training model with the best hyperparameters
    - Parameters: the best hyperparams (we got them at the previous stage)
    - Model: Improving DeBERTa
    - Result: 
        | Step | Training Loss | Validation Loss | F1 |  Exact Match |
        | :-: | :-: | :-: | :-: | :-: |
        | 100 | 1.976200 | 1.641488 | 0.837407 | 0.641600 |
        | 200 | 1.127900 | 1.904699 | 0.758720 | 0.561600 |
        |  |  |  |  |  |
    - Evaluate on the full test set:
        {**'eval_loss': 9.664545059204102**,
        **'eval_f1': 0.038647634497779845**,
        **'eval_exact_match': 0.0**,
        'eval_runtime': 557.6996,
        'eval_samples_per_second': 42.919,
        'eval_steps_per_second': 2.146,
        'epoch': 5.0}

## **SOME OBSERVATIONS**
As you can see, there is no any rapidly changes between metrics as the result of training model based on the base hyperparams VS hyperparams getting from automatic hyperparameter optimizations.

Moreover loss and metric values are not stable (and worse than at the first trainig experiments) during training based on the best hyperparams because I got only small part of the dataset for that.

- It will be better to use more data for getting best hyperparams and training model if you have enough resources (time and GPU/CPU memory).

But in this case I want to check only:
- how does optuna work for transformer model
- baseline value of f_1 score and exact_match

And we got it!