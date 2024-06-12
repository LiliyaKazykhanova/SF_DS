# SF-DS-CV-Project-3
### by Liliya Kazykhanova
Spacecraft segmentation

**Case Description**:
Semantic Segmentation of spacecraft components.

**Technical Task**
* Using the data to build a model to predict spacecraft trajectory in order to avoid their collision with space debris.

**Data:** Dataset consists of 2 folders - *images* and *mask* dataset divided into train and val part.

**Metrics:**
* to achieve mIoU > 0.70 on the validation sample

**Semantic Segmentation Task model**:
- DeepLabV3+

*Training on GPU (Kaggle resources)*

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_3/project/project-3-satelite-segmentation.ipynb)


## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_3#Introduction)

[Model training results](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_3#Model-training-results)

## INTRODUCTION
- Datasets. It's given dataset with 2517 images with mask in Train and 600 in Valid dataset marked by 3+1 classes:
    * solar panels,
    * spacecraft,
    * antennas,
    * and background.

## **MODEL TRAINING RESULTS**
* DeepLabV3+
    - epoch number - 5
    - optimizer - Adam
    - the initial learning rate to vary at the beginning of the epochs according to the "cosine annealing with warm restarts" schedule.

| Model | IoU Train | IoU Test |
| :-: | :-: | :-: |
| **DeepLabV3+** | 0.919 | 0.8587 |