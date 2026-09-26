# IEEE Access Framework Formalization

## Working Paper Identity

Recommended framework name:

**LC-ORF: Leakage-Controlled Operational Robustness Framework**

Recommended paper framing:

**This paper does not primarily propose another fraud classifier. It proposes and evaluates a leakage-controlled operational robustness framework for financial fraud detection across heterogeneous datasets.**

The revised manuscript should be built around one central thesis:

> Fraud-detection performance claims are incomplete unless the evaluation protocol controls feature leakage and tests model behavior under temporal shift, fraud-prevalence shift, calibration quality, and explanation stability.

## Novelty Position

The novelty is not that XGBoost, LightGBM, logistic regression, or neural networks can detect fraud. That is already well established.

The upgraded novelty claim is a counterfactual operational audit protocol. The protocol changes one deployment assumption at a time, quantifies the resulting metric delta with paired uncertainty intervals, and records the predictive, probabilistic, operational, and explanation-level consequence in a traceable audit profile.

The audit has six linked components:

1. Column-level feature governance before modeling.
2. Explicit leakage stress testing under unsafe feature and resampling conditions.
3. Multi-seed robustness with paired bootstrap uncertainty instead of one lucky split.
4. Chronological deployment-style evaluation with measurable distribution-shift diagnostics.
5. Prevalence-shift stress testing with fixed models, fixed thresholds, and fixed alert budgets.
6. Probability calibration and recalibration analysis separated from operating-cost analysis.
7. Explanation stability checked against held-out performance reliance where feasible.

This turns the work from a benchmark paper into an operational audit paper. The contribution is not the number of metrics; it is the controlled-change design that links each metric delta to one explicit deployment assumption and preserves uncertainty and artifact traceability.

The practical-effect thresholds and interpretation labels are pre-registered in `novelty_specification_v1.md`. They are study-level screening rules, not universal regulatory limits.

## Dataset Naming

Use compact dataset labels consistently:

- **D1:** European credit-card transactions.
- **D2:** simulated card-present/card-not-present merchant transactions from the fraudTest dataset.
- **D3:** PaySim mobile-money simulation.

The manuscript should explain that D1 is anonymized and D3 is synthetic. D2 provides the strongest real transaction-level temporal robustness evidence.

## Feature Governance Protocol

Define a feature set `F_strict` as:

```latex
F_{\mathrm{strict}} = \{x_j: x_j \text{ is available at scoring time and is not an identifier, label proxy, or post-outcome field}\}.
```

The main result protocol uses only `F_strict`.

Leakage-risk features are not silently included in the primary result. They are moved into stress-test scenarios:

- D1/D2 unsafe oversampling before split.
- D3 post-transaction ledger-state fields.

## Index 1: Leakage Inflation Index

Purpose:

Measure how much an unsafe evaluation condition inflates a metric relative to the strict safe protocol.

Definition:

```latex
\mathrm{LII}_{m,d,s}^{(q)} =
M_q(m,d,s_{\mathrm{unsafe}}) - M_q(m,d,s_{\mathrm{safe}})
```

where:

- `m` is the model.
- `d` is the dataset.
- `s` is the stress scenario.
- `q` is the metric, such as AP or MCC.
- `M_q` is the metric value.

Interpretation:

- Positive `LII` means the unsafe protocol reports higher performance.
- Large positive `LII` indicates strong leakage or evaluation inflation risk.

CSV source:

`03_leakage_stress_testing/received_multiseed_results_20260924/leakage_stress_multiseed_v1/results/leakage_inflation_multiseed_summary.csv`

Headline evidence:

- Unsafe SMOTE-before-split inflated AP by about `0.050` to `0.142`.
- Unsafe SMOTE-before-split inflated MCC by about `0.127` to `0.472`.
- D3 ledger-state fields inflated AP by about `0.017` to `0.022` and MCC by about `0.120` to `0.129`.

## Index 2: Temporal Robustness Drop

Purpose:

Measure how much performance drops when a random stratified split is replaced by chronological evaluation.

Definition:

```latex
\mathrm{TRD}_{m,d}^{(q)} =
M_q(m,d,\mathrm{chronological}) - M_q(m,d,\mathrm{random})
```

Interpretation:

- Negative `TRD` means chronological evaluation is harder than random evaluation.
- The strongest temporal claim should focus on D2.

CSV source:

