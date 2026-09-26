# Temporal Robustness Notebook

Notebook: `temporal_robustness_colab.ipynb`

Purpose:

- Test whether leakage-safe fraud models remain stable under chronological evaluation.
- Compare `RANDOM_STRATIFIED_SAFE` against `CHRONOLOGICAL_SAFE`.
- Use strict feature governance only.
- Produce Temporal Robustness Drop tables and 600-DPI figures.

Expected Colab T4 runtime:

- About 50-90 minutes for the full five-seed run.
- If Google Drive is slow, allow up to 2 hours.

Outputs:

- `results/temporal_robustness_results.csv`
- `results/temporal_robustness_index.csv`
- `results/temporal_robustness_summary.csv`
- 600-DPI PNG/PDF figures under `figures/`
- `run_summary.json`
- `logs/run.log`

Resume behavior:

- Rerun from the top after disconnect.
- Existing checkpoint CSVs are skipped.

Paper interpretation:

- Negative `trd_average_precision` or `trd_mcc` means chronological testing is harder than random split testing.
- D1 uses anonymized elapsed transaction time, so report it as pseudo-temporal/order robustness.
- D2 and D3 use source transaction/order time fields.
