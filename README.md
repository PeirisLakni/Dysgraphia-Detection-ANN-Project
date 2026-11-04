# Potential Dysgraphia Screening from Handwriting

> **Research prototype — not a diagnostic tool.** This project explores whether handwriting images can support early screening for potential dysgraphia. Predictions are intended only as decision support for qualified educational professionals and must not replace a comprehensive assessment.

## Project overview

Dysgraphia can affect handwriting legibility, letter formation, spacing, alignment, and consistency. Conventional handwriting assessment can require substantial manual effort and may vary between evaluators. This project investigates an AI-assisted approach for analyzing handwriting samples and flagging cases that may warrant further assessment.

The core model is planned as a specialized Artificial Neural Network (ANN) that combines visual features extracted from three sentence samples per child. A pretrained MobileNetV2-based convolutional neural network (CNN) is proposed for feature extraction, with an ANN for child-level binary classification. A Histogram of Oriented Gradients (HOG) and Support Vector Machine (SVM) pipeline will provide a classical machine-learning baseline.

The project also plans to explore Grad-CAM explanations, perturbation-based explanation checks, and the suitability of the Qwen2.5-VL vision-language model for handwriting interpretation or an adjacent task. A prototype interface is planned with Streamlit and FastAPI.

## Dataset

The study uses the publicly available **Potential Dysgraphia Dataset** hosted on Mendeley Data. The dataset description for this project reports:

- **249 handwritten images** from **83 children**
- Three sentence samples per child, with increasing sentence complexity
- **Potential Dysgraphia (PD):** 114 images
- **Low Potential Dysgraphia (LPD):** 135 images

The intended prediction unit is the **child**, not an individual image: the three samples belonging to a child are analyzed collectively to produce one screening prediction. Confirm the dataset's current terms of use, citation requirements, label definitions, and file organization on its Mendeley Data landing page before using or redistributing it. Dataset files are not included in this repository.

> **Important:** Image counts are sample-level counts, while model evaluation should be conducted at child level. Keep all samples from a child within the same data split to prevent identity leakage. Any augmentation or preprocessing used for training must be applied only after splitting.

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

This repository is intended to hold the project’s preprocessing, training, evaluation, and deployment scripts and notebooks, along with documentation and environment setup. The project is under development; update this section as files and workflows are added.

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

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/PeirisLakni/Dysgraphia-Detection-ANN-Project.git
cd Dysgraphia-Detection-ANN-Project
```

### 2. Create an environment

Python version and dependency pins should be documented in the project environment file once implementation choices are finalized. For a virtual environment:

```bash
python -m venv .venv
```

Activate it:

```bash
# Linux/macOS
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Install dependencies when `requirements.txt` is populated:

```bash
pip install -r requirements.txt
```

### 3. Obtain and place the dataset

Download the dataset from its Mendeley Data page, follow its license and citation terms, and place the files in the local data directory. Do not commit the dataset or identifiable handwriting images unless the dataset terms and project approvals explicitly permit redistribution.

The expected directory structure and metadata format should be documented here after verifying the downloaded dataset. Ensure there is a reliable mapping from each image to its child identifier and class label; do not infer child grouping from filenames unless verified.

### 4. Run project workflows

Commands for EDA, preprocessing, training, evaluation, and the application will be added when the corresponding scripts and notebooks are available. Record configuration, random seeds, data split strategy, model checkpoints, and evaluation outputs to support reproducibility.

## Evaluation and experimental integrity

- Split data by **child identifier** (grouped splitting), not by image.
- Keep a held-out test group untouched during model selection and hyperparameter tuning.
- Use validation data or grouped cross-validation for model selection where appropriate.
- Report class-wise performance and confusion matrices. In particular, report PD recall alongside precision, F1-score, specificity, and support.
- State the positive class and metric averaging method explicitly.
- Compare ANN and HOG/SVM approaches using the same leakage-safe splits.
- Document preprocessing, thresholds, random seeds, software/hardware, and deviations from the planned protocol.
- Avoid claims of clinical validity or generalization beyond the dataset without appropriate independent validation.

## Responsible use and limitations

This is an experimental educational screening prototype, not a medical or clinical diagnostic system. Dataset size is limited, and labels are preliminary; performance may not generalize across ages, languages, writing tasks, schools, writing instruments, or populations. Handwriting is personal data in many contexts. Protect uploaded samples, minimize retention, restrict access, and obtain appropriate consent and approvals before collecting or processing real-world student data. Human review and further assessment are necessary for any consequential decision.

Generative AI outputs may be inaccurate or inconsistent. Any Qwen2.5-VL experiments should be evaluated separately, with model/version, prompts, computational requirements, and limitations recorded. Do not treat generated descriptions or predictions as ground truth.

## Deployment and explainability plans

A Streamlit interface and FastAPI service are proposed for uploading handwriting samples and presenting model-generated screening results. Deployment must communicate uncertainty and limitations, avoid unsupported diagnostic language, and handle images securely. Grad-CAM visualizations are exploratory explanations, not proof that a model bases decisions on clinically meaningful evidence; explanation quality should be investigated, including with perturbation tests and error analysis.

## Citation and dataset acknowledgement

Please cite the Potential Dysgraphia Dataset using the citation provided on its Mendeley Data page. Add the exact dataset DOI and citation here after confirming the version used. Also cite relevant model architectures, libraries, and methods in project reports and documentation.

## License

The repository’s code license and the dataset’s license are separate. Check the dataset’s terms before use or redistribution. Add a repository license if and when the project owner chooses one.

## Project status

This README describes the research plan based on the project summary. Implementation details, dataset DOI/citation, dependency versions, actual directory layout, and runnable commands should be updated to reflect the files and experiments as they are added.
