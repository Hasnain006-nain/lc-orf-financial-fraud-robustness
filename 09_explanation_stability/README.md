# 🔍 Axis 5: Explanation Stability

This module audits the stability of explainable AI (XAI) feature attributions (Tree SHAP and feature importances) across random seeds and temporal splits.

## 📓 Notebook

- **`explanation_stability_colab.ipynb`**: Measures attribution rank correlation (Spearman $\rho$), Top-$K$ Jaccard overlap, and the *Explanation Reliability Gap*.

## 📂 Folder Contents

- **`figures/`**: Generated publication-quality vector PDF figures:
  - `fig07_explanation_reliability_gap.pdf`: Primary visualization demonstrating the gap between stable attribution ranks and predictive degradation.
  - `supp_protocol_explanation_instability_heatmap.pdf`: Protocol-level explanation correlation heatmap.
  - `seed_explanation_stability_top5.pdf`: Top-5 feature attribution stability across random seeds.
  - `top_strict_features_D1.pdf`, `top_strict_features_D2.pdf`, `top_strict_features_D3.pdf`: Dominant feature rankings per dataset.
- **`results/`**: Output data:
  - `table06_explanation_reliability_gap.csv`: Quantified explanation reliability gap metrics.
  - `top_feature_stability_summary.csv`: Summary of top feature stability across protocols.
  - `seed_explanation_stability_summary.csv`: Multiseed stability metrics.
  - `checkpoints/`: Seed-level metric and importance checkpoint CSVs.

## 🎯 Key Findings

- **The Explanation Reliability Gap:** Explanation rankings can remain stable while predictive behavior shifts, especially on D2. High attribution rank alignment indicates that explanation stability does not guarantee preservation of operational classification performance under temporal distribution change.
