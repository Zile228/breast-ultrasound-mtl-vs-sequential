# Breast Ultrasound Comparative Analysis with Deep Learning

This repository contains the implementation and experiment results of a deep learning study comparing **Sequential** and **Multitask Learning (MTL)** architectures for breast ultrasound image analysis. The two tasks include **tumor segmentation** and **lesion classification** into three classes: normal, benign, and malignant.

## 🧠 Objectives

- Compare the overall effectiveness of **Sequential** vs **MTL** learning frameworks.
- Evaluate the contribution of architectural modules: **Deformable Convolution** and **Capsule Network**.
- Validate results with statistical tests to ensure significance.

## 🏗️ Architectures & Variants

All models are based on **UNet with EfficientNet-B4** backbone.  
Key architectural variants:

- **ConvBlock** vs **DeformableConvBlock**
- **Fully Connected** vs **Capsule Network**
- Sequential: segmentation → classification
- MTL: shared backbone with dual-output branches

## ⚙️ Experiment Setup

- **Input size**: 256×256, normalized
- **Split**: 80% train / 20% test
- **Augmentation**: rotation, flip (horizontal/vertical)
- **Training**: 100 epochs, batch size 32, LR `2e-4`, T4×2 GPU (Kaggle)
- **Callbacks**: Early Stopping, ReduceLROnPlateau

## 📈 Evaluation Metrics

| Task            | Metrics              |
|-----------------|----------------------|
| Segmentation    | Dice, IoU            |
| Classification  | Accuracy, F1-score   |
| Efficiency      | Params, FLOPs, Time  |

Each model was trained **30 times**. All scores are reported as **mean ± std**.

## 📁 Folder Structure

```📁 breast-ultrasound-mtl-vs-sequential/
├── README.md
├── data/       # 30-run metrics for each model
│    ├── Multi-Task Learning/   
│    │   ├── MTL_ConV-Capsnet.xlsx
│    │   ├── MTL_ConV-FC.xlsx
│    │   ├── MTL_Deform-Capsnet.xlsx
│    │   └── MTL_Deform-FC.xlsx                  
│    └── Sequential Learning/
│        ├── ST_ConV-Capsnet.xlsx
│        ├── ST_ConV-FC.xlsx
│        ├── ST_Deform-Capsnet.xlsx
│        └── ST_Deform-FC.xlsx
├── src/  # Source code
│   ├── bgra-busi-full-implementation.ipynb
│   ├── Multi-task Testing.ipynb
│   ├── Multi-task vs Sequential Testing.ipynb
│   └── Sequential Testing.ipynb
```


## 🔬 Statistical Testing

### 1. Overall Comparison (Sequential vs MTL)
- **Shapiro-Wilk Test** for normality
- If non-normal: **Mann-Whitney U Test**
- If normal:
  - **Levene’s Test** for variance
  - → Equal variance: **T-test**
  - → Unequal variance: **Welch’s T-test**

### 2. Module Comparison (Ablation Study)
- ≥3 model groups:  
  - If non-normal: **Kruskal-Wallis H Test** → **Dunn’s post-hoc**
  - If normal:
    - Levene’s Test:
      - Equal variance: **One-way ANOVA** → **Tukey’s HSD**
      - Unequal variance: **Welch’s ANOVA** → **Games-Howell**



