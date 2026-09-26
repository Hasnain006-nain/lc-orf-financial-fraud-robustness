# Multi-Seed Leakage Stress Notebook

Notebook: `leakage_stress_multiseed_colab.ipynb`

Purpose:

- Repeat the core leakage/feature-availability stress experiment across five seeds.
- Use XGBoost and LightGBM only.
- Save resumable checkpoints after every seed/dataset/scenario/model result.

Expected Colab T4 runtime:

- About 45-75 minutes for the full run.
- If Google Drive is slow, allow up to 90 minutes.

Outputs:

- `results/leakage_stress_multiseed_results.csv`
- `results/leakage_inflation_multiseed_index.csv`
- `results/leakage_inflation_multiseed_summary.csv`
- 600-DPI PNG/PDF figures under `figures/`

Resume behavior:

- Rerun from the top after disconnect.
- Existing checkpoint CSVs are skipped.
