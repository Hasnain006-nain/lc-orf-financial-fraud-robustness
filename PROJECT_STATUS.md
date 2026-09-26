# Credit Fraud Paper Project Status

## Current Research Direction

The paper is being rebuilt from a model-comparison study into a novelty-focused operational evaluation framework for financial fraud detection.

Working thesis:

> A leakage-controlled operational stress-testing framework can show that fraud-detection model choice is unstable under feature availability, leakage risk, cost assumptions, review capacity, calibration quality, prevalence shift, and temporal ordering.

## Completed Work

### 01 Dataset Truth Audit

Location: `01_dataset_truth_audit/`

Completed:

- Audited `creditcard.csv`, `fraudTest.csv`, and `PS.csv`.
- Recorded rows, fraud counts, fraud rates, duplicates, missing values, label columns, time fields, identifier-risk columns, high-cardinality columns, and leakage-review columns.
- Confirmed D1 duplicate removal explains the manuscript's cleaned count: 283,726 rows and 473 fraud rows.
- Flagged D2 `Unnamed: 0` and `trans_num` as mandatory removals.
- Flagged D3 `isFlaggedFraud`, `nameOrig`, `nameDest`, `newbalanceOrig`, and `newbalanceDest` as high-risk columns requiring governance.

Key files:

- `dataset_truth_audit.md`
- `dataset_audit_summary.csv`
- `supplemental_risk_findings.csv`

### 02 Feature Governance

Location: `02_feature_governance/`

Completed:

- Created a column-level governance table for all three datasets.
- Defined the main `strict` feature set for the revised paper.
- Defined separate feature-set tiers for chronology, operational context, ledger-state stress, and sensitive/proxy variables.
- Established that D3 post-transaction balances are excluded from the strict main protocol and used only in a leakage/ledger-state stress test.

Key files:

- `feature_governance_table.md`
- `feature_governance_table.csv`
- `feature_set_definitions.csv`

### 03 Leakage Stress Testing

Location: `03_leakage_stress_testing/`

Prepared:

- Created a Google Colab notebook for T4 GPU runtime.
- Added Drive mounting and configurable `PROJECT_ROOT`.
- Added resumable per-dataset/per-scenario/per-model checkpoints.
- Added automatic Drive output folders for checkpoints, results, logs, and figures.
- Added 600-DPI PNG and PDF figure export.
- Implemented strict feature rules from the feature governance milestone.
- Implemented safe pipeline, unsafe preprocessing stress, unsafe SMOTE-before-split stress, and D3 ledger-state stress.

Key files:

- `leakage_stress_testing_colab.ipynb`
- `README.md`
- `leakage_stress_multiseed_colab.ipynb`
- `README_multiseed.md`

Prepared next:

- Created a five-seed leakage robustness notebook using XGBoost and LightGBM.
- Seeds: 42, 101, 202, 303, 404.
- Expected Colab T4 runtime: 45-75 minutes; allow up to 90 minutes if Drive I/O is slow.
- Outputs save under `03_leakage_stress_testing/leakage_stress_multiseed_v1/`.

### 11 Manuscript Rewrite

Goal:

Rewrite the LaTeX manuscript around the LC-ORF framework and IEEE Access resubmission standards.

Completed:

- Created a new IEEE Access manuscript draft centered on LC-ORF instead of model comparison.
- Added a new title, abstract, contributions, methodology, results, discussion, limitations, bibliography, and author biographies.
- Selected five main-paper figures and copied them into `11_manuscript_rewrite/paper_figures/`.
- Copied the deliverable package to `outputs/milestone_11_manuscript_rewrite/`.
- Verified that all LaTeX citations have matching BibTeX entries, all BibTeX entries are cited, the five selected paper figures exist, and no TODO/TBD placeholders remain.

Key files:

- `11_manuscript_rewrite/main.tex`
- `11_manuscript_rewrite/references.bib`
- `11_manuscript_rewrite/README.md`
- `11_manuscript_rewrite/paper_figures/`

## Next Milestone

### 12 Reproducibility and Submission Hardening

Goal:

Prepare the rewritten manuscript for IEEE Access-quality submission by checking compilation, source traceability, result-table accuracy, figure readability, bibliography metadata, and GitHub reproducibility.

Immediate work:

1. Compile the manuscript inside the official IEEE Access LaTeX template.
2. Fix any LaTeX class, bibliography, float, author-photo, or figure-path issues.
3. Cross-check every numeric claim in `main.tex` against the saved CSV files.
4. Verify all bibliography metadata from publisher or dataset pages.
5. Prepare a clean GitHub reproduction package with notebooks, environment notes, and result manifests.

## Non-Negotiable Rules

- No result can be reported without a saved CSV output.
- Every paper table/figure must map to a saved result file.
- The main paper must use the strict protocol as the primary result.
- Leakage-risk or identity-risk features can appear only in explicitly labeled stress tests.
- Do not call the work production-ready.
