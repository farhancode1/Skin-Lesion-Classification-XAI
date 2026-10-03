# Skin Lesion Classification Using Explainable AI

An Explainable Artificial Intelligence (XAI) framework for multiclass skin lesion classification using ResNet-18, Grad-CAM, and counterfactual explanations.

## Project Overview

Deep learning models can perform well in medical image classification, but their black-box nature can make their predictions difficult to interpret.

This project explores explainable AI techniques for skin lesion classification. The aim is not only to classify dermoscopic images, but also to understand which image regions influence the model's decision and how predictions change when important lesion features are perturbed.

The project combines a ResNet-18 image classification model with post-hoc explainability methods to provide more transparent and interpretable predictions.

## Dataset

The project uses a dermoscopic skin lesion dataset containing 9,547 images.

The dataset is divided into:

- Training: 6,675 images
- Validation: 1,911 images
- Testing: 961 images

The dataset contains seven skin lesion classes:

- BKL - Benign Keratosis
- NV - Melanocytic Nevi
- DF - Dermatofibroma
- MEL - Melanoma
- VASC - Vascular Lesions
- BCC - Basal Cell Carcinoma
- AKIEC - Actinic Keratoses

The original dataset contains substantial class imbalance. Data balancing and augmentation techniques were therefore used to reduce the dominance of majority classes.

## Model Architecture

The classification model is based on ResNet-18.

Key features include:

- ResNet-18 convolutional neural network
- ImageNet pretrained weights
- Transfer learning
- Input image size: 224 x 224 pixels
- Seven-class classification
- Residual blocks with skip connections
- Global Average Pooling
- Approximately 11 million parameters

The final fully connected layer was modified to output predictions for the seven skin lesion classes.

## Data Preprocessing and Augmentation

The preprocessing pipeline includes:

- Image resizing to 224 x 224 pixels
- Image normalization
- Random rotations
- Horizontal flipping
- Color variation
- Data augmentation for minority classes
- Downsampling of majority classes

These techniques were used to reduce class imbalance and improve the model's ability to learn from underrepresented lesion categories.

## Explainable AI Methods

Two main XAI techniques were applied in this project.

### 1. Grad-CAM

Gradient-weighted Class Activation Mapping (Grad-CAM) is used to identify the image regions that contribute most strongly to the model's prediction.

Grad-CAM uses gradient information from the convolutional layers to generate a heatmap highlighting important areas of the lesion.

This helps answer the question:

> Which part of the image influenced the model's prediction?

The Grad-CAM visualizations showed that the model frequently focused on lesion regions rather than only on the surrounding background.

### 2. Counterfactual / Meaningful Perturbation

Meaningful perturbation was used as a counterfactual explanation technique.

Important image regions are modified or removed to observe how the prediction changes.

This helps answer the question:

> What would happen to the model's prediction if an important lesion feature were removed?

In one example, the model originally predicted a lesion as Dermatofibroma with 85.86% confidence. After perturbing an important lesion region, the prediction changed to Basal Cell Carcinoma with 99.34% confidence.

This demonstrates the sensitivity of the model to specific visual features.

## Model Performance

The model achieved the following approximate validation results:

| Metric | Result |
|---|---:|
| Validation Accuracy | 57.1% |
| AUC-ROC | 0.80 |
| Macro F1-Score | 0.27 |
| RMSE | 2.10 |

The training accuracy exceeded 95%, while validation accuracy remained considerably lower.

This indicates that the model shows signs of overfitting and has difficulty generalizing to unseen images.

Performance was also weaker for some minority lesion classes.

## Confusion Matrix Analysis

The confusion matrix showed stronger classification performance for some classes, while several minority classes were more difficult for the model to identify correctly.

This highlights the importance of using class-sensitive evaluation metrics rather than relying only on overall accuracy.

## Why Explainable AI?

Explainability is especially important in medical AI because a prediction alone may not be sufficient for high-risk decision-making.

The XAI methods used in this project provide additional information about how the model reaches its predictions.

Potential benefits include:

- Improving transparency
- Identifying possible model errors
- Understanding model attention
- Investigating prediction sensitivity
- Supporting model auditing
- Identifying failure modes
- Reducing blind trust in black-box predictions

## Stakeholder Perspective

The project considers explainability from multiple perspectives.

### Clinician Perspective

Grad-CAM allows clinicians to observe which parts of the lesion influenced the prediction.

### Patient Perspective

Counterfactual explanations can help communicate how predictions may change when important visual features are altered.

### Auditor / Regulatory Perspective

Performance metrics, confusion matrices, and perturbation analysis can help identify model weaknesses and potential safety concerns.

## Interactive XAI Dashboard

An interactive Gradio-based dashboard was developed to display:

- Input skin lesion image
- Model prediction
- Prediction confidence
- Grad-CAM heatmap
- Grad-CAM overlay
- Counterfactual perturbation
- Confidence comparison
- Model performance information

The dashboard demonstrates how explainability techniques can be integrated into an interactive AI system.

## Technologies Used

- Python
- PyTorch
- Torchvision
- OpenCV
- NumPy
- Pandas
- Albumentations
- Scikit-learn
- Matplotlib
- Seaborn
- Pillow
- Jupyter Notebook
- Gradio

## Repository Structure

```text
Skin-Lesion-Classification-XAI/
│
├── XAI_AA_Final.ipynb
├── XAI_Skin_Lesion_Classification_Report.pdf
├── XAI_Skin_Lesion_Classification_Presentation.pdf
├── requirements.txt
├── .gitignore
└── README.md
