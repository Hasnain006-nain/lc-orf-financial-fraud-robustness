# Calibration and Recalibration Notebook

Notebook: `calibration_recalibration_colab.ipynb`

Purpose:

- Test probability calibration quality for strict fraud-detection models.
- Compare raw probabilities against validation-set Platt sigmoid and isotonic recalibration.
- Report Brier score, Expected Calibration Error, maximum calibration error, log loss, cost, MCC, and calibration curves.

Expected Colab T4 runtime:

- About 35-75 minutes for the full five-seed run.
- If Google Drive is slow, allow up to 90 minutes.

Outputs:

- `results/calibration_recalibration_results.csv`
- `results/calibration_improvement_index.csv`
- `results/calibration_recalibration_summary.csv`
- `results/calibration_curve_bins.csv`
- 600-DPI PNG/PDF figures under `figures/`
- `run_summary.json`
- `logs/run.log`

Resume behavior:

- Rerun from the top after disconnect.
- Existing seed/dataset/model checkpoint CSVs are skipped.

Paper interpretation:

- Positive Brier/ECE/log-loss reduction means recalibration improved probability quality.
- Cost delta can be positive or negative because recalibration changes thresholded operating behavior.
- Calibration is a separate claim from ranking performance; AP and ROC-AUC may not improve.
