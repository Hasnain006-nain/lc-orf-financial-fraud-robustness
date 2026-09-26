# LC-ORF Methodology Formalization

## Purpose

This file defines LC-ORF in manuscript-ready terms. It should be used to rewrite the Framework, Experimental Design, and Results Overview sections.

## Framework Definition

LC-ORF is a leakage-controlled operational robustness framework for fraud-detection evaluation. It does not introduce a new classifier. It defines a protocol for comparing model behavior under controlled changes in evaluation assumptions.

Each audit record is indexed by:

- dataset `d in D`
- model family `m in M`
- random seed `s in S`
- audit axis `a in A`
- reference scenario `c0`
- perturbed scenario `c1`
- metric `k in K`

The final audit profile stores one row for each aggregated axis-dataset-model-scenario-metric combination.

## Audit Axes

LC-ORF uses these axes:

1. `leakage`: compares strict leakage-controlled evaluation with unsafe leakage-prone variants.
2. `temporal`: compares random stratified evaluation with chronological evaluation.
3. `prevalence`: evaluates fixed models and thresholds under altered fraud-rate composition.
4. `calibration`: compares raw scores with Platt-sigmoid and isotonic recalibration.
5. `explanation_protocol`: compares explanation stability and predictive behavior across protocol changes.
6. `alert_budget`: evaluates model behavior under fixed investigation budgets.
7. `explanation_reliability_gap`: reports a proxy for disagreement between predictive fragility and explanation-rank instability.

## Scenario Delta

For each metric `k`, LC-ORF defines the scenario delta as:

```tex
\Delta_{a,d,m,s,k}
= Q_k(d,m,s,c_1) - Q_k(d,m,s,c_0),
```

where `c0` is the reference scenario and `c1` is the perturbed scenario.

This sign convention is important:

- Positive leakage deltas mean the unsafe protocol increased the measured metric relative to the strict protocol.
- Negative temporal deltas mean chronological evaluation reduced the measured metric relative to random stratified evaluation.
- For lower-is-better metrics such as Brier score, ECE, and cost, the sign must be interpreted with the metric direction in mind.

## Metric Direction

Higher is better:

- average precision
- MCC
- precision
- recall

Lower is better:

- Brier score
- ECE
- cost per 10,000 transactions

The paper should report raw deltas, but the discussion must interpret whether a change is beneficial or harmful according to the metric direction.

## Bootstrap Intervals

For leakage, temporal, calibration, and explanation-protocol comparisons, LC-ORF estimates uncertainty using `B = 1000` bootstrap replicates.

When predictions share row-level alignment, LC-ORF uses paired bootstrap resampling. When row-level alignment is unavailable, it uses stratified unpaired resampling to preserve the fraud/non-fraud label composition within each scenario.

For each bootstrap replicate `b`, the method computes:

```tex
\Delta^{(b)}_{a,d,m,s,k}
= Q_k^{(b)}(d,m,s,c_1) - Q_k^{(b)}(d,m,s,c_0).
```

The confidence interval is:

```tex
CI_{a,d,m,s,k}
= \left[
P_{2.5}\left(\Delta^{(1:B)}_{a,d,m,s,k}\right),
P_{97.5}\left(\Delta^{(1:B)}_{a,d,m,s,k}\right)
\right].
```

Across seeds, the final profile reports:

- mean delta across seeds
- standard deviation across seeds
- median lower bootstrap bound
- median upper bootstrap bound
- minimum number of bootstrap replicates
- bootstrap mode: `paired`, `stratified_unpaired`, `deterministic_resampling_summary`, or `artifact_join`

## Robust, Fragile, And Inconclusive Labels

LC-ORF applies materiality thresholds to avoid treating tiny numerical changes as meaningful.

Let `T_k` be the material threshold for metric `k`.

For bootstrap-backed comparisons:

```tex
\text{robust}
\quad \text{if} \quad
|CI_{\mathrm{low}}| < T_k
\ \text{and}\
|CI_{\mathrm{high}}| < T_k.
```

```tex
\text{fragile}
\quad \text{if} \quad
CI_{\mathrm{low}} > T_k
\ \text{and}\
CI_{\mathrm{high}} > T_k,
```

or

```tex
\text{fragile}
\quad \text{if} \quad
CI_{\mathrm{low}} < -T_k
\ \text{and}\
CI_{\mathrm{high}} < -T_k.
```

All other cases are labeled inconclusive.

The thresholds used in the final audit are:

- average precision: 0.020
- MCC: 0.050
- precision: 0.050
- recall: 0.050
- Brier score: 0.005
- ECE: 0.020
- cost per 10,000: `max(100, 0.10 * abs(reference cost))`

## Prevalence Profile

The prevalence axis uses deterministic resampling summaries rather than paired bootstrap intervals. For each dataset, model, metric, and target prevalence, LC-ORF computes the difference between the metric at the target fraud prevalence and the natural test-stream metric. The final prevalence component records:

- mean delta across target prevalence levels
- worst target prevalence
- maximum absolute delta
- robust or fragile label using the same metric thresholds where applicable

This axis should be described as a prevalence sensitivity profile, not as a new training method.

## Explanation Reliability Gap

The explanation reliability gap is a proxy, not a causal explanation test.

Let:

```tex
EII_{d,m} = 1 - \overline{J}_{d,m}^{(top-k)},
```

where `J` is the top-k Jaccard agreement between explanation feature rankings across the compared protocols. In the final results, `k = 5`.

Let:

```tex
F^{AP}_{d,m}
= \frac{|\Delta^{AP}_{explanation\_protocol,d,m}|}{T_{AP}},
```

where `T_AP = 0.020`.

LC-ORF defines:

```tex
ERG_{d,m} = F^{AP}_{d,m} - EII_{d,m}.
```

The interpretation is:

- `ERG > 1`: predictive shift exceeds explanation-rank instability by at least one AP materiality unit.
- `EII >= 0.200`: explanation-rank instability is detected.
- `F_AP < 1`: predictive shift is not material.

This should be written carefully. It indicates a reliability gap between predictive behavior and explanation-rank movement in the available artifacts. It does not prove that explanations are causally faithful or unfaithful.

## Alert-Budget Evaluation

For alert-budget analysis, LC-ORF ranks transactions by model score and evaluates fixed investigation budgets. The audit reports:

- precision
- recall
- false alerts
- estimated cost

Budgets include fixed alerts per 10,000 transactions and a top-fraction budget. This converts score behavior into operational workload evidence.

## Manuscript Claim Boundary

The methodology section should explicitly say:

LC-ORF is an audit framework. It does not claim to replace model development, prove universal deployment robustness, or validate explanations causally. It gives a reproducible way to measure how conclusions change when evaluation assumptions are perturbed.

## LaTeX Integration

Use `lcorf_methodology_latex_snippet.tex` as a starting point for the Methodology section. The snippet should be edited into `main.tex` after the related-work section.
