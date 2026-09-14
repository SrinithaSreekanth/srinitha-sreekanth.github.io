# Quantifying Subject-Level Heterogeneity in Facial Electromyography

**A Small-Sample Cross-Validation Study for Assistive Control Models**

*Undergraduate Extension Study — Machine Learning Reanalysis of a Prior Hardware System*

Srinitha Sreekanth · Department of Biomedical Engineering
Independent Researcher / Project Associate, IIT Madras

---

## Overview

Assistive control interfaces based on facial electromyography (sEMG) are usually built and evaluated as pooled, subject-generalized models — the underlying assumption being that variation *between* people matters less than the consistency of the signal *within* one person. This study puts that assumption to the test.

Using a previously collected facial-sEMG wheelchair command dataset (5 commands, 10 subjects, 120 trials total), three classical classifiers — Logistic Regression, XGBoost, and K-Nearest Neighbors — were evaluated under rigorous 5-fold stratified cross-validation. The core question: does pooling data across subjects meaningfully hurt performance compared to training a separate, personalized model per subject?

## Relation to Prior Work

The hardware, electrode placement (Buccinator and Zygomaticus Major muscles), and signal acquisition protocol used to collect this dataset came from an earlier published project — a threshold-based facial-EMG wheelchair control system. That work had no learned classifier, no cross-validation, and no analysis of inter-subject variability. This study reuses the same trial recordings purely as a dataset source to ask a new, independent statistical question — all modeling and analysis here is original to this study.

## Methodology

- **Dataset:** 120 labeled sEMG trials (Forward, Backward, Left, Right, Stop — 24 trials each) from 10 subjects, recorded on a BIOPAC MP45, band-pass filtered 30–500 Hz
- **Features:** 8 time- and frequency-domain features per trial — Mean Absolute Value, RMS, Integrated EMG, Waveform Length, Zero Crossings, Slope Sign Changes, Mean Frequency, Median Frequency
- **Baseline:** stratified 5-fold cross-validation on the full pooled dataset
- **Heterogeneity test:** personalized (within-subject) models vs. leave-one-subject-out (LOSO) generalized models — if heterogeneity matters, personalized should beat LOSO

## Results

**Generalized 5-fold cross-validation performance**

| Model | Mean Accuracy | Std. Dev. |
|---|---|---|
| Logistic Regression | 57.50% | ± 4.86% |
| XGBoost | 56.67% | ± 8.58% |
| K-Nearest Neighbors | 48.33% | ± 5.65% |

**Personalized vs. generalized validation**

| Scheme | Description | Mean Accuracy |
|---|---|---|
| Within-subject (personalized) | Trained & tested on each subject's own trials | 58.33% |
| Leave-one-subject-out (generalized) | Trained on 9 subjects, tested on the 10th | 59.17% |

## Key Finding

No meaningful heterogeneity penalty was observed — the generalized model *slightly outperformed* the personalized one (+0.83 pp), a gap well within the expected noise floor of a 120-trial dataset. Reported as a null result: at this sample size, trial-to-trial noise appears to dominate any true inter-subject variance. That's informative on its own — it argues against investing in subject-specific personalization before first addressing dataset scale.

## Limitations

- Personalized models trained on only ~2–3 trials per class per subject — likely too few to build a reliable subject-specific boundary
- A null result here doesn't disprove inter-subject heterogeneity in facial sEMG generally — it means this dataset is underpowered to detect it
- No claim is made about real-world deployable classification accuracy; the contribution is methodological
