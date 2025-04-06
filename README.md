# 🧬 Breast Cancer Detection with Deep Learning

This project implements **BreastNet**, a custom Convolutional Neural Network (CNN) for classifying breast tissue patches as cancerous or non-cancerous. The pipeline includes preprocessing, training, prediction, and **image reconstruction with cancer detection overlays**, offering interpretable support for medical diagnostics.

---

## 📌 Table of Contents

- [Motivation](#motivation)
- [Dataset](#dataset)
- [Model: BreastNet](#model-breastnet)
- [Image Reconstruction & Visualization](#image-reconstruction--visualization)
- [Results](#results)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## 💡 Motivation

Breast cancer is the most prevalent cancer worldwide, with Invasive Ductal Carcinoma (IDC) accounting for ~80% of all cases. Diagnosing IDC manually from histopathology images is labor-intensive and prone to human error. This project aims to automate this process using deep learning to assist clinicians in identifying cancerous tissue efficiently and accurately.

---

## 🧪 Dataset

We use the **Breast Histopathology Images** dataset from Kaggle, consisting of over 277,000 labeled 50×50 image patches.

- **1 = IDC-positive (cancerous)**
- **0 = IDC-negative (non-cancerous)**

### Preprocessing

- Normalization and conversion to 3×50×50 RGB tensors.
- Addressed class imbalance via undersampling.
- Data augmentations: rotations, flips, color jitter, erasing, and cropping.
- Stratified 70/10/20 split for training, validation, and testing.

---

## 🧠 Model: BreastNet

BreastNet is a deep CNN tailored for binary classification of image patches.

**Architecture Highlights:**

- 6 Convolutional Layers (32 → 512 filters)
- Batch Normalization + SiLU activation
- MaxPooling after first 4 layers
- 3 Fully Connected Layers with dropout
- Optimizer: Adam | Loss: CrossEntropy | LR: 0.002

<!-- Optional image: Model architecture diagram -->

![Model Architecture](images/breastnet_architecture.png)

---

## 🧩 Image Reconstruction & Visualization

A key feature of this project is reconstructing full breast tissue images from predicted patches:

1. **Patch-Based Prediction** — The model processes each 50×50 patch independently.
2. **Reconstruction** — Patches are combined using their encoded (x, y) coordinates from filenames.
3. **Color Overlay** — Detected cancerous patches are highlighted with a visual overlay.

<!-- Optional image: Original tissue sample -->

![Original Tissue Sample](images/original_patch_layout.png)

<!-- Optional image: Reconstructed image with overlay -->

![Cancer Detection Overlay](images/reconstructed_detection_overlay.png)

This visualization helps pathologists localize cancer more efficiently.

---

## 📊 Results

| Metric          | Value  |
| --------------- | ------ |
| **Accuracy**    | 85.00% |
| **Recall**      | 86%    |
| **Specificity** | 84%    |
| **F1-Score**    | 85%    |
| **RMSE**        | 0.39   |

- **High Recall** minimizes false negatives — critical in cancer diagnosis.
- **Safety-First Bias**: Tendency to over-flag (false positives) is acceptable in clinical settings.

<!-- Optional image: Confusion matrix -->

![Confusion Matrix](images/confusion_matrix.png)

---
