# 🧪 Axis 1: Leakage Stress Testing

This module evaluates the empirical impact of evaluation protocol leakage across the benchmark datasets using LightGBM and XGBoost.

## 📓 Notebooks

- **`leakage_stress_multiseed_colab.ipynb`** *(Recommended)*: Complete 5-seed evaluation (`42, 101, 202, 303, 404`) across all three datasets and leakage scenarios with prediction artifact exports.
- **`leakage_stress_testing_colab.ipynb`**: Initial single-seed reference test.

## 📂 Folder Contents

- **`figures/`**: Generated publication-quality vector PDF figures:
  - `fig03_multiseed_ap_leakage_inflation_heatmap.pdf`: Primary audit heatmap demonstrating AP inflation under unsafe SMOTE.
  - `multiseed_cost_delta_per_10k_by_dataset.pdf`: Operating cost distortions per 10k transactions.
  - `multiseed_lii_average_precision_by_dataset.pdf`: Leakage Inflation Index (LII) across models.
  - `multiseed_lii_mcc_by_dataset.pdf`: MCC inflation across seeds.
- **`results/`**: Output metrics and checkpoints:
  - `table03_key_bootstrap_findings.csv`: Key 1,000-replicate paired bootstrap significance deltas.
  - `partial_metrics_latest.csv`: Latest consolidated metrics.
  - `checkpoints/`: Seed-by-seed intermediate checkpoint CSV files.

## 🎯 Key Findings

- **D2 (fraudTest):** Unsafe SMOTE-before-split artificially inflated MCC by **+0.472** (XGBoost) and **+0.361** (LightGBM).
- **D1 (creditcard):** Artificially inflated MCC by **+0.357** (XGBoost) and **+0.320** (LightGBM).
- **D3 (PaySim):** Post-transaction balance access inflated MCC by **+0.129** (XGBoost).
