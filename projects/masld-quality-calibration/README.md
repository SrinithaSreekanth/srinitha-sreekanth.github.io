# Quality-Aware Evaluation and Confounding Analysis of Deep Learning Models for Ultrasound-Based MASLD Detection

Srinitha Sreekanth · Project Associate, Office of IC&SR
Indian Institute of Technology (IIT) Madras

---

## Overview

Deep learning models routinely report very high accuracy for detecting Metabolic Dysfunction-Associated Steatotic Liver Disease (MASLD) from ultrasound — but high accuracy alone doesn't confirm the model is actually reading disease-specific biomarkers rather than exploiting shortcuts in the data. This study builds a quality-aware, explainable framework to test that directly, training EfficientNet-B0 and ResNet-18 on 4,500 cropped liver ultrasound images from public datasets, then interrogating *why* the models perform as well as they do.

## Methods

- **Datasets:** LUS-7Seg (healthy liver scans) and a NAFLD/MASLD dataset, combined and standardized to grayscale 224×224 B-mode images
- **Leakage auditing:** MD5 hashing for exact duplicates + perceptual hashing (pHash) for near-duplicates, with patient-level splits wherever possible
- **Preprocessing:** automated ROI cropping (removing probe interface, depth text, and acoustic cone borders via OpenCV) + CLAHE contrast enhancement
- **Image-quality metrics:** brightness, contrast, sharpness, and entropy, extracted per image
- **Models:** EfficientNet-B0 and ResNet-18, fine-tuned for binary classification (normal vs. MASLD) with AdamW + binary cross-entropy over 5 epochs
- **Explainability:** Grad-CAM to visualize whether model attention lands on liver parenchyma or elsewhere
- **Confounding check:** a separate classifier trained purely to predict *dataset origin* (not disease) — if that succeeds too well, it signals the disease label is confounded with scanner/source artifacts

## Results

**Model performance**

| Metric | EfficientNet-B0 | ResNet-18 |
|---|---|---|
| Accuracy | 99.53% | 97.63% |
| AUC | 99.99% | 99.12% |
| Precision | 99.57% | 95.31% |
| Recall | 99.15% | 98.73% |
| F1 Score | 99.36% | 96.89% |

**Data leakage audit:** 93 exact (MD5) duplicates and 85 near-duplicates (pHash) removed, leaving a clean 4,458-image dataset (3,150 train / 675 validation / 633 test) with zero cross-split overlap.

**Quality-stratified accuracy:** EfficientNet-B0 held ~99.53% accuracy uniformly across low, medium, and high sharpness groups — performance didn't depend on image quality at all.

## Key Finding: The Accuracy Is Confounded

A ResNet-18 trained only to guess which *dataset* an image came from — with no disease label at all — hit 99.11% accuracy (AUC 1.0000). Since dataset origin correlates almost perfectly with disease status here, this means the "disease classifier" may largely be a disguised *scanner classifier*. Grad-CAM backed this up: activation on MASLD images was diffuse and spread across texture-rich regions rather than localized to the liver parenchyma, consistent with the model keying on scanner speckle noise and probe signatures rather than genuine hepatic biomarkers.

MASLD images also had systematically different baseline image properties (lower brightness, lower contrast, lower sharpness, higher entropy) than healthy images — differences that stem from the datasets themselves, not necessarily the disease.

## Why This Matters

Near-perfect accuracy in a single-source or poorly-audited multi-source setup can look like a clinical win while actually being a data artifact. This framework — leakage auditing, quality stratification, source-confounding checks, and Grad-CAM — is offered as a template for catching that failure mode before it reaches deployment.

## Limitations

- Healthy and MASLD images came from separate datasets, so disease status and acquisition source are entangled
- Patient-level identifiers weren't consistently available across both datasets
- No external multi-center validation yet; no disease-severity/fibrosis staging
- Findings show *risk* of shortcut learning, not a definitive proof the models learned zero real biomarkers

## Future Work

Demographic subgroup evaluation (sex, age, BMI), calibration metrics (Brier score, ECE), domain adaptation and dataset harmonization, and multi-center external validation.

---

