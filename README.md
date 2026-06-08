# Network Intrusion Detection System

Builds a network intrusion detection system (NIDS) that classifies network connections as normal or one of several attack types. Multiple classifiers are compared, including Decision Tree, Random Forest, AdaBoost, XGBoost, Gradient Boosting, and HistGradientBoosting, with evaluation via accuracy, precision, recall, F1-score, and confusion matrices.

## Dataset

[KDD Cup 1999](http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html) dataset (`KDDCup Data 10 Percent.csv`) -- a widely used benchmark for network intrusion detection research. Supporting files include `kddcup.txt` (column names) and `training_attack_types.txt` (attack type mappings).

## Tech Stack

- Pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn (Decision Tree, Random Forest, AdaBoost, Gradient Boosting, HistGradientBoosting, StandardScaler, LabelEncoder, GridSearchCV)
- XGBoost