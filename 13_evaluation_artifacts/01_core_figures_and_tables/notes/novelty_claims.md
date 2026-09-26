# LC-ORF Novelty Claims

## Working Title

LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection

## One-Sentence Contribution

This paper introduces LC-ORF, a leakage-controlled operational robustness framework that audits financial fraud detection models across leakage inflation, temporal degradation, prevalence shift, calibration behavior, explanation reliability, and alert-budget constraints.

## What Is New

The novelty is not a new classifier. The novelty is the framework-level audit protocol and the final operational profile that joins several failure modes usually studied separately.

LC-ORF contributes:

1. A unified audit structure for fraud-detection evaluation under multiple operational assumptions.
2. A leakage-controlled experimental protocol that separates strict evaluation from unsafe or assumption-shifted evaluation.
3. A final audit profile that reports metric deltas, uncertainty intervals, alert-budget behavior, and explanation-reliability evidence.
4. A multi-dataset empirical study across `D1_creditcard`, `D2_fraudTest`, and `D3_PaySim` using LightGBM and XGBoost over five random seeds.
5. An artifact-level explanation reliability gap that compares explanation-rank stability against predictive degradation under protocol shift.

## Evidence Behind The Claim

Primary source files:

- `table01_lcorf_audit_axes.csv`
- `table02_final_profile_axis_summary.csv`
- `table03_key_bootstrap_findings.csv`
- `table04_d2_temporal_drift_features.csv`
- `table05_d2_temporal_prevalence_by_split.csv`
- `table06_explanation_reliability_gap.csv`
- `table07_alert_budget_compact_summary.csv`
- `table08_prevalence_profile_component.csv`

Primary figures:

- `fig01_lcorf_framework_workflow`
- `fig02_lcorf_final_audit_profile_heatmap`
- `fig03_multiseed_ap_leakage_inflation_heatmap`
- `fig04_d2_drift_vs_temporal_drop`
- `fig05_prevalence_profile_heatmap`
- `fig06_alert_budget_precision_by_axis_dataset`
- `fig07_explanation_reliability_gap`

## Main Paper Claim

LC-ORF shows that fraud-detection performance can change materially when evaluation assumptions change. The framework makes these changes measurable through a structured profile rather than treating model scores, calibration, explanations, and alert budgets as separate analyses.

## Claims We Can Defend

- Unsafe preprocessing can inflate apparent fraud-detection performance.
- Chronological evaluation can expose degradation that random stratified splits hide.
- Fraud-prevalence shifts can materially change precision, MCC, and operating cost.
- Calibration can improve probability quality while not necessarily improving every operational metric.
- Explanation rankings can appear stable even when predictive behavior shifts, which motivates reporting explanation reliability together with predictive deltas.
- Alert-budget evaluation adds operational meaning beyond aggregate AUC or average precision.

## Claims We Must Not Make

- LC-ORF is not a new fraud classifier.
- LC-ORF does not prove state-of-the-art fraud detection performance.
- LC-ORF does not prove universal robustness across all financial institutions.
- The explanation reliability gap is not causal explanation validation.
- The three datasets are not enough to claim universal deployment behavior.
- The alert-budget analysis is not a full fraud-operations optimization policy.

## Reviewer-Facing Novelty Framing

The contribution should be framed as follows:

Fraud-detection papers often report model performance under a narrow evaluation design. LC-ORF instead asks how much of that performance remains when key operational assumptions are changed. The framework measures leakage sensitivity, temporal degradation, prevalence sensitivity, calibration effects, explanation reliability, and alert-budget behavior in one auditable profile.

## Short Abstract Sentence

Rather than proposing another classifier, LC-ORF provides a structured audit protocol for measuring how fraud-detection models behave when the assumptions behind their evaluation are changed.

## Introduction Contribution Bullets

- We propose LC-ORF, a leakage-controlled operational robustness framework for auditing fraud-detection models across six operational axes.
- We instantiate LC-ORF on three fraud datasets and two tree-based ensemble families over five seeds, using bootstrap intervals and alert-budget summaries to separate robust, fragile, and inconclusive findings.
- We report a final audit profile that connects leakage inflation, temporal degradation, prevalence sensitivity, calibration behavior, explanation reliability, and operational alert constraints.

## Discussion Framing

The important result is not that one model wins. The important result is that model behavior changes differently under different operational assumptions. LC-ORF provides a way to make those changes visible, reproducible, and easier to discuss before deployment.
