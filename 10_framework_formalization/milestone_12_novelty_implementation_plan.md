# Milestone 12 Novelty Upgrade Implementation Plan

> **For agentic workers:** Execute this plan task-by-task with a verification checkpoint after every experiment. Do not rewrite the manuscript around results that have not been generated and audited.

**Goal:** Upgrade LC-ORF from a multi-test evaluation framework into a counterfactual, uncertainty-aware, decision-oriented audit protocol whose novelty is supported by new evidence rather than wording alone.

**Architecture:** Preserve the existing strict feature-governance pipeline and five stress modules. Add three evidence layers: paired counterfactual deltas with bootstrap confidence intervals, fixed-alert-budget operational metrics, and drift/explanation-reliability diagnostics. Report the result as a multidimensional audit profile, not an arbitrary weighted score.

**Tech Stack:** Google Colab, Python, pandas, NumPy, scikit-learn, LightGBM, XGBoost, matplotlib, seaborn, SciPy, Google Drive checkpointing, IEEE Access LaTeX.

## Global Constraints

- The strict protocol remains the primary result; unsafe scenarios are stress tests only.
- Every scenario changes one evaluation assumption at a time.
- All preprocessing, resampling, threshold selection, calibration, and drift reference statistics are fitted only on permitted training or validation data.
- The five existing random seeds remain fixed: 42, 101, 202, 303, and 404.
- No arbitrary composite robustness score will be introduced.
- Every displayed number must trace to a saved CSV artifact and a reproducible notebook cell.
- D1 pseudo-temporal evidence and D3 synthetic-data evidence must remain explicitly bounded in the claims.
- No claim may say that LC-ORF is universally novel or guarantees deployment performance.

---

### Task 1: Freeze the novelty specification before new runs

**Files:**
- Create: `Credit__\10_framework_formalization\novelty_specification_v1.md`
- Modify: `Credit__\10_framework_formalization\IEEE_ACCESS_FRAMEWORK_FORMALIZATION.md`

**Produces:** A one-page specification defining the proposed contribution as a counterfactual operational audit and listing the exact outputs required for every dataset/model pair.

- [x] Write the central contribution statement:

```text
LC-ORF is a counterfactual operational audit protocol. It perturbs one deployment assumption at a time, quantifies the resulting metric delta with uncertainty, and records the predictive, probabilistic, operational, and explanation-level consequence in a traceable audit profile.
```

- [x] Define the audit record fields: `dataset`, `model`, `reference_scenario`, `perturbed_scenario`, `changed_assumption`, `metric`, `delta`, `ci_low`, `ci_high`, `operational_delta`, `interpretation`, and `artifact_id`.
- [x] Define the three interpretation labels before running experiments: `robust` when the interval contains only practically negligible change, `fragile` when the interval excludes zero and the change is practically material, and `inconclusive` when the interval is wide or crosses the decision boundary.
- [x] Do not choose numerical practical-effect thresholds after viewing results. Store the chosen thresholds in the specification file before running the new notebooks.

**Verification:** The specification contains no unfinished placeholders, no unbounded novelty claim, and defines every output column used by later tasks.

### Task 2: Build the paired-bootstrap uncertainty layer

**Files:**
- Create: `Credit__\10_framework_formalization\notebooks\10_paired_bootstrap_uncertainty.ipynb`
- Create: `Credit__\10_framework_formalization\results\paired_bootstrap_delta_summary.csv`
- Create: `Credit__\10_framework_formalization\results\paired_bootstrap_delta_per_seed.csv`

**Consumes:** Existing checkpointed predictions and labels from milestones 03, 06, 07, 08, and 09.

**Produces:** 95% percentile bootstrap intervals for every major stress delta.

- [ ] Load saved predictions without retraining whenever the existing artifacts contain the required labels and scores.
- [ ] Use stratified resampling within each class for binary test labels. Use the same bootstrap index for the reference and perturbed predictions so each delta is paired.
- [ ] Run 1,000 bootstrap replicates per dataset/model/scenario/metric/seed.
- [ ] Compute the following paired deltas:

```python
delta_b = metric(y_boot, score_perturbed_boot) - metric(y_boot, score_reference_boot)
ci_low, ci_high = np.percentile(delta_samples, [2.5, 97.5])
```

