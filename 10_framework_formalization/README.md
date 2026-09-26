# 📊 Unified Framework Audit & Alert Budgeting

This module consolidates prediction-export artifacts, runs 1,000 paired bootstrap iterations, evaluates operational alert-budget capacity, and produces the unified LC-ORF audit profile.

## 📓 Notebooks

- **`14_lcorf_bootstrap_alert_profile_colab.ipynb`** *(Core Evaluation)*: Performs 1,000 paired bootstrap calculations across all audit units, computes confidence intervals, assigns materiality labels (*Robust*, *Fragile*, *Inconclusive*), and evaluates top 1%, 2%, 5% alert-budget precision.
- **`10_task2_prediction_artifact_audit_colab.ipynb`**: Audits prediction export integrity and alignment.
- **`15_lcorf_final_novelty_hardening_colab.ipynb`**: Verification and consistency audits across all artifact outputs.

## 📂 Folder Contents

- **`figures/`**: Generated publication-quality vector PDF figures:
  - `fig02_lcorf_final_audit_profile_heatmap.pdf`: Consolidated multi-axis operational audit profile heatmap across all six evaluation dimensions.
  - `fig06_alert_budget_precision_by_axis_dataset.pdf`: Operational alert-budget precision curves under capacity constraints.
- **`results/`**: Comprehensive audit tables:
  - `lcorf_final_audit_profile.csv`: The definitive multi-axis audit profile table.
  - `paired_bootstrap_delta_summary.csv`: Summary of 1,000 paired bootstrap deltas and 95% confidence intervals.
  - `paired_bootstrap_delta_per_seed.csv`: Seed-level bootstrap distributions.
  - `alert_budget_summary.csv`: Comprehensive alert workload performance under review budgets.
  - `table01_lcorf_audit_axes.csv`: Formal definitions of all audit axes.
  - `table02_final_profile_axis_summary.csv`: Profile coverage summary.
  - `table07_alert_budget_compact_summary.csv`: Compact operational alert-budget metrics.
  - `table09_related_work_matrix.csv`: Literature matrix comparing fraud evaluation frameworks.
  - `table10_lcorf_notation.csv`: Mathematical notation for framework formalization.
  - `table11_lcorf_material_thresholds.csv`: Metric-specific materiality decision thresholds.
