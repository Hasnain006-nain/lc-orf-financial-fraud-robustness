# LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection

[![Python 3.10+](https://img.shields.io/badge/python-3.10%20%7C%203.11-blue.svg)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/framework-LC--ORF-green.svg)](#framework-overview)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Reproducibility](https://img.shields.io/badge/reproducibility-1000%20bootstraps%20%7C%205%20seeds-orange.svg)](#reproducibility-guide)
[![Colab Ready](https://img.shields.io/badge/Colab-GPU%20Ready-f39f37.svg)](https://colab.research.google.com/)
[![Target: IEEE Access](https://img.shields.io/badge/submission-IEEE%20Access-00629B.svg)](#citation)

---

## 📌 Executive Summary

Financial fraud detection research is predominantly reported as a **single-split model-comparison problem**, where algorithms compete on static test leaderboards using summary metrics like ROC-AUC. However, in live production banking environments, fraud detection models routinely fail because real-world operational conditions violate static evaluation assumptions:

1. **Preprocessing & Resampling Leakage:** Oversampling (e.g., SMOTE) or feature scaling applied before data splitting leaks test distribution information, producing phantom performance.
2. **Temporal Distribution Drift:** Random train/test splits inadvertently mix future knowledge into the past, severely masking real-world chronological degradation.
3. **Prevalence Shifts:** The base fraud rate fluctuates dynamically across payment seasons, causing dramatic swings in alert precision and false positive rates.
4. **Uncalibrated Probability Scores:** High classification ranking does not guarantee calibrated probabilities for automated cutoff thresholding and risk scoring.
5. **The Explanation Reliability Gap:** Feature attribution rankings (e.g., Tree SHAP) can appear deceptively stable even while predictive performance experiences catastrophic drops.
6. **Alert-Budget Bottlenecks:** Human review teams have fixed daily alert capacities, meaning high recall at arbitrary thresholds is operationally useless without high precision in the top budget tiers (e.g., top 1% or 2%).

**LC-ORF** addresses this systemic reporting gap. Rather than proposing another incremental classifier, **LC-ORF is a leakage-controlled operational audit framework** that perturbs evaluation assumptions across six critical axes to produce auditable, bootstrap-backed operational profiles.

---

## 🏗️ Framework Architecture

<div align="center">
  <img src="assets/fig01_lcorf_framework_workflow.png" alt="LC-ORF Operational Robustness Workflow" width="95%"/>
  <p><em><strong>Figure 1:</strong> LC-ORF operational robustness workflow. The same fraud-detection models are audited under controlled changes in leakage, temporal protocol, prevalence, calibration, explanation behavior, and alert-budget assumptions.</em></p>
</div>

The LC-ORF workflow operates in five structured stages:

* **Stage 1 (Public Fraud Datasets):** Multi-domain benchmark evaluation covering European card transactions (D1), simulated merchant terminal streams (D2), and mobile money transactions (D3).
* **Stage 2 (Leakage-Safe Feature Governance):** Elimination of direct and proxy identifiers, mandatory exclusion of post-transaction ledger state fields, and formal partitioning between *Strict* (production-available) and *Stress* feature sets.
* **Stage 3 (Scenario-Pair Evaluation):** Controlled evaluation across reference ($c_0$) and stressed ($c_1$) scenarios for all six audit axes.
* **Stage 4 (Model and Artifact Layer):** Tree-based gradient boosted models (LightGBM, XGBoost) audited over five random seeds ($s \in \{42, 101, 202, 303, 404\}$) with row-level prediction exports (scores, true labels, operational thresholds, transaction IDs).
* **Stage 5 (LC-ORF Audit Profile):** Pairwise metric deltas evaluated with 1,000 paired bootstrap iterations against metric-specific materiality thresholds, yielding definitive *Robust*, *Fragile*, or *Inconclusive* claims accompanied by explicit claim boundaries.

---

## 🔍 The Six Operational Robustness Audit Axes

LC-ORF formalizes an audit unit as $(d, m, s, a, c_0, c_1, k)$, representing dataset $d$, model family $m$, random seed $s$, audit axis $a$, reference scenario $c_0$, perturbed scenario $c_1$, and metric $k$.

| Audit Axis | Reference Condition ($c_0$) | Perturbed Condition ($c_1$) | Target Operational Vulnerability | Materiality Threshold |
| :--- | :--- | :--- | :--- | :--- |
| **1. Leakage Inflation** | `SAFE_STRICT` (Strict pipeline inside cross-validation) | `UNSAFE_SMOTE_BEFORE_SPLIT` / `D3_LEDGER_STATE` | Resampling leakage and post-transaction balance leakage | $\Delta \text{MCC} \ge +0.05$<br>$\Delta \text{AP} \ge +0.05$ |
| **2. Temporal Degradation** | `RANDOM_STRATIFIED_SAFE` | `CHRONOLOGICAL_SAFE` (Sequential temporal split) | Concept drift, merchant/consumer shift over time | $\Delta \text{AP} \le -0.05$<br>$\Delta \text{MCC} \le -0.05$ |
| **3. Prevalence Sensitivity** | Native empirical base rate ($\pi_0$) | Controlled downsampling across 6 base-rate tiers ($\pi \in \{0.0001 \dots 0.05\}$) | Sensitivity to fluctuating fraud volume and false positive explosion | Fragility rate over profile components |
| **4. Calibration Quality** | Raw model probabilities | Platt Scaling / Isotonic Recalibration | Score distortion, Expected Calibration Error (ECE), Brier score | $\Delta \text{Brier} \le -0.005$<br>$\Delta \text{Cost} \le -0.05$ |
| **5. Explanation Reliability** | Random split explanation rankings | Chronological split explanation rankings | Decoupling between feature attribution rank stability and accuracy | $\text{Rank Corr} > 0.85$ despite $\Delta \text{AP} < -0.15$ |
| **6. Alert-Budget Capacity** | Theoretical max recall / F1 | Top 1%, Top 2%, Top 5% decision thresholds | Human investigator review capacity constraints | Alert-tier Precision & Detection Rate |

---

## 📊 Key Empirical Discoveries

Across 5 random seeds, 3 datasets, and 1,000 paired bootstrap iterations per unit:

```
                                 EMPIRICAL AUDIT HIGHLIGHTS
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│ 1. SMOTE Leakage Inflation:                                                                 │
│    • D2 (fraudTest): XGBoost MCC artificially inflated by +0.472 [95% CI: 0.459, 0.483]     │
│    • D2 (fraudTest): LightGBM MCC artificially inflated by +0.361 [95% CI: 0.376, 0.406]    │
│    • D1 (creditcard): XGBoost MCC inflated by +0.357 [95% CI: 0.275, 0.378]                 │
│                                                                                             │
│ 2. Chronological Temporal Degradation:                                                      │
│    • D2 (fraudTest): XGBoost Average Precision dropped by -0.277 [95% CI: -0.354, -0.202]   │
│    • D2 (fraudTest): LightGBM Average Precision dropped by -0.245 [95% CI: -0.308, -0.186]  │
│                                                                                             │
│ 3. Prevalence Shift Fragility:                                                              │
│    • 29 of 36 evaluated prevalence-profile components were labeled operationally "Fragile"   │
│                                                                                             │
│ 4. Explanation Reliability Gap:                                                             │
│    • Top-5 feature attribution rankings remained highly correlated (Spearman rho > 0.90)    │
│      even while model precision experienced sharp temporal degradation                      │
└─────────────────────────────────────────────────────────────────────────────────────────────┘
```

### Representative Bootstrap Audit Findings (Table III from Manuscript)

| Axis | Dataset | Model | Metric | Reference | Perturbed | Mean Delta ($\bar{\Delta}$) | Median 95% Bootstrap CI | Label Interpretation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Leakage** | D2\_fraudTest | XGBoost | MCC | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.472** | [0.459, 0.483] | **Fragile** (5/5 seeds) |
| **Leakage** | D2\_fraudTest | LightGBM | MCC | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.361** | [0.376, 0.406] | **Fragile** (5/5 seeds) |
| **Leakage** | D1\_creditcard | XGBoost | MCC | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.357** | [0.275, 0.378] | **Fragile** (5/5 seeds) |
| **Leakage** | D1\_creditcard | XGBoost | AP | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.142** | [0.085, 0.215] | **Fragile** (5/5 seeds) |
| **Leakage** | D1\_creditcard | LightGBM | AP | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.140** | [0.081, 0.215] | **Fragile** (5/5 seeds) |
| **Leakage** | D3\_PaySim | XGBoost | MCC | `D3_STRICT_SAFE` | `D3_LEDGER_STATE` | **+0.129** | [0.126, 0.152] | **Fragile** (4/5 seeds) |
| **Temporal** | D2\_fraudTest | XGBoost | AP | `RAND_STRAT_SAFE` | `CHRONO_SAFE` | **-0.277** | [-0.354, -0.202] | **Fragile** (5/5 seeds) |
| **Temporal** | D2\_fraudTest | LightGBM | AP | `RAND_STRAT_SAFE` | `CHRONO_SAFE` | **-0.245** | [-0.308, -0.186] | **Fragile** (5/5 seeds) |
| **Temporal** | D2\_fraudTest | LightGBM | MCC | `RAND_STRAT_SAFE` | `CHRONO_SAFE` | **-0.242** | [-0.288, -0.245] | **Fragile** (5/5 seeds) |
| **Temporal** | D2\_fraudTest | XGBoost | MCC | `RAND_STRAT_SAFE` | `CHRONO_SAFE` | **-0.208** | [-0.218, -0.176] | **Fragile** (5/5 seeds) |

---

## 📂 Benchmark Datasets & Governance

The framework audits three public benchmarks under strict feature governance protocols:

| ID | Dataset Benchmark | Domain | Raw Transactions | Fraud Count | Raw Rate | Governed Cleaned State |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **D1** | Credit Card Fraud (ULB) | European card transactions | 284,807 | 492 | 0.173% | **283,726** unique rows (473 frauds) after deduplication |
| **D2** | Fraud Detection (Kartik Shenoy) | Simulated merchant stream | 555,719 | 2,145 | 0.386% | Removed index artifact `Unnamed: 0` and ID `trans_num` |
| **D3** | PaySim (Lopez-Rojas et al.) | Mobile money simulator | 5,840,046 | 4,497 | 0.077% | Filtered `TRANSFER`/`CASH_OUT`; post-balances isolated |

### Public Dataset Acquisition

Raw dataset files are **not** committed to this repository due to size constraints (~800 MB). To reproduce the complete pipeline from scratch:

1. Download the three public CSV files:
   - **`creditcard.csv`**: [Kaggle ULB MLG Link](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
   - **`fraudTest.csv`**: [Kaggle Kartik Shenoy Link](https://www.kaggle.com/datasets/kartik2112/fraud-detection)
   - **`PS.csv`**: [Kaggle PaySim Link](https://www.kaggle.com/datasets/ealaxi/paysim1)
2. Place the uncompressed CSV files in `00_source_datasets/` (see [00_source_datasets/README.md](00_source_datasets/README.md)).
3. Refer to [00_source_datasets_notes/DATASET_ACCESS_NOTE.md](00_source_datasets_notes/DATASET_ACCESS_NOTE.md) for full hash verification and details.

---

## 🗂️ Repository Structure

```
lc-orf-financial-fraud-robustness/
├── assets/                                  # High-resolution publication figures (Figure 1)
│   └── fig01_lcorf_framework_workflow.png
├── 00_source_datasets/                      # Expected directory for raw benchmark CSVs
│   └── README.md                            # Download instructions and dataset notes
├── 00_source_datasets_notes/                # Access policies, hashes, and size notes
│   └── DATASET_ACCESS_NOTE.md
├── 01_dataset_truth_audit/                  # Raw dataset auditing, duplicate verification
│   ├── dataset_truth_audit.md               # Audit findings on D1, D2, and D3
│   ├── dataset_audit_summary.csv            # Summary metrics and duplicate counts
│   └── supplemental_risk_findings.csv       # Identified leakage columns & ID hazards
├── 02_feature_governance/                   # Column-by-column governance rules
│   ├── feature_governance_table.md          # Governance definitions for all fields
│   ├── feature_governance_table.csv         # Structured rule table
│   └── feature_set_definitions.csv          # Strict vs. stress tier specifications
├── 03_leakage_stress_testing/               # Leakage stress test Colab notebooks & results
│   ├── leakage_stress_multiseed_colab.ipynb # 5-seed LightGBM / XGBoost leakage pipeline
│   ├── leakage_stress_testing_colab.ipynb   # Initial single-seed pipeline
│   └── received_multiseed_results_20260924/ # Checkpoints and raw CSV outputs
├── 06_temporal_robustness/                  # Chronological evaluation notebooks & data
│   ├── temporal_robustness_colab.ipynb      # Sequential split and population drift
│   └── received_results_20260924/           # Temporal results and drift metrics
├── 07_prevalence_stress_test/               # Base-rate shift notebooks & profiles
│   ├── prevalence_stress_colab.ipynb        # Deterministic downsampling experiments
│   └── received_results_20260924/           # Prevalence profile tables
├── 08_calibration_recalibration/            # Probability calibration evaluation
│   ├── calibration_recalibration_colab.ipynb# ECE, Brier score, Platt, and Isotonic
│   └── received_results_20260924/           # Calibration metrics and cost evaluations
├── 09_explanation_stability/                # XAI attribution stability notebooks
│   ├── explanation_stability_colab.ipynb    # Tree SHAP & Feature Importance stability
│   └── received_results_20260924/           # Spearman rank correlation outputs
├── 10_framework_formalization/              # Formal methodology, bootstrap, & alert budgets
│   ├── IEEE_ACCESS_FRAMEWORK_FORMALIZATION.md
│   ├── RESULTS_TABLE_FIGURE_MAP.md          # Mapping between paper and code artifacts
│   ├── CLAIMS_AND_LIMITATIONS_REGISTER.md   # Explicit boundary register
│   └── notebooks/                           # Bootstrap and prediction audit notebooks
├── 12_github_reproducibility/               # Reproducibility instructions & configs
│   └── README.md
├── 13_paper_submission_assets/              # Production-ready paper assets
│   ├── 01_main_paper_assets/                # Main manuscript figures (PDF/PNG) & tables
│   └── 02_supplementary_assets/             # Supplementary tables, source result CSVs
├── 14_lcorf_manuscript_rebuild/             # IEEE Access LaTeX manuscript sources
│   ├── main.tex                             # Rebuilt complete manuscript LaTeX
│   ├── references.bib                       # Verified BibTeX citations
│   ├── biographies.tex                      # Author biographies
│   └── figures/                             # High-resolution manuscript figures
├── .gitignore                               # Rigorous ignore rules (CSVs, tmp, caches)
├── PROJECT_STATUS.md                        # Framework milestone completion log
├── README.md                                # Comprehensive repository documentation
└── requirements.txt                         # Python environment dependencies
```

---

## 🚀 Reproduction & Quickstart Guide

### 1. Environment Installation

Ensure you have Python 3.10 or 3.11 installed:

```bash
# Clone the repository
git clone https://github.com/Hasnain006-nain/lc-orf-financial-fraud-robustness.git
cd lc-orf-financial-fraud-robustness

# Set up virtual environment
python -m venv venv

# Activate environment
# On Linux / macOS:
source venv/bin/activate
# On Windows (PowerShell):
.\venv\Scripts\Activate.ps1

# Install required packages
pip install -r requirements.txt
```

### 2. Google Colab GPU Reproduction

All experimental notebooks in `03_leakage_stress_testing`, `06_temporal_robustness`, `07_prevalence_stress_test`, `08_calibration_recalibration`, `09_explanation_stability`, and `10_framework_formalization` are configured for **Google Colab (T4 GPU runtime)**:

* Built-in Google Drive mounting persists checkpoints directly to your Drive.
* If a session disconnects, rerun from the top cell: existing checkpoint files are automatically recognized and skipped.
* Figures are saved automatically in both high-resolution PNG (600 DPI) and publication-ready vector PDF.

### 3. Bootstrap Significance & Final Audit Profile

To reproduce the 1,000 paired bootstrap calculations and generate the consolidated multi-axis audit profile without needing raw transaction data:

1. Open `10_framework_formalization/notebooks/14_lcorf_bootstrap_alert_profile_colab.ipynb`.
2. Execute the cells to process the exported prediction artifacts.
3. The notebook reproduces `lcorf_final_audit_profile.csv`, confidence intervals, and the alert-budget summary tables.

---

## 📑 Manuscript Traceability Map

Every table and figure in the manuscript corresponds directly to generated CSV outputs in this package:

| Paper Asset | Manuscript Description | Source Result Artifact |
| :--- | :--- | :--- |
| **Figure 1** | LC-ORF Operational Framework Workflow | [`assets/fig01_lcorf_framework_workflow.png`](assets/fig01_lcorf_framework_workflow.png) |
| **Figure 2** | Final Multi-Axis Audit Profile Heatmap | `13_paper_submission_assets/01_main_paper_assets/figures/png/fig02_*.png` |
| **Figure 3** | Multi-Seed AP Leakage Inflation Heatmap | `13_paper_submission_assets/01_main_paper_assets/figures/png/fig03_*.png` |
| **Figure 4** | D2 Feature Drift vs. Temporal AP Drop | `13_paper_submission_assets/01_main_paper_assets/figures/png/fig04_*.png` |
| **Figure 5** | Prevalence Profile Heatmap | `13_paper_submission_assets/01_main_paper_assets/figures/png/fig05_*.png` |
| **Figure 6** | Alert Budget Precision by Axis & Dataset | `13_paper_submission_assets/01_main_paper_assets/figures/png/fig06_*.png` |
| **Figure 7** | Explanation Reliability Gap Visualization | `13_paper_submission_assets/01_main_paper_assets/figures/png/fig07_*.png` |
| **Table I** | LC-ORF Audit Axes & Claim Boundaries | `13_paper_submission_assets/01_main_paper_assets/tables/table01_lcorf_audit_axes.csv` |
| **Table II** | Final Audit Profile Coverage Summary | `13_paper_submission_assets/01_main_paper_assets/tables/table02_final_profile_axis_summary.csv` |
| **Table III** | Key Paired Bootstrap Findings (1,000 reps) | `13_paper_submission_assets/01_main_paper_assets/tables/table03_key_bootstrap_findings.csv` |
| **Table IV** | D2 Temporal Drift Diagnostic Features | `13_paper_submission_assets/01_main_paper_assets/tables/table04_d2_temporal_drift_features.csv` |
| **Table V** | D2 Temporal Prevalence by Split | `13_paper_submission_assets/01_main_paper_assets/tables/table05_d2_temporal_prevalence_by_split.csv` |
| **Table VI** | Explanation Reliability Gap Evidence | `13_paper_submission_assets/01_main_paper_assets/tables/table06_explanation_reliability_gap.csv` |
| **Table VII** | Compact Alert Budget Capacity Summary | `13_paper_submission_assets/01_main_paper_assets/tables/table07_alert_budget_compact_summary.csv` |
| **Table VIII**| Prevalence Fragility Components | `13_paper_submission_assets/01_main_paper_assets/tables/table08_prevalence_profile_component.csv` |

---

## ⚖️ Explicit Research Claim Boundaries

In adherence to rigorous scientific integrity standards, this repository maintains explicit boundaries:

* 🚫 **No Classifier SOTA Claims:** LC-ORF does *not* claim that LightGBM or XGBoost is a superior classifier or state-of-the-art fraud detection model.
* 🚫 **No Production-Ready Claims:** The framework is an operational evaluation and stress-testing audit protocol; it does not claim to be a drop-in production banking backend.
* 🚫 **No Universal Drift Claims:** Measured temporal degradation reflects the tested benchmark protocol and cannot be generalized as proof of drift in all financial institutions.
* 🚫 **No Causal XAI Claims:** The *Explanation Reliability Gap* measures empirical rank divergence between attribution rankings and predictive drop; it does *not* validate causal explanations.
* ✅ **Transparent Reporting:** Robust, fragile, and inconclusive audit results are reported with equal scientific weight.

---

## 👥 Authors & Affiliations

* **Hasnain Haider**<sup>1</sup> *(Corresponding Author: hasnain.haider@student.aiu.edu.my)*
* **Waseem Mushtaq**<sup>1</sup>
* **Qaiser Abbas**<sup>2</sup>
* **Adnan Nadeem Al Hassan**<sup>2</sup>
* **Abdullah Alshanqiti**<sup>2</sup>
* **Sami Albouq**<sup>2</sup>

<sup>1</sup> *School of Computing and Informatics, Albukhary International University, Alor Setar, Kedah, Malaysia*  
<sup>2</sup> *Faculty of Computer and Information Systems, Islamic University of Madinah, Madinah, Saudi Arabia*

---

## 📖 Citation

If you find this framework, experimental suite, or audit methodology useful in your research, please cite:

```bibtex
@article{haider2026lcorf,
  title={{LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection}},
  author={Haider, Hasnain and Mushtaq, Waseem and Abbas, Qaiser and Al Hassan, Adnan Nadeem and Alshanqiti, Abdullah and Albouq, Sami},
  journal={IEEE Access},
  year={2026},
  note={Under Review / Reproducibility Package}
}
```

---

## 📄 License

This research codebase and reproducibility package is licensed under the [MIT License](LICENSE).