- [ ] Save `mean_delta`, `std_delta`, `ci_low`, `ci_high`, and `n_bootstrap` for AP, MCC, precision, recall, Brier score, ECE, and cost wherever the source artifact supports the metric.
- [ ] Repeat the calculation for each of the five seeds before aggregating across seeds.

**Verification:** Every summary row has 1,000 bootstrap samples, no missing interval bounds, and the sign of the reported delta matches the existing stress-index definition.

### Task 3: Add fixed-alert-budget operational evaluation

**Files:**
- Create: `Credit__\10_framework_formalization\notebooks\11_alert_budget_evaluation.ipynb`
- Create: `Credit__\10_framework_formalization\results\alert_budget_summary.csv`
- Create: `Credit__\10_framework_formalization\results\alert_budget_per_seed.csv`
- Create: `Credit__\10_framework_formalization\figures\alert_budget_curves.png`

**Consumes:** Strict and stress-test prediction checkpoints from the existing milestones.

**Produces:** Precision, recall, false-alert count, and transparent cost at fixed review capacities.

- [ ] Evaluate fixed alert budgets of 100, 500, and 1,000 alerts per 10,000 transactions, plus a normalized top-1% budget when the test stream supports it.
- [ ] Rank transactions by the frozen model score and select the top budget count without tuning on test labels.
- [ ] Report precision-at-budget, recall-at-budget, fraud captures, false alerts, and cost per 10,000 transactions.
- [ ] Apply the same budgets to strict, unsafe, chronological, and prevalence-shift scenarios where the prediction artifact supports a valid comparison.
- [ ] Save the alert-budget curves at 600 DPI with vector PDF export as a secondary format.

**Verification:** The alert budget is selected without test-label optimization, and every curve has explicit axes, units, dataset labels, and model labels.

### Task 4: Quantify D2 temporal distribution shift

**Files:**
- Create: `Credit__\10_framework_formalization\notebooks\12_temporal_drift_diagnostics.ipynb`
- Create: `Credit__\10_framework_formalization\results\d2_drift_diagnostics.csv`
- Create: `Credit__\10_framework_formalization\figures\d2_drift_vs_ap_drop.png`

**Consumes:** D2 governed features and the existing random/chronological split metadata.

**Produces:** Feature-distribution drift diagnostics paired with chronological performance degradation.

- [ ] Use the training split as the reference distribution and compute train-to-test PSI, Jensen--Shannon divergence, and two-sample KS statistics for numeric governed features.
- [ ] Compute train, validation, and chronological-test fraud prevalence with confidence intervals for the two proportions.
- [ ] Join the drift summary with the corresponding AP and MCC drops without claiming causality.
- [ ] Report the number of features tested and the multiple-testing correction used for KS p-values.
- [ ] Plot feature drift magnitude against model AP drop only as an exploratory association, with a caption stating that association is not causal evidence.

**Verification:** No chronological-test label is used to fit a preprocessing step, choose a feature, or tune a threshold; it is used only to evaluate the already-defined diagnostic.

### Task 5: Measure explanation-reliability gap

**Files:**
- Create: `Credit__\10_framework_formalization\notebooks\13_explanation_reliability_gap.ipynb`
- Create: `Credit__\10_framework_formalization\results\explanation_reliability_gap.csv`
- Create: `Credit__\10_framework_formalization\figures\explanation_reliability_gap.png`

**Consumes:** Fitted tree models or reproducible model checkpoints, governed feature names, strict test data, and existing model-native feature rankings.

**Produces:** Agreement between model-native importance, permutation reliance, and existing explanation rankings.

- [ ] Compute model-native feature importance on the fitted tree model.
- [ ] Compute permutation importance on the held-out test set using a fixed scoring metric and a fixed number of repeats.
- [ ] Map one-hot columns back to governed source feature groups before ranking.
- [ ] Compute Top-5 and Top-10 Jaccard agreement plus Spearman rank correlation between importance methods.
- [ ] Define the explanation-reliability gap as the difference between explanation ranking stability and performance-reliance stability; report it as a profile component, not as a universal quality score.
- [ ] Preserve the D1 instability result as a valid negative finding.

