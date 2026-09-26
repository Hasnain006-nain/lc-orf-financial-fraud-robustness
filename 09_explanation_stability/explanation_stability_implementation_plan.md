# Explanation Stability Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Colab T4 notebook that evaluates whether strict fraud-detection explanations remain stable across seeds and evaluation protocols.

**Architecture:** The notebook trains strict XGBoost and LightGBM models under random stratified and chronological splits. It extracts model-native feature importances, maps transformed one-hot/scaled features back to original governed feature names, normalizes importances, and computes Top-K Jaccard, weighted-overlap, and rank-correlation stability indices across seeds and between protocols.

**Tech Stack:** Google Colab, pandas, numpy, scikit-learn, XGBoost, LightGBM, scipy, seaborn, matplotlib.

## Global Constraints

- Use `PROJECT_ROOT = Path('/content/drive/MyDrive/Credit__')`.
- Use strict leakage-safe feature sets only.
- Do not add ledger-state or identifier-risk features.
- Use seeds `[42, 101, 202, 303, 404]`.
- Save all outputs under `09_explanation_stability/explanation_stability_v1/`.
- Export PNG and PDF figures at 600 DPI.
- Existing checkpoints must be skipped on rerun.

---

### Task 1: Notebook Builder

**Files:**
- Create: `work/build_colab_explanation_stability_notebook.py`
- Create: `C:\Users\Admin\Documents\Codex\Credit__\09_explanation_stability\explanation_stability_colab.ipynb`
- Create: `C:\Users\Admin\Documents\Codex\Credit__\09_explanation_stability\README.md`

**Interfaces:**
- Produces a valid Jupyter notebook.
- Produces a README with runtime, output files, and interpretation notes.

- [x] Write notebook builder with Drive paths, dependencies, loaders, strict feature sets, split protocols, model training, feature-name aggregation, stability metrics, summaries, figures, and run summary.
- [x] Generate notebook and README.
- [x] Validate notebook JSON and key strings.

### Task 2: Project Status Update

**Files:**
- Modify: `C:\Users\Admin\Documents\Codex\Credit__\PROJECT_STATUS.md`

**Interfaces:**
- Produces a current milestone section for Milestone 09.

- [x] Replace Next Milestone text with Explanation Stability instructions.
- [x] Include outputs and paper interpretation.

### Task 3: User-Facing Copy

**Files:**
- Create copy: `C:\Users\Admin\Documents\Codex\2026-09-23\dear-mr-haider-i-am-writing\outputs\explanation_stability\explanation_stability_colab.ipynb`
- Create copy: `C:\Users\Admin\Documents\Codex\2026-09-23\dear-mr-haider-i-am-writing\outputs\explanation_stability\README.md`

**Interfaces:**
- Produces output copies that match the master project files.

- [x] Copy notebook and README to the task outputs folder.
- [x] Verify copied notebook hash matches master notebook hash.
