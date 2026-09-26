# 📉 Axis 3: Prevalence Stress Testing

This module evaluates model sensitivity to non-stationary fraud base rates using controlled downsampling across multiple prevalence tiers.

## 📓 Notebook

- **`prevalence_stress_colab.ipynb`**: Conducts deterministic downsampling across 6 target fraud prevalence ratios ($\pi \in \{0.0001 \dots 0.05\}$).

## 📂 Folder Contents

- **`figures/`**: Generated figures (PNG at 600 DPI and vector PDF):
  - `fig05_prevalence_profile_heatmap.png` / `.pdf`: Primary audit heatmap across prevalence shift conditions.
  - `supp_prevalence_precision_curve.png` / `.pdf`: Precision decay curves across downsampled base rates.
  - `prevalence_cost_sensitivity_heatmap.png`: Operating cost variations under base-rate shifts.
  - `prevalence_mcc_curve.png`: MCC stability curves.
- **`results/`**: Output data:
  - `table08_prevalence_profile_component.csv`: Component-by-component fragility labels.
  - `prevalence_profile_per_target.csv`: Per-target prevalence performance records.
  - `checkpoints/`: Seed and ratio checkpoint CSVs.

## 🎯 Key Findings

- **High Operational Fragility:** **29 out of 36** evaluated prevalence-profile components were labeled operationally **Fragile**, indicating extreme vulnerability to base-rate fluctuations in production streams.
