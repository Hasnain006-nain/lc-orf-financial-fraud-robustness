<div align="center">

# 🛡️ LC-ORF
### **A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection**

[![Python Version](https://img.shields.io/badge/Python-3.10%20%7C%203.11-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-LC--ORF-10B981?style=for-the-badge&logo=shield&logoColor=white)](#-framework-architecture)
[![Colab Ready](https://img.shields.io/badge/Google_Colab-T4_GPU_Ready-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](#-experiment-modules--notebook-suite)
[![Audit](https://img.shields.io/badge/Bootstrap-1000_Replicates-6366F1?style=for-the-badge)](#-key-empirical-findings)
[![Figures](https://img.shields.io/badge/Figures-Vector_PDF-EC1C24?style=for-the-badge&logo=adobeacrobatreader&logoColor=white)](#-experiment-modules--notebook-suite)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

<br/>

[**Overview**](#-overview) •
[**Framework Workflow**](#-framework-architecture) •
[**Modules & Notebooks**](#-experiment-modules--notebook-suite) •
[**Key Findings**](#-key-empirical-findings) •
[**Datasets & Governance**](#-datasets--governance) •
[**Quickstart**](#-quickstart-guide) •
[**Citation**](#-citation)

---

</div>

## 💡 Overview

In deployed financial fraud detection systems, models often experience dramatic post-deployment degradation. The root cause is a fundamental evaluation gap: **fraud models are traditionally evaluated as static leaderboard benchmarks** using single random splits and summary metrics (e.g., ROC-AUC) that mask operational hazards:

* 🚨 **Preprocessing Leakage:** Resampling (such as SMOTE) or normalization applied prior to data splitting leaks future distribution information into the training set.
* 📉 **Temporal Invalidation:** Random splits allow models to peek into the future, hiding severe performance collapse under true chronological transaction arrival.
* ⚠️ **Prevalence Shifts:** The base fraud rate fluctuates continuously in production, causing severe false alarm spikes if models are sensitive to prevalence changes.
* 🎯 **Uncalibrated Probability Scores:** Classification rankings do not guarantee calibrated probabilities for automated cutoff thresholding and risk scoring.
* 🔍 **The Explanation Reliability Gap:** Feature attribution rankings (e.g. Tree SHAP) can remain superficially stable even while predictive performance collapses.
* ⏱️ **Alert-Budget Bottlenecks:** Human review teams have hard daily alert capacities; high recall at arbitrary thresholds is operationally useless without high precision in the top budget tiers (e.g., top 1% or 2%).

**LC-ORF (Leakage-Controlled Operational Robustness Framework)** introduces an active audit methodology. Instead of accepting a single leaderboard score, LC-ORF evaluates models across controlled reference-stress scenario pairs, producing auditable operational profiles backed by 1,000 paired bootstrap iterations.

---

## 🏛️ Framework Architecture

<div align="center">
  <img src="assets/fig01_lcorf_framework_workflow.png" alt="LC-ORF Operational Robustness Workflow" width="94%" style="border-radius: 8px; border: 1px solid #e1e4e8;"/>
  <p><em><strong>Figure 1:</strong> LC-ORF operational robustness workflow. The framework audits fraud-detection models under controlled changes in leakage, temporal protocol, prevalence, calibration, explanation stability, and alert-budget capacity.</em></p>
</div>

The LC-ORF protocol executes in **five structured stages**:

1. **Stage 1 (Public Fraud Datasets):** Multi-domain benchmark evaluation covering European card transactions (D1), simulated merchant terminal streams (D2), and mobile money transactions (D3).
2. **Stage 2 (Leakage-Safe Feature Governance):** Systematic removal of transactional identifiers, future variables, and ledger-state balances to establish a leak-free **Strict Main Feature Set**.
3. **Stage 3 (Scenario-Pair Perturbations):** Controlled evaluation comparing reference conditions ($c_0$) against targeted stress conditions ($c_1$) across 6 operational axes.
4. **Stage 4 (Model & Artifact Layer):** 5-seed tree-based ensemble training (LightGBM & XGBoost) exporting granular predictions (scores, ground-truth labels, decision thresholds).
5. **Stage 5 (Audit Profile & Significance):** 1,000 paired bootstrap resamples per unit evaluated against metric materiality thresholds to produce auditable **Robust**, **Fragile**, or **Inconclusive** profiles.

---

## 🔬 Experiment Modules & Notebook Suite

Each experiment module is completely self-contained with its own notebook, dedicated publication-grade vector PDF `figures/` folder, and dedicated `results/` CSV folder:

| Module / Audit Axis | Notebook | Dedicated Vector PDF Figures | Dedicated Results & CSVs |
| :--- | :--- | :--- | :--- |
| **03. Leakage Stress Testing** | [`leakage_stress_multiseed_colab.ipynb`](03_leakage_stress_testing/leakage_stress_multiseed_colab.ipynb) | [`03_.../figures/`](03_leakage_stress_testing/figures/)<br>• `fig03_multiseed_ap_leakage_inflation_heatmap.pdf` | [`03_.../results/`](03_leakage_stress_testing/results/)<br>• `table03_key_bootstrap_findings.csv`<br>• Checkpoint CSVs |
| **06. Temporal Robustness** | [`temporal_robustness_colab.ipynb`](06_temporal_robustness/temporal_robustness_colab.ipynb) | [`06_.../figures/`](06_temporal_robustness/figures/)<br>• `fig04_d2_drift_vs_temporal_drop.pdf`<br>• `temporal_ap_drop_heatmap.pdf` | [`06_.../results/`](06_temporal_robustness/results/)<br>• `d2_temporal_drift_diagnostics.csv`<br>• `d2_temporal_drop_summary.csv` |
| **07. Prevalence Sensitivity** | [`prevalence_stress_colab.ipynb`](07_prevalence_stress_test/prevalence_stress_colab.ipynb) | [`07_.../figures/`](07_prevalence_stress_test/figures/)<br>• `fig05_prevalence_profile_heatmap.pdf`<br>• `supp_prevalence_precision_curve.pdf` | [`07_.../results/`](07_prevalence_stress_test/results/)<br>• `table08_prevalence_profile_component.csv`<br>• `prevalence_profile_per_target.csv` |
| **08. Calibration Analysis** | [`calibration_recalibration_colab.ipynb`](08_calibration_recalibration/calibration_recalibration_colab.ipynb) | [`08_.../figures/`](08_calibration_recalibration/figures/)<br>• `supp_calibration_brier_reduction_by_dataset.pdf`<br>• `calibration_curve_*.pdf` | [`08_.../results/`](08_calibration_recalibration/results/)<br>• Brier & ECE metric tables<br>• Recalibration checkpoints |
| **09. Explanation Stability** | [`explanation_stability_colab.ipynb`](09_explanation_stability/explanation_stability_colab.ipynb) | [`09_.../figures/`](09_explanation_stability/figures/)<br>• `fig07_explanation_reliability_gap.pdf`<br>• `supp_protocol_explanation_instability_heatmap.pdf` | [`09_.../results/`](09_explanation_stability/results/)<br>• `table06_explanation_reliability_gap.csv`<br>• Feature ranking summaries |
| **10. Unified Audit Profile** | [`14_lcorf_bootstrap_alert_profile_colab.ipynb`](10_framework_formalization/14_lcorf_bootstrap_alert_profile_colab.ipynb) | [`10_.../figures/`](10_framework_formalization/figures/)<br>• `fig02_lcorf_final_audit_profile_heatmap.pdf`<br>• `fig06_alert_budget_precision_by_axis_dataset.pdf` | [`10_.../results/`](10_framework_formalization/results/)<br>• `lcorf_final_audit_profile.csv`<br>• `alert_budget_summary.csv`<br>• `paired_bootstrap_delta_summary.csv` |

---

## 📈 Key Empirical Findings

Audited across **5 random seeds**, **3 benchmark datasets**, and **1,000 paired bootstrap iterations**:

```
 ┌─────────────────────────────────────────────────────────────────────────────────────────────────┐
 │ 🚨 Massive Resampling Leakage Inflation                                                         │
 │    Applying SMOTE before train/test splitting inflated MCC by +0.472 on D2 and +0.357 on D1.   │
 │    This proves standard benchmark oversampling protocols report phantom performance.            │
 ├─────────────────────────────────────────────────────────────────────────────────────────────────┤
 │ 📉 Severe Chronological Degradation                                                             │
 │    Moving from random split to chronological evaluation reduced Average Precision by            │
 │    -0.277 (XGBoost) and -0.245 (LightGBM) on D2 due to unmasked transaction drift.              │
 ├─────────────────────────────────────────────────────────────────────────────────────────────────┤
 │ ⚠️ High Prevalence Fragility (80.6%)                                                            │
 │    29 out of 36 evaluated prevalence-profile components were labeled operationally Fragile      │
 │    under base-rate shifts, exposing high vulnerability in production volume shifts.            │
 ├─────────────────────────────────────────────────────────────────────────────────────────────────┤
 │ 🔍 The Explanation Reliability Gap                                                             │
 │    Top feature importance rankings remained highly correlated (Spearman rho > 0.90)          │
 │    even when models suffered severe predictive collapse, proving XAI stability does not         │
 │    guarantee model reliability.                                                                 │
 └─────────────────────────────────────────────────────────────────────────────────────────────────┘
```

<details>
<summary><b>🔍 Click to view representative paired bootstrap audit findings (1,000 replicates)</b></summary>
<br>

| Audit Axis | Dataset | Model | Metric | Reference | Perturbed | Mean Delta ($\bar{\Delta}$) | Median 95% Bootstrap CI | Outcome |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **Leakage** | D2\_fraudTest | XGBoost | MCC | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.472** | [0.459, 0.483] | 🔴 **Fragile** (5/5 seeds) |
| **Leakage** | D2\_fraudTest | LightGBM | MCC | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.361** | [0.376, 0.406] | 🔴 **Fragile** (5/5 seeds) |
| **Leakage** | D1\_creditcard | XGBoost | MCC | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.357** | [0.275, 0.378] | 🔴 **Fragile** (5/5 seeds) |
| **Leakage** | D1\_creditcard | XGBoost | AP | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.142** | [0.085, 0.215] | 🔴 **Fragile** (5/5 seeds) |
| **Leakage** | D1\_creditcard | LightGBM | AP | `SAFE_STRICT` | `UNSAFE_SMOTE` | **+0.140** | [0.081, 0.215] | 🔴 **Fragile** (5/5 seeds) |
| **Leakage** | D3\_PaySim | XGBoost | MCC | `D3_STRICT` | `D3_LEDGER_STATE` | **+0.129** | [0.126, 0.152] | 🔴 **Fragile** (4/5 seeds) |
| **Temporal** | D2\_fraudTest | XGBoost | AP | `RANDOM_SAFE` | `CHRONO_SAFE` | **-0.277** | [-0.354, -0.202] | 🔴 **Fragile** (5/5 seeds) |
| **Temporal** | D2\_fraudTest | LightGBM | AP | `RANDOM_SAFE` | `CHRONO_SAFE` | **-0.245** | [-0.308, -0.186] | 🔴 **Fragile** (5/5 seeds) |
| **Temporal** | D2\_fraudTest | LightGBM | MCC | `RANDOM_SAFE` | `CHRONO_SAFE` | **-0.242** | [-0.288, -0.245] | 🔴 **Fragile** (5/5 seeds) |
| **Temporal** | D2\_fraudTest | XGBoost | MCC | `RANDOM_SAFE` | `CHRONO_SAFE` | **-0.208** | [-0.218, -0.176] | 🔴 **Fragile** (5/5 seeds) |

</details>

---

## 🗃️ Datasets & Governance

LC-ORF evaluates three widely recognized financial fraud benchmarks under leakage-safe feature governance:

| ID | Dataset | Domain | Raw Records | Frauds | Cleaned Records | Feature Governance Protocol |
| :---: | :--- | :--- | :---: | :---: | :---: | :--- |
| **D1** | [ULB Credit Card](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) | European card payments | 284,807 | 492 (0.17%) | **283,726** | Removed 1,081 duplicate transactions |
| **D2** | [Fraud Detection](https://www.kaggle.com/datasets/kartik2112/fraud-detection) | Merchant transactions | 555,719 | 2,145 (0.39%) | **555,719** | Stripped index artifact `Unnamed: 0` and ID `trans_num` |
| **D3** | [PaySim Mobile Money](https://www.kaggle.com/datasets/ealaxi/paysim1) | Mobile payments | 5,840,046 | 4,497 (0.08%) | **5,840,046** | Isolated post-transaction ledger balances (`newbalance*`) |

> [!NOTE]
> **Data Access Policy:** Raw CSV files (~800 MB uncompressed) are excluded from the repository.
> To run experiments requiring raw data, download the CSV files (`creditcard.csv`, `fraudTest.csv`, `PS.csv`) using the Kaggle links above and place them into [00_source_datasets/](00_source_datasets/). Detailed checksums and verification notes are documented in [00_source_datasets/DATASET_ACCESS_NOTE.md](00_source_datasets/DATASET_ACCESS_NOTE.md).

---

## 🚀 Quickstart Guide

### 1. Local Environment Setup

```bash
# Clone repository
git clone https://github.com/Hasnain006-nain/lc-orf-financial-fraud-robustness.git
cd lc-orf-financial-fraud-robustness

# Set up virtual environment
python -m venv venv

# Activate environment
# On Linux / macOS:
source venv/bin/activate
# On Windows (PowerShell):
.\venv\Scripts\Activate.ps1

# Install requirements
pip install -r requirements.txt
```

### 2. Google Colab GPU Execution

All notebooks in `03_...`, `06_...`, `07_...`, `08_...`, `09_...`, and `10_...` are configured for **Google Colab (T4 GPU runtime)**:
* Automated Google Drive mounting preserves checkpoint CSVs and vector PDF figures.
* Resumable execution: if disconnected, rerunning the notebook automatically detects completed seeds and skips recomputation.

---

## 📁 Repository Structure

```
lc-orf-financial-fraud-robustness/
├── assets/                                 # Figure 1 workflow diagram
│   └── fig01_lcorf_framework_workflow.png
├── 00_source_datasets/                     # Dataset drop directory & access notes
│   ├── README.md                           # Download instructions & URLs
│   └── DATASET_ACCESS_NOTE.md              # Checksums, sizes, and row counts
├── 01_dataset_truth_audit/                 # Duplicate checks & ground-truth audit
│   ├── dataset_audit_summary.csv           # Summary statistics
│   ├── supplemental_risk_findings.csv      # Risk & column classifications
│   └── dataset_truth_audit.md              # Detailed audit report
├── 02_feature_governance/                  # Column-level feature governance
│   ├── feature_governance_table.csv        # Column exclusion rules
│   ├── feature_set_definitions.csv         # Strict vs. stress feature sets
│   └── feature_governance_table.md         # Formal governance criteria
├── 03_leakage_stress_testing/              # Axis 1: Leakage stress testing
│   ├── leakage_stress_multiseed_colab.ipynb# 5-seed Colab notebook
│   ├── figures/                            # Vector PDF heatmaps & cost charts
│   ├── results/                            # Metrics & seed checkpoints
│   └── README.md                           # Axis documentation
├── 06_temporal_robustness/                 # Axis 2: Temporal robustness
│   ├── temporal_robustness_colab.ipynb     # Chronological evaluation notebook
│   ├── figures/                            # Vector PDF drift & AP drop plots
│   ├── results/                            # Drift diagnostics & metrics
│   └── README.md                           # Axis documentation
├── 07_prevalence_stress_test/              # Axis 3: Prevalence stress testing
│   ├── prevalence_stress_colab.ipynb       # Base-rate shift notebook
│   ├── figures/                            # Vector PDF prevalence heatmaps
│   ├── results/                            # Fragility component tables
│   └── README.md                           # Axis documentation
├── 08_calibration_recalibration/           # Axis 4: Calibration & recalibration
│   ├── calibration_recalibration_colab.ipynb# Brier score & ECE notebook
│   ├── figures/                            # Vector PDF calibration curves
│   ├── results/                            # Calibration metrics & checkpoints
│   └── README.md                           # Axis documentation
├── 09_explanation_stability/               # Axis 5: Explanation stability (XAI)
│   ├── explanation_stability_colab.ipynb   # Tree SHAP rank stability notebook
│   ├── figures/                            # Vector PDF reliability gap plots
│   ├── results/                            # Spearman rank correlation tables
│   └── README.md                           # Axis documentation
├── 10_framework_formalization/             # Axis 6: Unified audit & alert budgeting
│   ├── 14_lcorf_bootstrap_alert_profile_colab.ipynb # 1,000-bootstrap notebook
│   ├── figures/                            # Final multi-axis audit PDF heatmaps
│   ├── results/                            # Consolidated profiles & budgets
│   └── README.md                           # Module documentation
├── requirements.txt                        # Environment dependencies
├── LICENSE                                 # MIT License
└── README.md                               # Repository documentation
```

---

## ⚖️ Responsible Research Claim Boundaries

* 🚫 **No Classifier SOTA Claims:** We do not claim LightGBM or XGBoost are superior classifiers. Our contribution is the **operational audit framework**.
* 🚫 **No Universal Drift Claims:** Measured temporal drops reflect the tested benchmark protocol, not universal bank transaction dynamics.
* 🚫 **No Causal XAI Claims:** The *Explanation Reliability Gap* measures empirical rank divergence; it does not validate causal explanations.
* ✅ **Unbiased Reporting:** Robust, Fragile, and Inconclusive outcomes are reported with equal scientific weight.

---

## 📚 Citation

If you utilize this framework, evaluation suite, or audit methodology in your research, please cite:

```bibtex
@article{haider2026lcorf,
  title={{LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection}},
  author={Haider, Hasnain and Mushtaq, Waseem and Abbas, Qaiser and Al Hassan, Adnan Nadeem and Alshanqiti, Abdullah and Albouq, Sami},
  year={2026},
  url={https://github.com/Hasnain006-nain/lc-orf-financial-fraud-robustness}
}
```

---

## 📜 License

This research framework and reproducibility package is open-source under the [MIT License](LICENSE).
