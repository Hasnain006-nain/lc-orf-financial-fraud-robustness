# 🎯 Axis 4: Calibration & Recalibration

This module audits probability score reliability using calibration metrics and post-hoc recalibration techniques (Platt Scaling and Isotonic Regression).

## 📓 Notebook

- **`calibration_recalibration_colab.ipynb`**: Evaluates probability calibration, Expected Calibration Error (ECE), Brier score, and expected operating costs.

## 📂 Folder Contents

- **`figures/`**: Generated publication-quality vector PDF figures:
  - `supp_calibration_brier_reduction_by_dataset.pdf`: Brier score improvements via recalibration.
  - `supp_calibration_ece_reduction_by_dataset.pdf`: ECE reduction across datasets.
  - `calibration_curve_D1.pdf`, `calibration_curve_D2.pdf`, `calibration_curve_D3.pdf`: Reliability diagrams before and after recalibration.
  - `calibration_cost_delta_by_dataset.pdf`: Operating cost variations.
- **`results/`**: Output data:
  - Metric CSVs with raw vs. recalibrated Brier score and ECE.
  - `checkpoints/`: Seed-level calibration checkpoint CSVs.

## 🎯 Key Findings

- **Calibration vs. Cost Decoupling:** While post-hoc recalibration substantially reduced ECE and Brier score, it did not automatically reduce operating cost without deliberate decision threshold realignment.