**Verification:** Permutation importance never uses training labels to refit the model, and the manuscript does not call feature importance causal.

### Task 6: Create the literature-gap and novelty evidence matrix

**Files:**
- Create: `Credit__\10_framework_formalization\novelty_comparison_matrix.csv`
- Create: `Credit__\10_framework_formalization\novelty_comparison_matrix.md`
- Modify: `Credit__\11_manuscript_rewrite\references.bib`

**Produces:** A source-backed comparison of existing fraud-evaluation studies against the exact LC-ORF dimensions.

- [ ] Include columns for leakage control, chronological evaluation, prevalence shift, calibration, alert capacity, explanation stability, performance-reliance validation, uncertainty intervals, and reproducible artifacts.
- [ ] Include only papers that can be verified from a publisher, proceedings, DOI, or stable preprint page.
- [ ] Use cautious wording: `not identified in our search` rather than `never done before`.
- [ ] Cite the strongest overlapping studies in Related Work and explain the remaining contribution as the paired counterfactual audit record plus uncertainty and operational consequences.

**Verification:** Every row has a complete citation key, stable source, and a manually checked inclusion rationale.

### Task 7: Build the multidimensional audit profile

**Files:**
- Create: `Credit__\10_framework_formalization\results\lcorf_audit_profile.csv`
- Create: `Credit__\10_framework_formalization\figures\lcorf_audit_profile_heatmap.png`
- Create: `Credit__\10_framework_formalization\LCORF_AUDIT_PROFILE_SPEC.md`

**Consumes:** Outputs from Tasks 2--5.

**Produces:** One auditable record per dataset/model pair, without an arbitrary weighted score.

- [ ] Store the five existing indices plus confidence intervals, alert-budget impact, drift diagnostics, and explanation-reliability agreement.
- [ ] Assign `robust`, `fragile`, or `inconclusive` only using the thresholds frozen in Task 1.
- [ ] Render the profile as a heatmap and a CSV, with each cell linked to an artifact ID.
- [ ] Do not collapse the profile into one number.

**Verification:** Every profile cell can be traced to a summary CSV and a notebook; no result is manually typed into the heatmap source.

### Task 8: Rewrite the manuscript around the upgraded contribution

**Files:**
- Modify: `Credit__\11_manuscript_rewrite\main.tex`
- Modify: `Credit__\11_manuscript_rewrite\references.bib`
- Modify: `Credit__\11_manuscript_rewrite\README.md`

- [ ] Rewrite the abstract so it states the counterfactual audit, uncertainty intervals, fixed-alert evaluation, and multidimensional audit profile.
- [ ] Replace the current novelty paragraph with the formal audit-record definition and the one-change rule.
- [ ] Add the literature-gap matrix as a compact table.
- [ ] Add the bootstrap, alert-budget, drift, and explanation-reliability results only after their CSV outputs pass verification.
- [ ] Add a clear limitations paragraph covering public datasets, D3 simulation, D1 pseudo-time, public cost assumptions, and the absence of human-grounded explanation validation.
- [ ] Update the contribution list so each contribution maps to one artifact family and one research question.

**Verification:** Run citation-key, figure-path, placeholder, and source-artifact checks before compiling.

### Task 9: Compile and perform the final strict-review gate

**Files:**
- Create: `Credit__\11_manuscript_rewrite\final_review_checklist.md`
- Create: `Credit__\11_manuscript_rewrite\final_pdf_audit_report.md`

- [ ] Compile with the IEEE Access class using the clean sequence: LaTeX, BibTeX, LaTeX, LaTeX.
- [ ] Recompile from scratch so no stale `.aux`, `.bbl`, `.bcf`, or `.blg` files remain.
- [ ] Confirm zero `[?]` citations, zero overfull boxes in the compiler log, no clipped table rows, and readable figures at 100% zoom.
- [ ] Confirm all experimental figures are 600 DPI and all author portraits are replaced with consistent professional images where available.
- [ ] Recalculate the four reviewer scores only after the final PDF audit.

**Exit criterion:** The novelty claim is supported by new uncertainty-aware operational evidence, not by renamed indices or additional prose alone.
