# Prevalence Stress Test Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Colab T4 notebook that tests whether strict fraud-detection models remain stable when the fraud prevalence in the test stream changes.

**Architecture:** The notebook trains XGBoost and LightGBM once per dataset and seed using leakage-safe strict features. It chooses one cost-sensitive threshold on the natural validation set, then evaluates the fixed model and fixed threshold on prevalence-resampled test sets. Every checkpoint, result, summary, log, and 600-DPI figure is saved to Google Drive.

**Tech Stack:** Google Colab, pandas, numpy, scikit-learn, XGBoost, LightGBM, seaborn, matplotlib.

## Global Constraints

- Use `PROJECT_ROOT = Path('/content/drive/MyDrive/Credit__')`.
- Use strict leakage-safe feature sets only.
- Do not add ledger-state or identifier-risk features.
- Use seeds `[42, 101, 202, 303, 404]`.
- Save all outputs under `07_prevalence_stress_test/prevalence_stress_v1/`.
- Export PNG and PDF figures at 600 DPI.
- Existing checkpoints must be skipped on rerun.

---

### Task 1: Notebook Builder

**Files:**
- Create: `work/build_colab_prevalence_stress_notebook.py`
- Create: `C:\Users\Admin\Documents\Codex\Credit__\07_prevalence_stress_test\prevalence_stress_colab.ipynb`
- Create: `C:\Users\Admin\Documents\Codex\Credit__\07_prevalence_stress_test\README.md`

**Interfaces:**
- Produces a valid Jupyter notebook with 14 cells.
- Produces a README with runtime, output files, and interpretation notes.

- [x] Write notebook builder with Drive paths, dependencies, loaders, models, prevalence resampling, summaries, figures, and run summary.
- [x] Generate notebook and README.
- [x] Validate notebook JSON and key strings.

### Task 2: Project Status Update

**Files:**
- Modify: `C:\Users\Admin\Documents\Codex\Credit__\PROJECT_STATUS.md`

**Interfaces:**
- Produces a current milestone section for Milestone 07.

- [x] Replace Next Milestone text with Prevalence Stress Test instructions.
- [x] Include outputs and paper interpretation.

### Task 3: User-Facing Copy

**Files:**
- Create copy: `C:\Users\Admin\Documents\Codex\2026-09-23\dear-mr-haider-i-am-writing\outputs\prevalence_stress\prevalence_stress_colab.ipynb`
- Create copy: `C:\Users\Admin\Documents\Codex\2026-09-23\dear-mr-haider-i-am-writing\outputs\prevalence_stress\README.md`

**Interfaces:**
- Produces output copies that match the master project files.

- [x] Copy notebook and README to the task outputs folder.
- [x] Verify copied notebook hash matches master notebook hash.
