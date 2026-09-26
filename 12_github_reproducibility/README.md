# LC-ORF Reproducibility Package

This directory provides comprehensive documentation, execution instructions, and environment configurations to reproduce all empirical evaluations reported in the manuscript:

> **LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection**

---

## 1. Reproduction Architecture

The LC-ORF evaluation pipeline audits models under controlled perturbations rather than a single static split. Experiments are organized into modular, reproducible milestones:

```
01_dataset_truth_audit/        -> Raw data auditing, duplicate detection, and integrity checks
02_feature_governance/          -> Strict vs. stress feature sets, leakage-safe exclusions
03_leakage_stress_testing/      -> Safe split vs. unsafe SMOTE-before-split & ledger leakage
06_temporal_robustness/         -> Stratified random split vs. chronological sequential split
07_prevalence_stress_test/      -> Deterministic base-rate downsampling across 6 target ratios
08_calibration_recalibration/   -> ECE, Brier score, Platt scaling, and Isotonic regression
09_explanation_stability/       -> Spearman rank correlation & Top-K feature importance Jaccard
10_framework_formalization/     -> Formalization, 1000-sample bootstrap intervals & alert budget
13_paper_submission_assets/     -> Generated figures (PDF/PNG 600 DPI) and manuscript source tables
14_lcorf_manuscript_rebuild/    -> IEEE Access LaTeX manuscript, author bios, and references
```

---

## 2. Environment Setup

### Local Python Environment (Python 3.10+)

Create a clean virtual environment and install the required dependencies:

```bash
# Create and activate environment
python -m venv venv
source venv/bin/activate  # On Windows: .\venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt
```

### Google Colab Execution (T4 GPU Recommended)

Each operational audit milestone includes a self-contained Google Colab notebook (`*_colab.ipynb`):
- Mounts Google Drive automatically to persist checkpoints and artifacts.
- Automatically handles checkpointing: if a Colab session disconnects, rerunning the notebook resumes seamlessly without recomputing completed seeds.
- Automatically outputs 600-DPI publication figures (PNG and PDF) and full result CSV tables.

---

## 3. Execution Pipeline & Suggested Order

For end-to-end reproduction of the audit results:

1. **Dataset Integrity Verification:**
   - Inspect `01_dataset_truth_audit/dataset_truth_audit.md` and `01_dataset_truth_audit/dataset_audit_summary.csv`.
   - Confirm row counts, duplicate deduplication (e.g., D1: 284,807 -> 283,726 unique transactions), and identified leakage risks (`Unnamed: 0`, `trans_num`, `newbalanceOrig`, etc.).

2. **Feature Governance Enforcement:**
   - Review `02_feature_governance/feature_governance_table.csv`.
   - Note the separation between the **Strict Main Feature Set** (leakage-free) and **Stress Feature Sets** (used exclusively for stress tests).

3. **Leakage Inflation Stress Test:**
   - Notebook: `03_leakage_stress_testing/leakage_stress_multiseed_colab.ipynb`
   - Evaluates LightGBM and XGBoost across 5 random seeds (42, 101, 202, 303, 404).
   - Generates `table03_key_bootstrap_findings.csv` and `fig03_multiseed_ap_leakage_inflation_heatmap.png`.

4. **Temporal Robustness Stress Test:**
   - Notebook: `06_temporal_robustness/temporal_robustness_colab.ipynb`
   - Quantifies chronological degradation and population drift on D2.
   - Generates `fig04_d2_drift_vs_temporal_drop.png` and drift diagnostics.

5. **Prevalence Shift Stress Test:**
   - Notebook: `07_prevalence_stress_test/prevalence_stress_colab.ipynb`
   - Generates deterministic prevalence-shift profiles across 6 prevalence tiers.
   - Outputs `fig05_prevalence_profile_heatmap.png` and `table08_prevalence_profile_component.csv`.

6. **Calibration & Recalibration Evaluation:**
   - Notebook: `08_calibration_recalibration/calibration_recalibration_colab.ipynb`
   - Measures Brier score and ECE before and after Platt scaling / Isotonic regression.

7. **Explanation Stability Analysis:**
   - Notebook: `09_explanation_stability/explanation_stability_colab.ipynb`
   - Quantifies the Explanation Reliability Gap (Spearman rank correlation vs. predictive degradation).

8. **Unified LC-ORF Audit Profile & Bootstrap Significance:**
   - Notebook: `10_framework_formalization/notebooks/14_lcorf_bootstrap_alert_profile_colab.ipynb`
   - Performs 1,000 paired bootstrap iterations on prediction exports to compute confidence intervals and assign materiality labels (*Robust*, *Fragile*, or *Inconclusive*).

---

## 4. Verification & Artifact Validation

All reported numbers in the manuscript correspond directly to saved CSV files:
- Source result profiles: `13_paper_submission_assets/02_supplementary_assets/tables/source_results/`
- Bootstrap summary: `paired_bootstrap_delta_summary.csv`
- Final multi-axis audit profile: `lcorf_final_audit_profile.csv`
- Alert budget performance: `alert_budget_summary.csv`
