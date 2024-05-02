# SF-DS-CV-Project-2
### by Liliya Kazykhanova
Face mask detection

**Case Description**:
In this work, a deep learning based model for detecting masks over faces in public place to curtail community spread of Coronavirus is presented.

**Technical Task**
* Using the data to build Face mask detection model (CV task).

**Data:** Dataset consists of 2 folders - *annotations* and *images* of faces with mask or without.

**Metrics:**
* mAP (mAP_50)

**Computer Vision algorithms**:
- Using pretrained Faster R-CNN model (Faster RCNN ResNet50 FPN V2)
- Using pretrained YOLO model (Yolov8)

*Training on GPU (Kaggle resources)*

*Note: Images classification is an example of supervised machine learning since we train the model with labelled data.*

[Link to Project](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_2/project/project-2-face-mask-detection.ipynb)


## Content
[Introduction](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_2#Introduction)

[Model training results](https://github.com/LiliyaKazykhanova/SF_DS/tree/main/COMPUTER_VISION_PROJECTS/PROJECT_2#Model-training-results)

## INTRODUCTION
- Datasets. It's given dataset with 853 unique images marked by 3 classes:
    * with mask
    * without mask
    * mask weared incorrect

## **MODEL TRAINING RESULTS**
* Faster RCNN ResNet50 FPN V2
    - split data to traininig and validation set by 80/20
    - epoch number - 20 (early stopping at 12 epochs)
    - optimizer - SGD
* YOLOv8
    - split data to traininig and validation set by 90/10
    - epoch number - 40

| Model | mAP (all) |
| :-: | :-: |
| **Faster RCNN ResNet50 FPN V2** | 0.88 |
| **YOLOv8** | 0.898 |