#  Breast Cancer Detection: Deep Learning Classification and Segmentation

![Language](https://img.shields.io/badge/Language-Python-blue)
![Course](https://img.shields.io/badge/Course-Deep_Learning_for_AI-brightgreen)
![Status](https://img.shields.io/badge/Status-Completed-success)

##  Overview
This repository contains a deep learning project focused on the early detection of breast cancer using ultrasound images. It implements a dual-task approach: 
1. **Classification:** Determining the presence and type of cancer (benign, malignant, or normal) using a modified Convolutional Neural Network (ResNet18).
2. **Segmentation:** Identifying and localizing cancerous tissues at the pixel level using a U-Net architecture.

##  Academic Context
* **Authors:** Giorgia Cappellato, Andrea Frattesi
* **Course:** Deep Learning for AI
* **Institution:** Università Cattolica del Sacro Cuore

##  Dataset
The project utilizes a dataset of 780 grayscale ultrasound images collected over a year at Baheya hospital (sourced from Kaggle). 
* **Class Distribution:** 487 Benign, 210 Malignant, and 133 Normal cases.
* **Annotations:** Images in the benign and malignant groups include freehand segmentation masks provided by expert radiologists.
* **Data Augmentation:** To ensure consistency and reduce overfitting, training images were resized to 256 pixels, center-cropped to 224 pixels, and subjected to random horizontal/vertical flips and rotations.

##  Model Architectures & Training

### 1. Classification (ResNet18)
* **Architecture:** Adapted a pre-trained ResNet18 model to accept four input channels (RGB + mask) by modifying the first convolutional layer, improving the network's focus on relevant scan areas. Residual connections were utilized to mitigate the vanishing gradient problem.
* **Loss Function:** Cross Entropy Loss.
* **Optimizer:** Stochastic Gradient Descent (SGD) with a learning rate of 0.001, momentum of 0.9 (Nesterov accelerated), and weight decay of 1e-5.
* **Scheduler:** StepLR (step size 10, gamma 0.1).

### 2. Segmentation (U-Net)
* **Architecture:** Developed a U-Net model from scratch, featuring an Encoder for feature extraction and a Decoder for upsampling, linked by Skip Connections to preserve object boundaries and high-resolution spatial information.
* **Loss Function:** Binary Cross-Entropy with Logits Loss (combining Sigmoid activation and BCE).
* **Optimizer:** SGD with Nesterov momentum (0.9) and weight decay (1e-5).
* **Scheduler:** Cosine Annealing (learning rate decreasing from 0.1 to 1e-5 over 50 epochs).

##  Key Results
* **Classification Performance:** The model achieved outstanding Receiver Operating Characteristic (ROC) scores, with an Area Under the Curve (AUC) of 1.00 for normal cases, 0.97 for benign cases, and 0.94 for malignant cases.
* **Segmentation Accuracy:** Tumor regions were accurately localized. The optimal prediction threshold was identified at 0.5, which provided the best trade-off between false positives and false negatives by maximizing the average Intersection over Union (IoU).

##  Future Work & Limitations
While the model generalizes well, the relatively small dataset restricts real-world robustness. Future improvements could involve collecting larger datasets and integrating multi-modal information, such as patient history or genetic data.

##  How to Run the Project
1. Clone the repository:
   ```bash
   git clone [https://github.com/tuousername/breast-cancer-detection.git](https://github.com/tuousername/breast-cancer-detection.git)
