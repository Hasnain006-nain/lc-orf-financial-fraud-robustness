# LC-ORF Novelty Specification v1

## Purpose

LC-ORF is specified as a counterfactual operational audit protocol. It changes one deployment assumption at a time, measures the resulting metric delta with paired uncertainty intervals, and records the predictive, probabilistic, operational, and explanation-level consequence in a traceable audit profile.

The contribution is therefore the audit procedure and evidence representation, not a new classifier, a new explanation algorithm, or a universal guarantee of deployment performance.

## Audit Record

Every reference/perturbed comparison must produce one or more rows with these fields:

| Field | Meaning |
|---|---|
| `dataset` | D1, D2, or D3. |
| `model` | XGBoost or LightGBM. |
| `reference_scenario` | Strict, random, raw, or the protocol-specific reference condition. |
| `perturbed_scenario` | Unsafe, chronological, prevalence-shifted, calibrated, or explanation comparison condition. |
| `changed_assumption` | The single deployment assumption changed by the comparison. |
| `metric` | AP, MCC, precision, recall, Brier, ECE, cost, alert-budget precision/recall, Jaccard, or rank correlation. |
| `delta` | Perturbed metric minus reference metric, using the stated direction convention. |
| `ci_low`, `ci_high` | Paired stratified-bootstrap 95% interval when predictions support resampling. |
| `operational_delta` | Change in fixed-alert precision, recall, false alerts, or cost when available. |
| `interpretation` | `robust`, `fragile`, or `inconclusive`. |
| `artifact_id` | Stable identifier for the source CSV, notebook, and figure. |

## Pre-Registered Practical-Effect Thresholds

The following thresholds are screening rules for this study. They are not universal regulatory limits and are not tuned after observing results.

| Quantity | Practically material absolute change |
|---|---:|
| Average precision | 0.020 |
| MCC | 0.050 |
| Precision or recall | 0.050 |
| Brier score | 0.005 |
| ECE | 0.020 |
| Cost per 10,000 transactions | 100 units or 10% of the reference cost, whichever is larger |
| Top-$k$ Jaccard / EII | 0.200 |
| Spearman explanation-rank correlation | 0.200 decrease from the reference |
| Fixed-alert precision or recall | 0.050 |

For a metric with lower-is-better interpretation, the practical threshold is applied to the absolute delta while the manuscript preserves the signed delta. For cost, the percentage rule prevents a fixed threshold from dominating very small reference costs.

## Interpretation Rule

- `robust`: the 95% interval is fully contained within the practically negligible region defined by the metric threshold.
- `fragile`: the 95% interval is separated from zero in a direction that exceeds the practical-effect threshold.
- `inconclusive`: the interval crosses zero, crosses the practical-effect boundary, or cannot be estimated because the source artifact lacks the required paired predictions.

An interval that is statistically different from zero but smaller than the practical threshold is not labeled fragile. Conversely, a practically large point estimate with a wide interval is not labeled fragile; it is labeled inconclusive until the evidence is sufficiently precise.

## Scenario Pairing

The audit uses these one-change comparisons:

| Audit axis | Reference | Perturbation | Main index |
|---|---|---|---|
| Availability and resampling | Strict protocol | Unsafe SMOTE-before-split or D3 ledger-state fields | LII |
| Temporal ordering | Random stratified test | Chronological test | TRD |
| Prevalence | Original test stream | Frozen-model target prevalence stream | PSI |
| Probability quality | Raw score | Validation-fitted sigmoid or isotonic mapping | CII |
| Explanation stability | Reference seed/protocol | Alternate seed/protocol and reliance method | EII plus reliability gap |

## Claim Boundary

The paper may claim that LC-ORF makes protocol sensitivity measurable and auditable on the evaluated datasets. It may not claim that the framework is the first such idea worldwide, that any one threshold is institutionally universal, or that public-dataset results guarantee production performance.

## Exit Test

Task 1 is complete only when the thresholds are frozen, every audit-record field is defined, the one-change scenario pairs are listed, and no result has been used to choose an interpretation rule.
