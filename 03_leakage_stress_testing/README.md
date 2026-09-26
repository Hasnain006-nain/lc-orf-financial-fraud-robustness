# Leakage Stress Testing Notebook

Notebook: `leakage_stress_testing_colab.ipynb`

Purpose:

- Run the first novelty experiment for the revised fraud-detection paper.
- Compare strict safe evaluation against unsafe preprocessing, unsafe SMOTE-before-split, and D3 ledger-state feature stress.
- Save every checkpoint, table, and 600-DPI figure to Google Drive.

Colab instructions:

1. Upload the whole `Credit__` folder to Google Drive.
2. Open `leakage_stress_testing_colab.ipynb` in Colab.
3. Confirm `PROJECT_ROOT = Path('/content/drive/MyDrive/Credit__')` in the configuration cell.
4. Runtime > Change runtime type > T4 GPU.
5. Run all cells.

Resume behavior:

- Each dataset/scenario/model result is saved under `03_leakage_stress_testing/leakage_stress_v1/checkpoints`.
- If Colab disconnects, rerun from the top. Existing checkpoints are skipped.
- Consolidated results are saved in `results/leakage_stress_results.csv`.
- Leakage Inflation Index results are saved in `results/leakage_inflation_index.csv`.
- Figures are saved in both PNG at 600 DPI and PDF.

Main paper rule:

- Use strict safe-pipeline results as the primary result.
- Unsafe scenarios are stress tests only.
- D3 post-transaction balance fields are stress-test features, not main protocol features.
