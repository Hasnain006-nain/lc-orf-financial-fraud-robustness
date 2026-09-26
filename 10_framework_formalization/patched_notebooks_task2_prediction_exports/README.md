# Task 2 Patched Notebooks: Raw Prediction Exports

These notebooks are copies of the experiment notebooks with raw prediction export added.

Use these files in Colab instead of the old versions. They save row-level prediction CSVs in each experiment's `prediction_exports` folder.

Required output columns:

```text
dataset, model, scenario, seed, split, row_id, y_true, score, threshold
```

Recommended run order:

1. `leakage_stress_multiseed_colab_with_prediction_exports.ipynb`
2. `temporal_robustness_colab_with_prediction_exports.ipynb`
3. `calibration_recalibration_colab_with_prediction_exports.ipynb`
4. `explanation_stability_colab_with_prediction_exports.ipynb`
5. `prevalence_stress_colab_with_prediction_exports.ipynb`
6. Optional legacy/single-seed: `leakage_stress_testing_colab_with_prediction_exports.ipynb`
7. Run `10_task2_prediction_artifact_audit_colab.ipynb` again.

The patched notebooks rerun a completed metric checkpoint if its matching prediction CSV is missing. This is necessary because older runs saved metrics only.

Do not start paired bootstrap until the audit shows `PASS_RAW_PREDICTION_SCHEMA` and `READY_FOR_BOOTSTRAP = True`.
