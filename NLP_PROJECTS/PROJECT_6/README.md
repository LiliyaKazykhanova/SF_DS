# SF-DS-NLP-Project-6
### by Liliya Kazykhanova
Transformers in production

**Case Description**:
In this notebook we will reduce model size by distillation and quantization methods.

**Task**
* Check metric results on test data for fine-tuning BERT model before and after applying Distillation & Quantification methods.

**Type of ML/DL task**
* Model compression via distillation and quantization

**Data:**
* It is a [AG news dataset](https://huggingface.co/datasets/fancyzhx/ag_news).


**NOTES**:
* I run it based on Kaggle resources (GPU) - [version 5](https://www.kaggle.com/code/liliyak/project-6-transformers-in-production/notebook)

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_6/project/project-6-transformers-in-production.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_6#Introduction)

[Model training](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_6#Model-training)

[Some observations](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/NLP_PROJECTS/PROJECT_6#Some-observations)


## INTRODUCTION
Our dataset is AG news with:
- 120k in **training** set
- 7,6k in **test** set

Split dataset into train/validation/ test sets: 108k, 12k, 7.6k

Each of them has several important fields:
- **text**: description fields of articles
- **label**: 4 clasess of articles

Preprocessing dataset with relevant tokenizer.

The AG's news topic classification dataset is constructed by choosing 4 largest classes from the original corpus. Each class contains 30,000 training samples and 1,900 testing samples. The total number of training samples is 120,000 and testing 7,600.
It means that as a key metric I can choose *accuracy_score* because our data is balanced

## **MODEL TRAINING**
- Metric for computation: accuracy
- Base model: BERT
- Distilled models: DistilBert, TinyBERT, MiniLM
- Quantized models: dynamic, static, quantization aware training

RESULTS
| Model | Accuracy score on test data | Model size (MB) |
| :-: | :-: | :-: |
| Bert | 0.94 | 438 |
| Distil_Bert | 0.938 | 267.86 |
| Tiny_Bert | 0.91 | 57.43 |
| MiniLM | 0.93 | 133.51 |
| Dynamic_Quantization | 0.935 | 110 |
| Static_Quantization | 0.93 | 0.004 |
| Quantization_aware_training | 0.94 | 0.004 |
|  |  |  |  |  |

## **SOME OBSERVATIONS**
As can be seen from the results tables, the success of the models does not vary by a great margin.
But distilled and quantized models' size is much smaller than bert_base model. It's great!