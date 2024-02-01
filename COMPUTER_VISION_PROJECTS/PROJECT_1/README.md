# SF-DS-CV-Project-1
### by Liliya Kazykhanova
Image classification: person faces

**Case Description**:
Facial Recognition is the task of making a positive identification of a face in a photo or video image against a pre-existing database of faces

**Technical Task**
* Using the data to build Image classification (faces) model.

**Computer Vision task**
* Image classification
* Using pretrained ResNet model

**Metrics:**
* Accuracy

**Data:** Images are separated into train and valid subfolders by classes (5)

**NOTES**:
* I run it based on Kaggle resources (with GPU accelerator)
* This project (input and output data) is available on Kaggle by the link [version 2](`https://www.kaggle.com/code/liliyak/project-1-image-classification-faces/notebook`)

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_1/project/project-1-image-classification-faces.ipynb)

## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_1#Introduction)

[Feature engineering: Image preprocessing](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_1#Feature-engineering:-Image-preprocessing)

[Model training results](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_1#Model-training-results)

## INTRODUCTION
- Datasets. It's given 2 datasets with images (person faces)
    * 'train' folder with 5 subfolders by classes: 3000 images
    * 'valid' folder with 5 subfolders by classes: 914 images
    * classes:
        - 'bill_gates', 'elon_musk', 'jeff_bezos', 'mark_zuckerberg', 'steve_jobs'

## **FEATURE ENGINEERING: Image preprocessing**
Using transforms method to increase the size and diversity of dataset
- RandomHorizontalFlip(), RandomVerticalFlip(), and RandomResizedCrop()

## **MODEL TRAINING RESULTS**
* criterion for classification task is CrossEntropyLoss()
* optimizer is SGD
* epoch number = 10

| Model | Accuracy |
| :-: | :-: |
| **Own CNN model** | 0.678 |
| **ResNet** | 0.763 |
| <font color='LightSeaGreen'>**ResNeT<br>with pretrained weights**</font> | 0.922 |
| **ResNet<br>Freezing layers and Fine-tuning** | 0.885 |
|  |  |