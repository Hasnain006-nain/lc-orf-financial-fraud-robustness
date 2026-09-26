<div align="center">

# 🛡️ LC-ORF
### **A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection**

[![Python Version](https://img.shields.io/badge/Python-3.10%20%7C%203.11-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-LC--ORF-10B981?style=for-the-badge&logo=shield&logoColor=white)](#-framework-architecture)
[![Colab GPU](https://img.shields.io/badge/Colab-GPU%20Ready-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](#-notebook-suite--quickstart)
[![Bootstrap](https://img.shields.io/badge/Audit-1000%20Bootstraps-6366F1?style=for-the-badge)](#-key-empirical-findings)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

<br/>

[**Overview**](#-overview) •
[**Framework Architecture**](#-framework-architecture) •
[**The 6 Audit Axes**](#-the-six-operational-audit-axes) •
[**Key Findings**](#-key-empirical-findings) •
[**Datasets & Governance**](#-datasets--governance) •
[**Colab Suite**](#-notebook-suite--quickstart) •
[**Citation**](#-citation)

---

</div>

## 💡 Overview

In production financial ecosystems, fraud detection models frequently experience catastrophic failure post-deployment. The root cause is a systemic scientific disconnect: **models are routinely evaluated as static leaderboard benchmarks** using single-split metrics (such as ROC-AUC) that completely hide real-world operational vulnerabilities.

**LC-ORF (Leakage-Controlled Operational Robustness Framework)** bridges the gap between laboratory evaluation and operational reality. Instead of treating evaluation as a passive test split, LC-ORF enforces an active, multi-axis operational stress-testing audit protocol.

```
┌──────────────────────────────────────────────┐       ┌──────────────────────────────────────────────┐
│       ❌ Traditional Fraud Evaluation        │       │             ✅ The LC-ORF Paradigm           │
├──────────────────────────────────────────────┤       ├──────────────────────────────────────────────┤
│ • Static random train/test splits            │  ───► │ • Chronological & population-drift audits    │
│ • Resampling/scaling before data splitting   │       │ • Strict leakage-safe feature governance     │
│ • Unchecked SMOTE performance inflation      │       │ • Unsafe vs. safe reference-stress deltas    │
│ • Fixed prevalence base-rate assumptions     │       │ • Deterministic prevalence stress testing    │
│ • Blind trust in static SHAP feature ranks   │       │ • Audit of Explanation Reliability Gaps      │
│ • Theoretical metrics ignoring alert budgets │       │ • Realistic human-analyst review constraints │
└──────────────────────────────────────────────┘       └──────────────────────────────────────────────┘
```

---

## 🏛️ Framework Architecture

<div align="center">
  <img src="assets/fig01_lcorf_framework_workflow.png" alt="LC-ORF Operational Robustness Workflow" width="92%" style="border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);"/>
  <p><em><strong>Figure 1:</strong> LC-ORF operational robustness workflow. Models undergo controlled perturbations across leakage, temporal ordering, base-rate prevalence, calibration, explanation stability, and alert-budget capacity.</em></p>
</div>

The LC-ORF protocol executes in **five standardized stages**:

1. **Stage 1 (Benchmark Ingestion):** Diverse transaction streams spanning card payments, merchant terminals, and mobile money.
2. **Stage 2 (Leakage-Safe Feature Governance):** Systematic removal of transactional identifiers, future variables, and ledger-state balances to establish a leak-free **Strict Main Feature Set**.
3. **Stage 3 (Scenario-Pair Perturbations):** Paired evaluations comparing reference conditions ($c_0$) against targeted stress conditions ($c_1$) across 6 operational axes.
4. **Stage 4 (Artifact & Model Layer):** 5-seed tree-based ensemble training (LightGBM & XGBoost) exporting granular predictions (scores, ground-truth labels, decision thresholds).
5. **Stage 5 (Audit Profile & Significance):** 1,000 paired bootstrap resamples per unit evaluated against metric materiality thresholds to produce auditable **Robust**, **Fragile**, or **Inconclusive** profiles.

---

## 🔬 The Six Operational Audit Axes

LC-ORF formalizes an audit unit as $(d, m, s, a, c_0, c_1, k)$ across datasets $\mathcal{D}$, models $\mathcal{M}$, seeds $\mathcal{S}$, axes $\mathcal{A}$, reference $c_0$, stress $c_1$, and metric $k$:

| Axis | Reference Scenario ($c_0$) | Perturbed Scenario ($c_1$) | Target Operational Vulnerability | Metric Materiality Bound |
| :---: | :--- | :--- | :--- | :---: |
| <img src="https://img.shields.io/badge/Axis_1-Leakage-red?style=flat-square"/> | Safe pipeline inside split | SMOTE-before-split / Post-balance access | Artificially inflated precision & false confidence | $\Delta \text{MCC} \ge +0.05$<br>$\Delta \text{AP} \ge +0.05$ |
| <img src="https://img.shields.io/badge/Axis_2-Temporal-blue?style=flat-square"/> | Random stratified split | Chronological split (Past $\to$ Future) | Real-world concept drift & consumer pattern shift | $\Delta \text{AP} \le -0.05$<br>$\Delta \text{MCC} \le -0.05$ |
| <img src="https://img.shields.io/badge/Axis_3-Prevalence-purple?style=flat-square"/> | Native base rate ($\pi_0$) | Downsampled stream ($\pi \in \{0.01\% \dots 5\%\}$) | False-alarm explosion during seasonal rate changes | Component Fragility Rate |
| <img src="https://img.shields.io/badge/Axis_4-Calibration-orange?style=flat-square"/> | Raw model probabilities | Platt scaling / Isotonic regression | Distortion in automated cutoffs & risk rankings | $\Delta \text{Brier} \le -0.005$<br>$\Delta \text{Cost} \le -0.05$ |
| <img src="https://img.shields.io/badge/Axis_5-Explanation-green?style=flat-square"/> | Random split attributions | Chronological split attributions | Explanation Reliability Gap (Stable ranks $\neq$ Model safety) | $\text{Rank Corr} > 0.85$<br>when $\Delta \text{AP} < -0.15$ |
| <img src="https://img.shields.io/badge/Axis_6-Alert_Budget-yellow?style=flat-square"/> | Unconstrained recall | Top 1%, Top 2%, Top 5% review budget | Real-world fraud detection team capacity bottlenecks | Tier Precision & Capture |

---

## 📈 Key Empirical Findings

Audited across **5 random seeds**, **3 benchmark datasets**, and **1,000 paired bootstrap iterations**:

<div align="center">

### 💥 High-Impact Operational Revelations

</div>

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
 │    Top feature importance rankings remained superficially stable (Spearman rho > 0.90)          │
 │    even when models suffered severe predictive collapse, proving XAI stability does not         │
 │    guarantee model reliability.                                                                 │
 └─────────────────────────────────────────────────────────────────────────────────────────────────┘
```

<details>
<summary><b>🔍 Click to view representative 1,000-replicate bootstrap findings table</b></summary>
<br>

| Axis | Dataset | Model | Metric | Reference | Perturbed | Mean Delta ($\bar{\Delta}$) | Median 95% Bootstrap CI | Outcome |
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

LC-ORF audits three widely recognized financial fraud benchmarks:

| ID | Dataset | Domain | Raw Records | Frauds | Cleaned Records | Feature Governance Highlights |
| :---: | :--- | :--- | :---: | :---: | :---: | :--- |
| **D1** | [ULB Credit Card](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) | European card payments | 284,807 | 492 (0.17%) | **283,726** | Removed 1,081 duplicate transactions |
| **D2** | [Fraud Detection](https://www.kaggle.com/datasets/kartik2112/fraud-detection) | Merchant transactions | 555,719 | 2,145 (0.39%) | **555,719** | Stripped index artifact `Unnamed: 0` and ID `trans_num` |
| **D3** | [PaySim Mobile Money](https://www.kaggle.com/datasets/ealaxi/paysim1) | Mobile payments | 5,840,046 | 4,497 (0.08%) | **5,840,046** | Isolated post-transaction ledger balances (`newbalance*`) |

> [!NOTE]
> **Data Download Policy:** In accordance with academic open-source repository practices, large raw CSV datasets (~800 MB uncompressed) are not committed to git.
> Download the datasets from Kaggle using the links above and place the CSV files (`creditcard.csv`, `fraudTest.csv`, `PS.csv`) directly in `00_source_datasets/`. See [00_source_datasets/README.md](00_source_datasets/README.md) and [00_source_datasets_notes/DATASET_ACCESS_NOTE.md](00_source_datasets_notes/DATASET_ACCESS_NOTE.md).

---

## 💻 Notebook Suite & Quickstart

### 🚀 1. Google Colab (One-Click GPU Execution)

All experiments are organized into standalone notebooks with automated Google Drive checkpointing:

| Milestone / Audit Axis | Colab Notebook | Focus & Deliverable |
| :--- | :---: | :--- |
| **03. Leakage Stress Testing** | [`leakage_stress_multiseed_colab.ipynb`](03_leakage_stress_testing/leakage_stress_multiseed_colab.ipynb) | 5-seed safe vs. unsafe SMOTE & ledger leakage audit |
| **06. Temporal Robustness** | [`temporal_robustness_colab.ipynb`](06_temporal_robustness/temporal_robustness_colab.ipynb) | Chronological vs. random split drift evaluation |
| **07. Prevalence Sensitivity** | [`prevalence_stress_colab.ipynb`](07_prevalence_stress_test/prevalence_stress_colab.ipynb) | Multi-tier deterministic base-rate downsampling |
| **08. Calibration Analysis** | [`calibration_recalibration_colab.ipynb`](08_calibration_recalibration/calibration_recalibration_colab.ipynb) | ECE, Brier score, Platt scaling, and Isotonic regression |
| **09. Explanation Stability** | [`explanation_stability_colab.ipynb`](09_explanation_stability/explanation_stability_colab.ipynb) | Tree SHAP feature rank stability across splits |
| **10. Bootstrap & Alert Profiling** | [`14_lcorf_bootstrap_alert_profile_colab.ipynb`](10_framework_formalization/notebooks/14_lcorf_bootstrap_alert_profile_colab.ipynb) | 1,000 paired bootstrap confidence intervals |

### 🛠️ 2. Local Environment Setup

```bash
# 1. Clone repository
git clone https://github.com/Hasnain006-nain/lc-orf-financial-fraud-robustness.git
cd lc-orf-financial-fraud-robustness

# 2. Create virtual environment
python -m venv venv

# 3. Activate environment
# On Linux / macOS:
source venv/bin/activate
# On Windows (PowerShell):
.\venv\Scripts\Activate.ps1

# 4. Install dependencies
pip install -r requirements.txt
```

---

## 📁 Repository Organization

```
lc-orf-financial-fraud-robustness/
├── assets/                                 # Visual architecture assets (Figure 1)
│   └── fig01_lcorf_framework_workflow.png
├── 00_source_datasets/                     # Local drop folder for raw Kaggle CSVs
├── 00_source_datasets_notes/               # Integrity hashes and verification notes
├── 01_dataset_truth_audit/                 # Duplicate checks, data truth audits
├── 02_feature_governance/                  # Column-by-column governance rules
├── 03_leakage_stress_testing/              # Leakage stress notebooks & checkpoints
├── 06_temporal_robustness/                 # Chronological evaluation notebooks & data
├── 07_prevalence_stress_test/              # Base-rate shift profiles and analysis
├── 08_calibration_recalibration/           # Probability calibration and cost evaluations
├── 09_explanation_stability/               # XAI attribution stability analysis
├── 10_framework_formalization/             # Methodology formalization, bootstrap notebooks
├── 12_github_reproducibility/              # Setup guides & execution pipelines
├── 13_evaluation_artifacts/                # 600-DPI publication figures & result tables
│   ├── 01_core_figures_and_tables/         # Primary benchmark heatmaps and summaries
│   └── 02_extended_results_and_data/       # Full bootstrap result CSVs and manifests
├── requirements.txt                        # Core Python dependencies
├── LICENSE                                 # MIT License
└── README.md                               # Framework documentation
```

---

## 🎯 Traceability to Benchmark Artifacts

All reported metrics are directly traceable to saved CSV artifacts in [13_evaluation_artifacts/](13_evaluation_artifacts/):

| Benchmark Item | Content Description | Source Result Artifact |
| :--- | :--- | :--- |
| **Figure 1** | LC-ORF 5-Stage Framework Workflow | [`assets/fig01_lcorf_framework_workflow.png`](assets/fig01_lcorf_framework_workflow.png) |
| **Figure 2** | Final Multi-Axis Audit Profile Heatmap | `13_evaluation_artifacts/01_core_figures_and_tables/figures/png/fig02_*.png` |
| **Figure 3** | Multi-Seed AP Leakage Inflation Heatmap | `13_evaluation_artifacts/01_core_figures_and_tables/figures/png/fig03_*.png` |
| **Figure 4** | D2 Feature Drift vs. Temporal AP Drop | `13_evaluation_artifacts/01_core_figures_and_tables/figures/png/fig04_*.png` |
| **Figure 5** | Prevalence Profile Sensitivity Heatmap | `13_evaluation_artifacts/01_core_figures_and_tables/figures/png/fig05_*.png` |
| **Figure 6** | Alert Budget Precision by Axis & Dataset | `13_evaluation_artifacts/01_core_figures_and_tables/figures/png/fig06_*.png` |
| **Figure 7** | Explanation Reliability Gap Visualization | `13_evaluation_artifacts/01_core_figures_and_tables/figures/png/fig07_*.png` |
| **Audit Profile** | 1,000-Replicate Paired Bootstrap Deltas | `13_evaluation_artifacts/02_extended_results_and_data/tables/source_results/lcorf_final_audit_profile.csv` |

---

## ⚖️ Responsible Research Claim Boundaries

To ensure scientific transparency, the LC-ORF research framework establishes explicit claim boundaries:

* 🚫 **No Classifier SOTA Claims:** We do not claim LightGBM or XGBoost are superior classifiers. Our contribution is the **operational audit framework**.
* 🚫 **No Universal Drift Claims:** Measured temporal drops reflect the tested benchmark protocol, not universal bank transaction dynamics.
* 🚫 **No Causal XAI Claims:** The *Explanation Reliability Gap* measures rank divergence; it does not validate causal explanations.
* ✅ **Unbiased Reporting:** Robust, Fragile, and Inconclusive outcomes are reported with equal scientific weight.

---

## 📚 Citation

If you utilize this framework, evaluation suite, or audit methodology in your research, please cite:

```bibtex
@article{lcorf2026robustness,
  title={{LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection}},
  author={Haider, Hasnain and Mushtaq, Waseem and Abbas, Qaiser and Al Hassan, Adnan Nadeem and Alshanqiti, Abdullah and Albouq, Sami},
  year={2026},
  journal={arXiv preprint},
  url={https://github.com/Hasnain006-nain/lc-orf-financial-fraud-robustness}
}
```

---

## 📜 License

This research framework and reproducibility package is open-source under the [MIT License](LICENSE).
