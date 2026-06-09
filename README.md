# 🛡️ Network Intrusion Detection System (NIDS)

A machine learning-based system that classifies network traffic as **normal or malicious**, comparing the performance of seven supervised learning algorithms on a real-world cybersecurity benchmark dataset.

---

## 📌 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Tech Stack](#tech-stack)
- [Results](#results)
- [Key Findings](#key-findings)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Future Improvements](#future-improvements)

---

## Overview

Network Intrusion Detection Systems (NIDS) are a critical layer of defense in modern cybersecurity infrastructure. They monitor network traffic and flag suspicious connections that may indicate attacks such as DoS, probing, or unauthorized remote access.

This project builds a multi-class classifier that identifies whether a network connection is **normal** or one of several known attack types. Seven ML models are trained, tuned, and compared using standard classification metrics to determine the best-performing approach.

---

## Dataset

**[KDD Cup 1999](http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html)** — a widely-used benchmark in network intrusion detection research.

- **Source file:** `KDDCup Data 10 Percent.csv` (10% stratified sample of the full dataset)
- **Size:** ~494,000 connection records
- **Features:** 41 features per connection (protocol type, service, flag, byte counts, etc.)
- **Labels:** 1 normal class + 4 attack categories (DoS, Probe, R2L, U2R), further broken down into ~22 specific attack subtypes

Supporting files:

- `kddcup.txt` — column names and feature descriptions
- `training_attack_types.txt` — mapping of attack subtypes to their parent categories

> ⚠️ **Note:** The KDD Cup 1999 dataset is a well-known academic benchmark. While it remains useful for learning and prototyping, it does not reflect the complexity of modern network traffic. Real-world deployment would require a contemporary dataset such as [CICIDS2017](https://www.unb.ca/cic/datasets/ids-2017.html).

---

## Methodology

The project follows a standard ML pipeline:

**1. Data Preprocessing**

- Column assignment using `kddcup.txt`
- Label encoding of categorical features (`protocol_type`, `service`, `flag`)
- Attack subtype mapping to parent categories via `training_attack_types.txt`
- Feature scaling with `StandardScaler`

**2. Exploratory Data Analysis**

- Class distribution analysis
- Feature correlation heatmaps using Seaborn
- Visualizations of attack type frequencies

**3. Model Training & Hyperparameter Tuning**

- Seven classifiers trained and evaluated
- `GridSearchCV` used for hyperparameter optimization on select models

**4. Evaluation**
Each model was evaluated on:

- Accuracy
- Precision, Recall, F1-Score (weighted)
- Confusion Matrix

---

## Tech Stack

| Category | Libraries |
|---|---|
| Data Manipulation | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn` |
| Machine Learning | `scikit-learn`, `xgboost` |
| Preprocessing | `StandardScaler`, `LabelEncoder` |
| Tuning | `GridSearchCV` |
| Environment | `jupyter` |

---

## Results

| Model | Accuracy |
|---|---|
| ✅ **Random Forest** | **99.76%** |
| Decision Tree | 99.59% |
| K-Nearest Neighbors | 99.41% |
| XGBoost | 99.39% |
| AdaBoost | 94.54% |
| Hist Gradient Boosting | 93.10% |
| Gradient Boosting | 92.86% |

---

## Key Findings

- **Random Forest** achieved the highest accuracy (99.76%), likely due to its ensemble nature reducing variance on this structured tabular dataset.
- **Tree-based models** (Decision Tree, Random Forest, XGBoost) significantly outperformed boosting approaches (AdaBoost, Gradient Boosting) on this benchmark.
- **KNN** performed surprisingly well (99.41%), suggesting the feature space is highly clustered by class after scaling.
- **Boosting methods** showed lower accuracy — possibly due to the heavy class imbalance in the KDD Cup dataset, which can cause boosting algorithms to overfit to the majority class without specific handling.

---

## Project Structure

```
Network-Intrusion-Detection-System/
│
├── NIDS.ipynb                     # Main notebook: EDA, training, evaluation
├── KDDCup Data 10 Percent.csv     # Training dataset (10% sample)
├── Workshop Dataset.csv           # Additional dataset used during analysis
├── kddcup.txt                     # Feature/column name definitions
├── training_attack_types.txt      # Attack subtype → category mapping
├── requirements.txt               # Python dependencies
└── README.md
```

---

## Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook

### Installation

```bash
# Clone the repository
git clone https://github.com/periwalkeshav/Network-Intrusion-Detection-System.git
cd Network-Intrusion-Detection-System

# Install dependencies
pip install -r requirements.txt
```

### Running the Notebook

```bash
jupyter notebook NIDS.ipynb
```

Make sure `KDDCup Data 10 Percent.csv`, `kddcup.txt`, and `training_attack_types.txt` are in the same directory as the notebook before running.

---

## Future Improvements

- [ ] Evaluate on a modern dataset (e.g., CICIDS2017, UNSW-NB15) for more realistic benchmarking
- [ ] Address class imbalance using SMOTE or class-weighted loss functions
- [ ] Add deep learning baseline (LSTM or 1D CNN) for sequential traffic analysis
- [ ] Build a real-time inference pipeline using a trained model artifact
- [ ] Perform feature importance analysis to identify the most predictive network attributes
