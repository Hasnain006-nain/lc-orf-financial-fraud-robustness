# ⏳ Axis 2: Temporal Robustness

This module investigates model degradation when transitioning from standard random stratified splitting to chronological sequential evaluation.

## 📓 Notebook

- **`temporal_robustness_colab.ipynb`**: Evaluates temporal stability across datasets, measuring chronological performance drops and feature distribution drift.

## 📂 Folder Contents

- **`figures/`**: Generated high-resolution figures (PNG at 600 DPI and vector PDF):
  - `fig04_d2_drift_vs_temporal_drop.png` / `.pdf`: Primary visualization connecting D2 feature drift with chronological performance drop.
  - `temporal_ap_drop_heatmap.png` / `.pdf`: Cross-dataset AP degradation heatmap.
  - `temporal_ap_drop_by_dataset.png`: AP reduction across datasets.
  - `temporal_cost_delta_by_dataset.png`: Financial operating cost impacts.
  - `temporal_mcc_drop_by_dataset.png`: MCC performance degradation.
- **`results/`**: Output data and diagnostics:
  - `d2_temporal_drift_diagnostics.csv`: Population stability index (PSI) and Wasserstein feature drift metrics.
  - `d2_temporal_drop_summary.csv`: Summary of performance drop under chronological testing.
  - `d2_temporal_prevalence_by_split.csv`: Base-rate variations across temporal partitions.
  - `temporal_robustness_results.csv`: Complete evaluation run results.
  - `checkpoints/`: Seed-level evaluation checkpoint CSVs.

## 🎯 Key Findings

- **Chronological Degradation:** On D2, moving to chronological evaluation reduced Average Precision by **-0.277** for XGBoost and **-0.245** for LightGBM.
- **Hidden Drift:** Random stratified splits hide significant temporal feature drift that surfaces immediately in chronological validation.
