# Enhancing Cloud Security through Deep Learning-Based Architecture of Intrusion Detection and Blockchain-Enabled Tamper-Proof Logging

This repository contains a Jupyter notebook for an experimental cloud-security intrusion-detection study. The notebook evaluates classical machine learning, deep learning, adversarial robustness, explainability, and blockchain-style audit logging using standard network intrusion detection datasets.

## Project Objective

The main goal is to enhance cloud security by building and evaluating intrusion detection models that can distinguish normal traffic from attacks and support transparent, auditable decision-making. The notebook focuses on:

- Cross-dataset intrusion detection using NSL-KDD, CICIDS2017, and UNSW-NB15.
- Binary and attack-family classification.
- Robustness testing under noisy and adversarial conditions.
- Explainable Learning using SHAP visualizations.
- Deep learning training analysis using accuracy and loss curves.
- Blockchain-style logging for prediction integrity and auditability.
- Final benchmark comparison under a consistent experimental protocol.

## Datasets

The notebook is designed to run on Kaggle and expects the following dataset paths:

```text
/kaggle/input/nsl-kdd/KDDTrain+.txt
/kaggle/input/nsl-kdd/KDDTest+.txt
/kaggle/input/cicids2017
/kaggle/input/unsw-nb15
```

The code automatically searches for CSV/TXT files inside the dataset folders, standardizes column names, detects label columns, and removes redundant identifiers such as IP addresses, timestamps, flow IDs, and record IDs.

## Notebook Structure

The notebook is divided into six phases.

### Phase 1: Cross-Dataset Baseline Evaluation

This phase loads the three datasets, standardizes the labels, derives binary attack labels and attack-family labels, creates stratified train/validation/test splits, and trains a classical machine learning baseline using `HistGradientBoostingClassifier`.

Main outputs:

```text
phase1_cross_dataset_metrics.csv
phase1_attack_family_protocol.csv
```

### Phase 2: Robustness and Explainability

This phase trains a deep learning model and an XGBoost model, then evaluates performance under clean data, Gaussian noise, FGSM attack, and PGD attack. It also generates SHAP-based global and local explanation plots.

Main outputs:

```text
phase2_robustness_table.csv
phase2_shap_global.png
phase2_shap_local.png
phase2_accuracy_under_attacks.png
phase2_gaussian_heatmap.png
phase2_robustness_comparison.png
```

### Phase 3: Deep Learning Training Analysis

This phase trains a neural network model and records the training history across epochs. It tracks training and validation loss and accuracy to show whether the model is learning effectively and whether overfitting occurs.

Main outputs:

```text
phase3_training_log.csv
phase3_learning_curve_accuracy.png
phase3_learning_curve_loss.png
```

### Phase 4: NSL-KDD Detailed Evaluation

This phase focuses on NSL-KDD using its original train/test structure. It evaluates the model using several metrics, including accuracy, precision, recall, F1-score, ROC-AUC, confusion matrix, ROC curve, and a Gaussian-noise baseline comparison.

Main outputs:

```text
phase4_nslkdd_metrics.csv
phase4_metric_relevance_table.csv
phase4_false_alarm_gaussian_baseline.csv
phase4_class_metric_heatmap.png
phase4_confusion_matrix.png
phase4_roc_curve.png
```

### Phase 5: Blockchain-Style Security Logging

This phase simulates a permissioned blockchain-style ledger for storing prediction events. Each block contains prediction information, confidence scores, labels, timestamps, and hashes. The hash chain is used to support integrity, traceability, and tamper-evident audit logging.

Main outputs:

```text
phase5_live_prediction_log.csv
phase5_blockchain_benchmarks.csv
phase5_system_footprint.csv
phase5_monthly_cost.csv
phase5_hash_chain_flow.png
phase5_live_confidence.png
phase5_label_distribution.png
```

### Phase 6: Final Fair Benchmark

This phase performs a final comparison across datasets using a consistent train/validation/test protocol and reports clean and noisy-data performance. It also generates confusion matrices for the modern benchmark datasets.

Main outputs:

```text
phase6_fair_comparison_protocol.csv
phase6_final_benchmark_summary.csv
phase6_modern_confusion_matrices.png
```

## Main Methods Used

The notebook uses the following methods and techniques:

- Data cleaning and column normalization.
- Automatic schema handling for NSL-KDD, CICIDS2017, and UNSW-NB15.
- Attack-family mapping for NSL-KDD attack categories such as DoS, Probe, R2L, and U2R.
- Binary label generation for normal vs. attack traffic.
- Stratified group splitting to reduce data leakage.
- Numerical feature scaling using `StandardScaler`.
- Categorical feature encoding using `OrdinalEncoder`.
- Missing-value handling using `SimpleImputer`.
- Classical machine learning using `HistGradientBoostingClassifier` and `XGBClassifier`.
- Deep learning using PyTorch fully connected neural networks.
- Adversarial testing using Gaussian noise, FGSM, and PGD.
- Explainability using SHAP.
- Blockchain-style hash-chain logging using SHA-256.

## Installation

Create a virtual environment and install the required packages:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

For Windows:

```bash
python -m venv .venv
.venv\\Scripts\\activate
pip install -r requirements.txt
```

## Running the Notebook

1. Upload the notebook to Kaggle or run it locally.
2. Make sure the required datasets are available in the expected paths.
3. Install the packages listed in `requirements.txt`.
4. Run the notebook cells from Phase 1 to Phase 6.
5. Review the generated CSV and PNG files under:

```text
/kaggle/working/results/
```

## Output Folder Structure

```text
results/
├── phase1/
├── phase2/
├── phase3/
├── phase4/
├── phase5/
└── phase6/
```

Each phase creates its own output folder and saves tables, figures, or logs inside it.

## Code Summary for Explanation

The code begins by importing the required libraries, setting random seeds, and defining output folders. It then defines helper functions to load datasets, normalize column names, identify label columns, clean redundant features, and map attacks into binary and family-level categories. After preprocessing, the code separates numerical and categorical features, imputes missing values, scales numerical values, and encodes categorical features.

In the modeling stages, the notebook trains classical and deep learning models for intrusion detection. The classical models provide strong baseline results, while the PyTorch neural network is used for deeper evaluation, robustness testing, and learning-curve analysis. The notebook evaluates the models using accuracy, balanced accuracy, precision, recall, F1-score, ROC-AUC, PR-AUC, and confusion matrices.

The robustness section tests how model performance changes when the input data is modified using Gaussian noise and adversarial attacks such as FGSM and PGD. This is important because intrusion detection systems in cloud environments may face noisy, incomplete, or intentionally manipulated traffic patterns.

The explainability section uses SHAP to show which features contribute most to model predictions. This helps make the intrusion detection system more transparent and supports security analysts in understanding why a sample is classified as normal or malicious.

The blockchain-style logging section simulates a tamper-evident ledger. Each prediction is stored with a timestamp, confidence score, label, previous hash, and current hash. This design helps demonstrate how intrusion detection outputs can be recorded in an auditable way for cloud-security monitoring.

## Notes

- The notebook is mainly configured for Kaggle paths.
- Running all phases may require significant memory and processing time depending on dataset size.
- GPU acceleration is optional but useful for the PyTorch deep learning phases.
- If running locally, update the dataset paths in the `data_sources` dictionaries.