`06_temporal_robustness/received_results_20260924/06_temporal_robustness/temporal_robustness_v1/results/temporal_robustness_summary.csv`

Headline evidence:

- D2 LightGBM AP dropped from `0.931` to `0.686`, with `TRD_AP = -0.245`.
- D2 XGBoost AP dropped from `0.891` to `0.614`, with `TRD_AP = -0.277`.
- D1 temporal evidence is moderate and should be called pseudo-temporal because D1 uses anonymized elapsed time.
- D3 temporal degradation is weak or mixed.

## Index 3: Prevalence Sensitivity Index

Purpose:

Measure how much metrics shift when fraud prevalence in the test stream changes while the trained model and threshold remain fixed.

Definition:

```latex
\mathrm{PSI}_{m,d}^{(q)} =
\max_{\pi \in \Pi} M_q(m,d,\pi) - \min_{\pi \in \Pi} M_q(m,d,\pi)
```

where `\Pi` is the set of target fraud-prevalence levels.

Interpretation:

- Larger `PSI` means stronger sensitivity to deployment base-rate shift.
- Precision and cost should be emphasized because they changed substantially.

CSV source:

`07_prevalence_stress_test/received_results_20260924/07_prevalence_stress_test/prevalence_stress_v1/results/prevalence_sensitivity_summary.csv`

Headline evidence:

- Precision range reached `0.503` for D2 LightGBM, `0.591` for D1 XGBoost, and `0.592` for D3 LightGBM.
- Cost range reached `423` per 10,000 for D2 XGBoost, `879` to `955` per 10,000 for D3, and more than `1400` per 10,000 for D1 models.

## Index 4: Calibration Improvement Index

Purpose:

Measure whether recalibration improves probability quality relative to raw model scores.

Definitions:

```latex
\mathrm{CII}_{m,d}^{(\mathrm{Brier})} =
\mathrm{Brier}(m,d,\mathrm{raw}) -
\mathrm{Brier}(m,d,\mathrm{calibrated})
```

```latex
\mathrm{CII}_{m,d}^{(\mathrm{ECE})} =
\mathrm{ECE}(m,d,\mathrm{raw}) -
\mathrm{ECE}(m,d,\mathrm{calibrated})
```

Interpretation:

- Positive values mean recalibration improved probability quality.
- Calibration improvement should not be equated with guaranteed cost improvement.

CSV source:

`08_calibration_recalibration/received_results_20260924/08_calibration_recalibration/calibration_recalibration_v1/results/calibration_recalibration_summary.csv`

Headline evidence:

- Isotonic recalibration achieved the best Brier score and best ECE for every dataset/model pair.
- Cost effects were mixed, so the manuscript should separate probability quality from operating-cost optimization.

## Index 5: Explanation Instability Index

Purpose:

Measure whether top feature-importance explanations remain stable across seeds and between evaluation protocols.

Definition:

```latex
\mathrm{EII}_{m,d}^{(k)} =
1 - \frac{|T_k(a) \cap T_k(b)|}{|T_k(a) \cup T_k(b)|}
```

where `T_k(a)` and `T_k(b)` are top-`k` feature sets under two seeds or two protocols.

Interpretation:

- `EII = 0` means identical top-`k` explanations.
- Higher `EII` means explanations are less stable.

CSV source:

`09_explanation_stability/received_results_20260924/09_explanation_stability/explanation_stability_v1/results/protocol_explanation_stability_summary.csv`

Headline evidence:

- D2 and D3 showed protocol-level Top-5 Jaccard of `1.000`, meaning `EII = 0.000`.
- D1 was mixed: LightGBM had `EII = 0.524`; XGBoost had `EII = 0.248`.

## Framework Flow

The methods section should present the framework as a sequence:

1. Dataset truth audit.
2. Feature governance.
3. Strict baseline model training.
4. Leakage stress tests.
5. Temporal stress tests.
6. Prevalence stress tests.
7. Calibration/recalibration analysis.
8. Explanation stability analysis.
9. Claim-bounded interpretation.

## Main Claim

Allowed main claim:

> The proposed framework shows that fraud-detection conclusions depend not only on model choice but also on leakage control, feature availability, temporal ordering, fraud prevalence, probability calibration, and explanation stability.

Avoid claiming:

> The proposed model is the best fraud detector.

The revised paper should argue for better evaluation, not universal model superiority.
