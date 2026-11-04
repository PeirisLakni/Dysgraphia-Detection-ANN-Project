# Potential Dysgraphia Screening from Handwriting

## Project overview

Dysgraphia can affect handwriting legibility, letter formation, spacing, alignment, and consistency. Conventional handwriting assessment can require substantial manual effort and may vary between evaluators. This project investigates an AI-assisted approach for analyzing handwriting samples and flagging cases that may warrant further assessment.

The core model is planned as a specialized Artificial Neural Network (ANN) that combines visual features extracted from three sentence samples per child. A pretrained MobileNetV2-based convolutional neural network (CNN) is proposed for feature extraction, with an ANN for child-level binary classification. A Histogram of Oriented Gradients (HOG) and Support Vector Machine (SVM) pipeline will provide a classical machine-learning baseline.

The project also plans to explore Grad-CAM explanations, perturbation-based explanation checks, and the suitability of the Qwen2.5-VL vision-language model for handwriting interpretation or an adjacent task. A prototype interface is planned with Streamlit and FastAPI.

## Dataset

The study uses the publicly available **Potential Dysgraphia Dataset** hosted on Mendeley Data. The dataset description for this project reports:

- **249 handwritten images** from **83 children**
- Three sentence samples per child, with increasing sentence complexity
- **Potential Dysgraphia (PD):** 114 images from 38 children
- **Low Potential Dysgraphia (LPD):** 135 images from 45 children

The intended prediction unit is the **child**, not an individual image: the three samples belonging to a child are analyzed collectively to produce one screening prediction.

> Image counts are sample-level counts, while model evaluation should be conducted at child level. Keep all samples from a child within the same data split to prevent identity leakage. Any augmentation or preprocessing used for training must be applied only after splitting.

## Objectives

1. Assess and document dataset quality, class distribution, image characteristics, and data limitations.
2. Develop reproducible preprocessing and exploratory data analysis (EDA) workflows.
3. Train and evaluate a child-level MobileNetV2-feature/ANN classifier and a HOG/SVM baseline.
4. Compare controlled experimental settings, including learning rate, batch size, architecture, regularization, and optimization method.
5. Prioritize recall for the Potential Dysgraphia class while reporting precision, F1-score, specificity, and other relevant metrics.
6. Investigate model explanations with Grad-CAM and assess them through perturbation experiments and incorrect-prediction analysis.
7. Explore Qwen2.5-VL for a meaningful handwriting-related task, documenting performance, resource requirements, speed, and limitations.
8. Build a prototype screening interface, if supported by the project implementation.

## Repository contents

This repository is intended to hold the project’s preprocessing, training, evaluation, and deployment scripts and notebooks, along with documentation and environment setup.

```text
.
├── README.md
├── requirements.txt          # Add or update as dependencies are established
├── data/                     # Local data only; excluded from version control
├── notebooks/                # EDA and experiment notebooks
├── src/                      # Reusable preprocessing, modeling, and evaluation code
├── app/                      # Streamlit/FastAPI prototype, if implemented
├── models/                   # Locally saved model artifacts; do not commit sensitive/large files
└── docs/                     # Methods, dataset notes, and experiment documentation
```

## Responsible use and limitations

This is an experimental educational screening prototype, not a medical or clinical diagnostic system. Dataset size is limited, and labels are preliminary; performance may not generalize across ages, languages, writing tasks, schools, writing instruments, or populations. Handwriting is personal data in many contexts. Protect uploaded samples, minimize retention, restrict access, and obtain appropriate consent and approvals before collecting or processing real-world student data. Human review and further assessment are necessary for any consequential decision.

Generative AI outputs may be inaccurate or inconsistent. Any Qwen2.5-VL experiments should be evaluated separately, with model/version, prompts, computational requirements, and limitations recorded. Do not treat generated descriptions or predictions as ground truth.

## Deployment and explainability plans

A Streamlit interface and FastAPI service are proposed for uploading handwriting samples and presenting model-generated screening results. Deployment must communicate uncertainty and limitations, avoid unsupported diagnostic language, and handle images securely. Grad-CAM visualizations are exploratory explanations, not proof that a model bases decisions on clinically meaningful evidence; explanation quality should be investigated, including with perturbation tests and error analysis.

## Citation and dataset acknowledgement

@article{RAMLAN2024110534,
title = {Development of potential dysgraphia handwriting dataset},
journal = {Data in Brief},
volume = {54},
pages = {110534},
year = {2024},
issn = {2352-3409},
doi = {https://doi.org/10.1016/j.dib.2024.110534},
url = {https://www.sciencedirect.com/science/article/pii/S2352340924005018},
}

This README describes the research plan based on the project summary. Implementation details, dataset DOI/citation, dependency versions, actual directory layout, and runnable commands should be updated to reflect the files and experiments as they are added.
