# Cyber Anomaly Detection – Course Project

**Track:** Applicative (Cyber)  
**Task:** Binary classification of network packets (positive = `anomaly`).  
**Main metric:** F1 for the positive class (anomaly).  
**CV:** Stratified 5-fold.

## Dataset
- **Source (Kaggle):** https://www.kaggle.com/datasets/maksimkaliaev/assignment-1-supervised-learning-flow-csecurity/data  
- **Included in this repo:** `packets_train.csv`, `packets_test.csv` (for easy grading).

## What we did (short)
- **EDA:** label balance, packet length, TTL, protocol patterns (with `hue=label`), correlation heatmap.
- **Feature engineering:** `hour` (from timestamp), `tcp_flag_sum` (SYN+ACK+FIN), `syn_only`, `len_ttl_ratio`.
- **Models & search:** Logistic Regression, Random Forest, Gradient Boosting with `GridSearchCV` (Stratified 5-fold, scoring = F1).
- **Imbalance handling:** `class_weight` in sklearn models (no `imblearn`).
- **Explainability:** feature importances / coefficients.
- **Applicative checks:** simple TTP groups (SYN_only, FIN_scan, Low_TTL).  
  _Note: TTP groups with zero samples (or no positive predictions) may be skipped._

## Best pipeline (from CV)
**Logistic Regression + StandardScaler** (`C=1`, `class_weight='balanced'`).  
A full CV summary table of all parameter combinations (from `cv_results_`) appears in Part 3.

## Final test results (this run)
- **F1 (positive = anomaly): 0.035**  
- **Confusion Matrix:** **TN=2005, FP=388, FN=0, TP=7**  
- **TTP F1:** `SYN_only ≈ 0.122`, `FIN_scan = 0.000`

## How to run
```bash
pip install -r requirements.txt
# open the notebook (Assignment_cyber_anomaly_detection_flow.ipynb) and Run all
