# Benchmark and Evaluation Artifact Selection

## Folder Structure

- `01_core_figures_and_tables`: primary benchmark figures and table sources for the LC-ORF evaluation framework.
- `02_extended_results_and_data`: supporting figures and source result files that provide complete bootstrap records, prediction manifests, and extended evaluation curves.

## Core Figures

1. `fig01_lcorf_framework_workflow`: Defines the LC-ORF workflow. Illustrated early in the methodology because the core contribution is the audit framework.
2. `fig02_lcorf_final_audit_profile_heatmap`: Comprehensive evidence map across leakage, temporal, prevalence, calibration, explanation, and alert-budget axes.
3. `fig03_multiseed_ap_leakage_inflation_heatmap`: Shows leakage inflation under unsafe protocols (e.g. SMOTE-before-split).
4. `fig04_d2_drift_vs_temporal_drop`: Connects D2 chronological drift with predictive degradation.
5. `fig05_prevalence_profile_heatmap`: Demonstrates prevalence sensitivity across base rates.
6. `fig06_alert_budget_precision_by_axis_dataset`: Displays alert workload behavior under operational review budgets.
7. `fig07_explanation_reliability_gap`: Shows the artifact-level explanation reliability gap.

## Core Tables

1. `table01_lcorf_audit_axes.csv`: Defines each LC-ORF axis, evidence, and claim boundary.
2. `table02_final_profile_axis_summary.csv`: Summarizes final audit-profile coverage.
3. `table03_key_bootstrap_findings.csv`: Gives representative bootstrap-backed deltas.
4. `table04_d2_temporal_drift_features.csv`: Supports the D2 temporal drift analysis.
5. `table05_d2_temporal_prevalence_by_split.csv`: Shows chronological fraud-rate shift in D2.
6. `table06_explanation_reliability_gap.csv`: Supports the explanation reliability gap analysis.
7. `table07_alert_budget_compact_summary.csv`: Compact operational alert-budget table.
8. `table08_prevalence_profile_component.csv`: Source table for prevalence fragility discussion.
9. `table09_related_work_matrix.csv`: Shows the literature gap matrix across operational fraud evaluation dimensions.
10. `table10_lcorf_notation.csv`: Defines the formal notation used in the LC-ORF methodology.
11. `table11_lcorf_material_thresholds.csv`: Lists metric-specific materiality thresholds.

## Methodology Notes

- `lcorf_methodology_formalization.md`: Human-readable formal method definition.

## Claim Boundaries

- Do not claim state-of-the-art fraud detection.
- Do not claim a new fraud classifier.
- Do not claim causal explanation validation.
- Report robust, fragile, and inconclusive outcomes with equal scientific weight.
- Treat `explanation_reliability_gap` as an artifact-level operational proxy.
