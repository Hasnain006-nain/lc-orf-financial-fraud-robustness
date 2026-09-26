# Explanation Stability Notebook

Notebook: `explanation_stability_colab.ipynb`

Purpose:

- Test whether strict model explanations remain stable across random seeds.
- Test whether top feature rankings change between random stratified and chronological evaluation.
- Aggregate transformed one-hot/scaled features back to original governed feature names.
- Report Top-K Jaccard stability, weighted importance overlap, rank correlation, and explanation instability.

Expected Colab T4 runtime:

- About 50-90 minutes for the full five-seed run.
- If Google Drive is slow, allow up to 2 hours.

Outputs:

- `results/explanation_model_metrics.csv`
- `results/feature_importance_rankings.csv`
- `results/seed_explanation_stability_index.csv`
- `results/protocol_explanation_stability_index.csv`
- `results/seed_explanation_stability_summary.csv`
- `results/protocol_explanation_stability_summary.csv`
- `results/top_feature_stability_summary.csv`
- 600-DPI PNG/PDF figures under `figures/`
- `run_summary.json`
- `logs/run.log`

Resume behavior:

- Rerun from the top after disconnect.
- Existing seed/dataset/split/model metric and importance checkpoint CSVs are skipped.

Paper interpretation:

- High Top-K Jaccard means explanations are stable.
- High instability means the paper should avoid overclaiming a single universal explanation.
- Native tree importances are model explanations, not causal explanations.
