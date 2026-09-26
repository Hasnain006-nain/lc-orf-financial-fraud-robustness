# Prevalence Stress Notebook

Notebook: `prevalence_stress_colab.ipynb`

Purpose:

- Test whether strict fraud detectors remain stable when the fraud rate in the test stream changes.
- Train once on natural training data.
- Select one cost-sensitive threshold on natural validation data.
- Evaluate the fixed model and fixed threshold across multiple target fraud prevalences.

Expected Colab T4 runtime:

- About 35-70 minutes for the full five-seed run.
- If Google Drive is slow, allow up to 90 minutes.

Outputs:

- `results/prevalence_stress_results.csv`
- `results/prevalence_sensitivity_index.csv`
- `results/prevalence_stress_summary_by_prevalence.csv`
- `results/prevalence_sensitivity_summary.csv`
- 600-DPI PNG/PDF figures under `figures/`
- `run_summary.json`
- `logs/run.log`

Resume behavior:

- Rerun from the top after disconnect.
- Existing seed/dataset/model checkpoint CSVs are skipped.

Paper interpretation:

- Precision and cost are expected to be highly prevalence-sensitive.
- The trained model and threshold are intentionally fixed, so changes reflect operating-environment shift rather than retraining.
- This milestone supports the paper's operational robustness framework.
