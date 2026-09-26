# LC-ORF Framework Project Status

## Research Direction & Framework Objective

LC-ORF establishes a novelty-focused operational evaluation and stress-testing framework for financial fraud detection.

**Working thesis:**

> A leakage-controlled operational stress-testing framework demonstrates that fraud-detection model choice and operational efficacy are highly sensitive to feature availability, leakage risk, cost assumptions, review capacity, calibration quality, prevalence shifts, and temporal ordering.

---

## Milestone Progress

### 01 Dataset Truth Audit
- **Location:** `01_dataset_truth_audit/`
- Audited `creditcard.csv` (D1), `fraudTest.csv` (D2), and `PS.csv` (D3).
- Confirmed row counts, fraud ratios, duplicates, missing values, and time fields.
- Verified D1 deduplication (284,807 down to 283,726 rows).
- Flagged identifier-risk features (e.g. `trans_num`, `Unnamed: 0`, and post-transaction balance fields).

### 02 Feature Governance
- **Location:** `02_feature_governance/`
- Established column-level governance rules across all three benchmarks.
- Defined the **Strict Main Feature Set** excluding future or post-transaction fields.
- Isolated post-transaction ledger balances for dedicated leakage stress experiments.

### 03 Leakage Stress Testing
- **Location:** `03_leakage_stress_testing/`
- Implemented Google Colab T4 GPU notebooks with resumable checkpointing.
- Tested safe pipelines against unsafe SMOTE-before-split and ledger-state leakage across 5 random seeds (42, 101, 202, 303, 404).

### 06 Temporal Robustness
- **Location:** `06_temporal_robustness/`
- Quantified performance drops between random stratified splits and chronological splits.
- Computed feature drift metrics and temporal degradation curves.

### 07 Prevalence Stress Testing
- **Location:** `07_prevalence_stress_test/`
- Evaluated models across 6 deterministic prevalence shift tiers.
- Generated prevalence sensitivity profiles and alert-cost heatmaps.

### 08 Calibration & Recalibration
- **Location:** `08_calibration_recalibration/`
- Measured Brier score, ECE, Platt scaling, and Isotonic regression.
- Demonstrated decoupling between probability calibration and downstream cost.

### 09 Explanation Stability
- **Location:** `09_explanation_stability/`
- Assessed SHAP and Tree feature attribution stability across seeds and temporal splits.
- Discovered the *Explanation Reliability Gap* where feature rank stability persists despite predictive drop.

### 10 Framework Formalization & Bootstrap Profiling
- **Location:** `10_framework_formalization/`
- Formalized audit units $(d, m, s, a, c_0, c_1, k)$ and metric materiality thresholds.
- Computed 1,000 paired bootstrap confidence intervals.
- Integrated fixed alert-budget capacity metrics (top 1%, 2%, 5%).

### 12 Reproducibility Hardening
- **Location:** `12_github_reproducibility/`
- Created environment setup guides and execution pipelines.

### 13 Evaluation Artifacts
- **Location:** `13_evaluation_artifacts/`
- Consolidated 600-DPI publication figures, bootstrap delta summaries, and prediction manifests.

---

## Core Operational Rules

1. No empirical result is reported without a saved CSV output.
2. Every benchmark table and figure maps directly to an exported artifact.
3. Strict feature protocol is enforced as the baseline reference.
4. Leakage-risk features appear exclusively in controlled stress tests.
5. Models are audited as operational profiles, not single static leaderboard scores.
