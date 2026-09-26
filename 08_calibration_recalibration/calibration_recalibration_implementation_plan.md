# Calibration and Recalibration Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Colab T4 notebook that tests whether strict fraud-detection model probability scores are calibrated and whether validation-set recalibration improves deployment metrics.

**Architecture:** The notebook trains XGBoost and LightGBM once per dataset and seed using strict leakage-safe features. It reserves a calibration/validation split, fits Platt sigmoid and isotonic recalibrators on validation scores, then evaluates raw and recalibrated probabilities on a held-out test set. It saves per-run checkpoints, summary CSVs, calibration improvement indices, and 600-DPI figures.

**Tech Stack:** Google Colab, pandas, numpy, scikit-learn, XGBoost, LightGBM, seaborn, matplotlib.

## Global Constraints

- Use `PROJECT_ROOT = Path('/content/drive/MyDrive/Credit__')`.
- Use strict leakage-safe feature sets only.
- Do not add ledger-state or identifier-risk features.
- Use seeds `[42, 101, 202, 303, 404]`.
- Save all outputs under `08_calibration_recalibration/calibration_recalibration_v1/`.
- Export PNG and PDF figures at 600 DPI.
- Existing checkpoints must be skipped on rerun.

---

### Task 1: Notebook Builder

**Files:**
- Create: `work/build_colab_calibration_recalibration_notebook.py`
- Create: `C:\Users\Admin\Documents\Codex\Credit__\08_calibration_recalibration\calibration_recalibration_colab.ipynb`
- Create: `C:\Users\Admin\Documents\Codex\Credit__\08_calibration_recalibration\README.md`

**Interfaces:**
- Produces a valid Jupyter notebook.
- Produces a README with runtime, output files, and interpretation notes.

- [x] Write notebook builder with Drive paths, dependencies, loaders, strict feature sets, models, recalibrators, calibration metrics, summaries, figures, and run summary.
- [x] Generate notebook and README.
- [x] Validate notebook JSON and key strings.

### Task 2: Project Status Update

**Files:**
- Modify: `C:\Users\Admin\Documents\Codex\Credit__\PROJECT_STATUS.md`

**Interfaces:**
- Produces a current milestone section for Milestone 08.

- [x] Replace Next Milestone text with Calibration and Recalibration instructions.
- [x] Include outputs and paper interpretation.

### Task 3: User-Facing Copy

**Files:**
- Create copy: `C:\Users\Admin\Documents\Codex\2026-09-23\dear-mr-haider-i-am-writing\outputs\calibration_recalibration\calibration_recalibration_colab.ipynb`
- Create copy: `C:\Users\Admin\Documents\Codex\2026-09-23\dear-mr-haider-i-am-writing\outputs\calibration_recalibration\README.md`

**Interfaces:**
- Produces output copies that match the master project files.

- [x] Copy notebook and README to the task outputs folder.
- [x] Verify copied notebook hash matches master notebook hash.
