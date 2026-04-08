# Fraud Detection Model Evaluation — Metrics that Matter

## Objective
Evaluated a logistic regression fraud detector on a severely imbalanced real-world dataset, demonstrating why accuracy is a misleading metric for rare-event classification and how threshold selection can be aligned to operational business constraints.

## Methodology
- **Dataset:** Kaggle Credit Card Fraud Detection — 284,807 European credit card transactions with PCA-anonymized features (V1–V28), transaction amount, and a binary fraud label (0.172% positive class)
- **Baseline audit:** Established the accuracy paradox — a naive all-negative classifier achieves 99.83% accuracy while detecting zero fraud cases
- **Model:** Trained a logistic regression classifier using scikit-learn; evaluated beyond accuracy using confusion matrices, precision, recall, F1-score, ROC-AUC, and PR-AUC
- **Threshold analysis:** Identified the F1-optimal decision threshold, showing it diverges substantially from the default 0.5 cutoff
- **Capacity-constrained operating point:** Applied a business rule (max 500 daily investigations) to select a threshold that maximizes recall within operational limits

## Key Findings
- Default accuracy metrics are actively misleading under severe class imbalance — a model predicting no fraud achieves 99.83% accuracy with zero utility
- Logistic regression achieved strong ROC-AUC and meaningful PR-AUC on the fraud class, confirming the model's discriminative power despite imbalance
- The F1-optimal threshold differs significantly from 0.5, underscoring that threshold selection is a business decision, not a modeling default
- At the capacity-constrained threshold (τ = 0.01), the model flags 246 transactions per day, recovers 88.78% of fraud cases, and operates well within the 500-investigation budget — a practically deployable operating point
