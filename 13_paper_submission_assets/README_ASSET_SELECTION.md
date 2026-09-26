# Paper And Supplementary Asset Selection

## Folder Structure

- `01_main_paper_assets`: figures and table sources recommended for the main IEEE Access manuscript.
- `02_supplementary_assets`: supporting figures and source result files that can be cited as supplementary material or used for appendix tables.

## Main Figures Selected

1. `fig01_lcorf_framework_workflow`: Defines the LC-ORF workflow. Use early in the method section because the paper's novelty is the audit framework, not a new classifier.
2. `fig02_lcorf_final_audit_profile_heatmap`: Main evidence map across leakage, temporal, prevalence, calibration, explanation, and alert-budget axes. This is the strongest single figure.
3. `fig03_multiseed_ap_leakage_inflation_heatmap`: Shows leakage inflation under unsafe protocols. Use to justify why leakage control is central.
4. `fig04_d2_drift_vs_temporal_drop`: Connects D2 chronological drift with predictive degradation. Use to defend the temporal robustness section.
5. `fig05_prevalence_profile_heatmap`: Shows prevalence sensitivity. Use because fraud prevalence shift is operationally important.
6. `fig06_alert_budget_precision_by_axis_dataset`: Shows alert workload behavior under operational budgets. Use to avoid a purely metric-only paper.
7. `fig07_explanation_reliability_gap`: Shows artifact-level explanation reliability gap. Use with cautious wording only.

## Main Tables Selected

1. `table01_lcorf_audit_axes.csv`: Defines each LC-ORF axis, evidence, and claim boundary.
2. `table02_final_profile_axis_summary.csv`: Summarizes final audit-profile coverage.
3. `table03_key_bootstrap_findings.csv`: Gives representative bootstrap-backed deltas.
4. `table04_d2_temporal_drift_features.csv`: Supports the D2 temporal drift argument.
5. `table05_d2_temporal_prevalence_by_split.csv`: Shows chronological fraud-rate shift in D2.
6. `table06_explanation_reliability_gap.csv`: Supports the explanation reliability gap claim.
7. `table07_alert_budget_compact_summary.csv`: Compact operational alert-budget table.
8. `table08_prevalence_profile_component.csv`: Source table for prevalence fragility discussion.
9. `table09_related_work_matrix.csv`: Shows the literature gap: prior work covers fraud, leakage, drift, calibration, explanations, and cost-sensitive evaluation mostly as separate strands, while LC-ORF combines them into a unified audit profile.
10. `table10_lcorf_notation.csv`: Defines the formal notation used in the LC-ORF methodology.
11. `table11_lcorf_material_thresholds.csv`: Lists the metric-specific materiality thresholds used for robust, fragile, and inconclusive labels.

## Methodology Notes

- `lcorf_methodology_formalization.md`: Human-readable formal method definition.
- `lcorf_methodology_latex_snippet.tex`: LaTeX-ready starting text for the manuscript methodology section.

## Claim Boundaries

- Do not claim state-of-the-art fraud detection.
- Do not claim a new fraud classifier.
- Do not claim causal explanation validation.
- Do not hide mixed findings; robust, fragile, and inconclusive outcomes all support the audit-framework contribution.
- Treat `explanation_reliability_gap` as an artifact-level operational proxy.
