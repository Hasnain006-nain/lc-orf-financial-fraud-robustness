# 📉 Axis 3: Prevalence Stress Testing

This module evaluates model sensitivity to non-stationary fraud base rates using controlled downsampling across multiple prevalence tiers.

## 📓 Notebook

- **`prevalence_stress_colab.ipynb`**: Conducts deterministic downsampling across 6 target fraud prevalence ratios ($\pi \in \{0.0001 \dots 0.05\}$).

## 📂 Folder Contents

- **`figures/`**: Generated publication-quality vector PDF figures:
  - `fig05_prevalence_profile_heatmap.pdf`: Primary audit heatmap across prevalence shift conditions.
  - `supp_prevalence_precision_curve.pdf`: Precision decay curves across downsampled base rates.
  - `supp_prevalence_profile_heatmap.pdf`: Full prevalence profile heatmap.
  - `prevalence_cost_sensitivity_heatmap.pdf`: Operating cost variations under base-rate shifts.
  - `prevalence_cost_curve.pdf`: Financial loss curve.
  - `prevalence_mcc_curve.pdf`: MCC stability curves.
  - `prevalence_precision_curve.pdf`: Alert precision curves.
- **`results/`**: Output data:
  - `table08_prevalence_profile_component.csv`: Component-by-component fragility labels.
  - `prevalence_profile_per_target.csv`: Per-target prevalence performance records.
  - `checkpoints/`: Seed and ratio checkpoint CSVs.

## 🎯 Key Findings

- **High Operational Fragility:** **29 out of 36** evaluated prevalence-profile components were labeled operationally **Fragile**, indicating extreme vulnerability to base-rate fluctuations in production streams.
