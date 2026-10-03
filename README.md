# Skin Lesion Classification with Explainable AI

A medical computer vision project for **seven-class skin lesion classification** using **ResNet-18**, **Grad-CAM**, and **counterfactual / meaningful perturbation explanations**.

The project goes beyond prediction accuracy by examining **where the model looks, how sensitive predictions are to image regions, and where the model fails**.

## Highlights

- Transfer learning with an ImageNet-pretrained **ResNet-18**
- Seven-class dermoscopic image classification
- Class-imbalance handling with augmentation and sampling strategies
- **Grad-CAM** visual explanations
- **Counterfactual / meaningful perturbation** analysis
- Confusion-matrix and class-sensitive performance analysis
- Interactive **Gradio-based XAI dashboard**
- Full project notebook, report, and presentation included

## Dataset

The project uses a dermoscopic skin-lesion dataset containing **9,547 images** across seven diagnostic classes.

| Split | Images |
|---|---:|
| Training | 6,675 |
| Validation | 1,911 |
| Testing | 961 |

Classes:

- AKIEC — Actinic Keratoses
- BCC — Basal Cell Carcinoma
- BKL — Benign Keratosis
- DF — Dermatofibroma
- MEL — Melanoma
- NV — Melanocytic Nevi
- VASC — Vascular Lesions

The dataset is imbalanced, so augmentation and class-balancing strategies were used to reduce majority-class dominance.

## Model

The classifier is based on **ResNet-18** with ImageNet-pretrained weights.

Key configuration:

- Input size: 224 × 224
- Output classes: 7
- Transfer learning
- Residual architecture with skip connections
- Global average pooling
- Approximately 11 million parameters

The final classification layer was adapted for seven lesion classes.

## Explainable AI

### Grad-CAM

Grad-CAM is used to identify image regions that most strongly influence the model's prediction.

This provides a visual answer to:

> Which parts of the image contributed most to this prediction?

The resulting heatmaps make it easier to inspect whether the model is focusing on lesion regions or potentially relying on irrelevant background information.

### Counterfactual / Meaningful Perturbation

Important image regions are altered or removed and the model is evaluated again.

This helps answer:

> How does the prediction change when an influential image region is perturbed?

In one experiment, a prediction changed from **Dermatofibroma (85.86%)** to **Basal Cell Carcinoma (99.34%)** after perturbing an important region, demonstrating the model's sensitivity to specific visual evidence.

## Results

Approximate validation results:

| Metric | Result |
|---|---:|
| Validation Accuracy | 57.1% |
| AUC-ROC | 0.80 |
| Macro F1-score | 0.27 |
| RMSE | 2.10 |

Training accuracy exceeded 95% while validation accuracy was substantially lower, indicating **overfitting and limited generalization**. Performance was also weaker for several minority classes.

Rather than hiding these limitations, the project uses them as part of the model-auditing and explainability analysis.

## Interactive XAI Dashboard

A Gradio interface was developed to display:

- Input dermoscopic image
- Predicted class
- Prediction confidence
- Grad-CAM heatmap
- Grad-CAM overlay
- Counterfactual perturbation
- Confidence comparison
- Model-performance information

## Repository Contents

```text
Skin-Lesion-Classification-XAI/
├── XAI_AA_Final.ipynb
├── XAI_Skin_Lesion_Classification_Report.pdf
├── XAI_Skin_Lesion_Classification_Presentation.pdf
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

## Run the Project

Clone the repository:

```bash
git clone https://github.com/farhancode1/Skin-Lesion-Classification-XAI.git
cd Skin-Lesion-Classification-XAI
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Then open:

```text
XAI_AA_Final.ipynb
```

The notebook was developed as an experimental research workflow, so dataset paths may need to be adjusted for your local or Google Colab environment.

## Tech Stack

**Python · PyTorch · Torchvision · OpenCV · Albumentations · Scikit-learn · NumPy · Pandas · Matplotlib · Seaborn · Pillow · Gradio · Jupyter**

## Why This Project Matters

Medical AI systems should not be evaluated only by whether they produce a prediction. They should also be inspected for **failure modes, sensitivity, transparency, and generalization**.

This project demonstrates a practical workflow for combining deep-learning classification with post-hoc explainability methods to support more transparent model analysis.

## Limitations

- Validation performance remains substantially below training performance.
- Minority classes are more difficult to classify reliably.
- Explainability methods provide evidence about model behavior but do not prove clinical reasoning.
- This repository is a research/educational project and is **not intended for clinical diagnosis**.

## License

This repository is released under the MIT License.
