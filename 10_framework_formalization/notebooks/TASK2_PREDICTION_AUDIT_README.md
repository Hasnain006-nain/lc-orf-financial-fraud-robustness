# Task 2 Prediction Artifact Audit

Run `10_task2_prediction_artifact_audit_colab.ipynb` in Google Colab before bootstrap.

What it does:

- mounts Google Drive;
- uses `/content/drive/MyDrive/Credit__`;
- scans milestones 03, 06, 07, 08, and 09 for CSV artifacts;
- checks whether any CSV has raw prediction columns needed for paired bootstrap;
- saves `prediction_artifact_audit.csv` and `prediction_artifact_audit_summary.csv` in `Credit__/10_framework_formalization/results`;
- provides the exact `save_prediction_export(...)` helper and calls to add to old experiment notebooks.

Strict rule: do not run paired bootstrap until the audit prints `READY_FOR_BOOTSTRAP = True`.
