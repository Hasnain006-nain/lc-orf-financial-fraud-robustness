# Results, Tables, and Figures Map

Every manuscript claim must map to a saved CSV and, where needed, a saved figure.

## Main Tables

### Table 1: Dataset Audit and Feature Governance

Purpose:

- Show D1/D2/D3 row counts, fraud rates, duplicates/missingness, label column, time field, and excluded leakage/identifier fields.

Source files:

- `01_dataset_truth_audit/dataset_audit_summary.csv`
- `02_feature_governance/feature_governance_table.csv`
- `02_feature_governance/feature_set_definitions.csv`

Key values:

- D1: `284,807` rows, `492` fraud rows before duplicate removal, fraud rate `0.173%`, `1,081` duplicate rows.
- D2: `555,719` rows, `2,145` fraud rows, fraud rate `0.386%`.
- D3: `5,840,046` rows, `4,497` fraud rows, fraud rate `0.077%`, one unknown-label row.

### Table 2: Leakage Inflation Summary

Purpose:

- Show AP and MCC inflation under unsafe scenarios.

Source file:

- `03_leakage_stress_testing/received_multiseed_results_20260924/leakage_stress_multiseed_v1/results/leakage_inflation_multiseed_summary.csv`

Key values:

- D1 unsafe SMOTE AP inflation: `0.140` to `0.142`.
- D2 unsafe SMOTE AP inflation: `0.050` to `0.082`.
- D2 unsafe SMOTE MCC inflation: `0.361` to `0.472`.
- D3 ledger-state AP inflation: `0.017` to `0.022`.

### Table 3: Temporal Robustness Summary

Purpose:

- Show random versus chronological AP/MCC and Temporal Robustness Drop.

Source file:

- `06_temporal_robustness/received_results_20260924/06_temporal_robustness/temporal_robustness_v1/results/temporal_robustness_summary.csv`

Key values:

- D2 LightGBM AP: `0.931` random to `0.686` chronological.
- D2 XGBoost AP: `0.891` random to `0.614` chronological.
- D3 temporal result is limited or mixed.

### Table 4: Prevalence Sensitivity Summary

Purpose:

- Show precision range, MCC range, and cost range across target fraud rates.

Source file:

- `07_prevalence_stress_test/received_results_20260924/07_prevalence_stress_test/prevalence_stress_v1/results/prevalence_sensitivity_summary.csv`

Key values:

- Precision range: up to `0.592`.
- D1 cost range: `1436` to `1793` per 10,000.
- D3 cost range: `878` to `955` per 10,000.

### Table 5: Calibration/Recalibration Summary

Purpose:

- Show raw, Platt, and isotonic calibration metrics.

Source file:

- `08_calibration_recalibration/received_results_20260924/08_calibration_recalibration/calibration_recalibration_v1/results/calibration_recalibration_summary.csv`

Key values:

- Isotonic recalibration produced the best Brier score and best ECE for all six dataset/model pairs.
- Cost improvement was mixed and should not be overclaimed.

### Table 6: Explanation Stability Summary

Purpose:

- Show protocol-level Top-5 Jaccard and Explanation Instability Index.

Source file:

- `09_explanation_stability/received_results_20260924/09_explanation_stability/explanation_stability_v1/results/protocol_explanation_stability_summary.csv`

Key values:

- D2/D3 protocol Top-5 Jaccard: `1.000`.
- D1 LightGBM protocol instability: `0.524`.
- D1 XGBoost protocol instability: `0.248`.

## Main Figures

### Figure 1: LC-ORF Pipeline Diagram

Create during manuscript rewrite.

Content:

- Dataset audit -> feature governance -> strict protocol -> stress-test modules -> claim-bounded interpretation.

### Figure 2: Leakage Inflation Heatmap

Use:

- `03_leakage_stress_testing/.../figures/multiseed_ap_leakage_inflation_heatmap.png`

Caption should emphasize unsafe evaluation inflation.

### Figure 3: Temporal Robustness Drop

Use:

- `06_temporal_robustness/.../figures/temporal_ap_drop_by_dataset.png`
- or `temporal_ap_drop_heatmap.png`

Caption should emphasize D2 as strongest temporal evidence.

### Figure 4: Prevalence Sensitivity Curve

Use:

- `07_prevalence_stress_test/.../figures/prevalence_precision_curve.png`
- or `prevalence_cost_curve.png`

Caption should explain that model and threshold are fixed while test prevalence changes.

### Figure 5: Calibration Improvement

Use:

- `08_calibration_recalibration/.../figures/calibration_brier_reduction_by_dataset.png`
- `calibration_ece_reduction_by_dataset.png`

Caption should separate probability-quality improvement from cost improvement.

### Figure 6: Explanation Instability Heatmap

Use:

- `09_explanation_stability/.../figures/protocol_explanation_instability_heatmap.png`

Caption should state that D2/D3 are stable while D1 is protocol-sensitive.

## Supplemental Tables

Move these to appendix/supplement if space is tight:

- Full per-seed leakage results.
- Full prevalence by-target-prevalence table.
- Full calibration curve bins.
- Full feature ranking table.
- Runtime/checkpoint summaries.

## Result Story Order

Use this exact order:

1. Governance explains what is allowed.
2. Leakage test shows why governance matters.
3. Temporal test shows random splits can be optimistic.
4. Prevalence test shows operating environment matters.
5. Calibration test shows probability quality matters.
6. Explanation stability test shows interpretability claims need stability checks.

