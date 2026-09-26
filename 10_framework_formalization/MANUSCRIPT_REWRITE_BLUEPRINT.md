# Manuscript Rewrite Blueprint for IEEE Access

## Recommended Title Options

Preferred:

**A Leakage-Controlled Operational Robustness Framework for Explainable Financial Fraud Detection Across Heterogeneous Transaction Datasets**

Shorter option:

**Leakage-Controlled Robustness Evaluation for Explainable Financial Fraud Detection**

More technical option:

**Beyond Model Comparison: Leakage, Robustness, Calibration, and Explanation Stability in Financial Fraud Detection**

Avoid the current title style if it sounds like a generic multi-model benchmark.

## New Abstract Structure

The abstract should follow this order:

1. Problem:
   Fraud-detection studies often report high performance under evaluation protocols that may be sensitive to leakage, random splits, prevalence assumptions, calibration quality, and explanation instability.

2. Gap:
   Existing benchmark-style studies often compare models but do not systematically quantify how operational evaluation choices affect reported performance and interpretability.

3. Method:
   Introduce LC-ORF, a leakage-controlled operational robustness framework with feature governance and five stress-test indices.

4. Datasets and models:
   Three heterogeneous fraud datasets, strict feature sets, XGBoost and LightGBM as primary tabular baselines, five random seeds.

5. Results:
   Include only headline evidence:
   - Leakage inflated AP and MCC under unsafe protocols.
   - D2 chronological AP dropped strongly relative to random splits.
   - Precision and cost were sensitive to fraud prevalence.
   - Isotonic recalibration improved Brier/ECE across dataset/model pairs.
   - Explanation stability was high in D2/D3 and protocol-sensitive in D1.

6. Conclusion:
   The framework provides a reproducible way to stress-test fraud-detection claims before deployment-oriented interpretation.

## Contribution Bullets

Use five contribution bullets:

1. **Feature-governed evaluation protocol:** A column-level governance process separates strict scoring-time features from identifiers, post-transaction fields, and leakage-risk variables.

2. **Leakage inflation quantification:** A Leakage Inflation Index measures how unsafe oversampling and ledger-state features inflate reported fraud-detection performance.

3. **Operational robustness stress tests:** Temporal Robustness Drop and Prevalence Sensitivity Index quantify sensitivity to chronological deployment and fraud-rate shift.

4. **Probability-quality analysis:** Calibration Improvement Index evaluates whether validation-set Platt and isotonic recalibration improve probability quality beyond ranking metrics.

5. **Explanation stability analysis:** Explanation Instability Index measures whether model-native feature-importance explanations remain stable across seeds and evaluation protocols.

Do not list "we compared many models" as a main contribution.

## Revised Paper Outline

### I. Introduction

Needed message:

- Fraud-detection models are often evaluated as static classifiers.
- In practice, fraud detection is an operational decision system.
- Evaluation can be distorted by leakage, random splits, changing fraud rates, miscalibration, and unstable explanations.
- This paper proposes LC-ORF to make these risks measurable.

End the introduction with the five contributions above.

### II. Related Work

Recommended subsections:

1. Machine learning for financial fraud detection.
2. Data leakage and evaluation bias in imbalanced classification.
3. Temporal validation and prevalence shift.
4. Calibration and thresholding in risk scoring.
5. Explainability and explanation stability.

The related work must show that the novelty is integration and measurement of operational stress, not invention of tree ensembles.

### III. Datasets and Feature Governance

Include:

- D1/D2/D3 overview table.
- Fraud rates.
- Strict feature-set definition.
- Excluded identifier/leakage columns.
- D3 ledger-state fields treated only as a stress scenario.

### IV. Proposed Framework

Present LC-ORF as a pipeline:

1. Dataset audit.
2. Feature governance.
3. Strict training protocol.
4. Leakage stress.
5. Temporal stress.
6. Prevalence stress.
7. Calibration stress.
8. Explanation stability stress.

This section should include equations for:

- LII
- TRD
- PSI
- CII
- EII

### V. Experimental Setup

Include:

- Models: XGBoost and LightGBM as primary models for stress tests.
- Seeds: `42, 101, 202, 303, 404`.
- Metrics: AP, MCC, Brier, ECE, cost per 10,000, Top-K Jaccard.
- Hardware/runtime: Colab T4 is acceptable for reproducibility notes, but do not make it a central claim.
- Saved CSV-backed output policy.

### VI. Results

Recommended result order:

1. Dataset audit and feature governance.
2. Leakage inflation results.
3. Temporal robustness results.
4. Prevalence sensitivity results.
5. Calibration/recalibration results.
6. Explanation stability results.

Each subsection should end with one short interpretation paragraph.

### VII. Discussion

Main points:

- Random high performance is not enough.
- D2 temporal drop shows realistic deployment evaluation can be much harder.
- D3 leakage stress shows post-transaction fields can inflate results.
- Calibration improves probability quality but does not automatically minimize operational cost.
- Explanations can be stable or unstable depending on dataset/protocol.

### VIII. Threats to Validity and Limitations

Must include:

- D1 uses anonymized elapsed time, so temporal results are pseudo-temporal.
- D3 is synthetic and capped to 1,000,000 rows in some stress tests.
- Model-native feature importance is not causal explanation.
- Cost ratio is a transparent stress assumption, not a bank-specific financial loss model.
- Datasets do not represent every fraud domain.

### IX. Conclusion

Conclude that LC-ORF helps evaluate fraud-detection claims under leakage, temporal, prevalence, calibration, and explanation-stability stress.

## Suggested Abstract Draft

Financial fraud-detection studies often report high predictive performance under evaluation settings that may not reflect deployment constraints. In particular, feature leakage, random train-test splitting, changing fraud prevalence, uncalibrated probabilities, and unstable explanations can distort conclusions about model reliability. This paper proposes LC-ORF, a leakage-controlled operational robustness framework for explainable financial fraud detection across heterogeneous transaction datasets. The framework combines column-level feature governance with five stress-test indices: Leakage Inflation Index, Temporal Robustness Drop, Prevalence Sensitivity Index, Calibration Improvement Index, and Explanation Instability Index. Using three fraud datasets and strict scoring-time feature sets, we evaluate XGBoost and LightGBM across five random seeds. The results show that unsafe oversampling before splitting and ledger-state features can inflate AP and MCC; chronological evaluation substantially reduces AP on the real transaction dataset D2; precision and operating cost vary strongly under fraud-prevalence shift; isotonic recalibration consistently improves Brier score and expected calibration error; and explanation stability is dataset-dependent, with D2 and D3 showing stable top feature rankings while D1 remains protocol-sensitive. These findings show that fraud-detection conclusions depend on evaluation protocol as much as model choice, and that reproducible robustness testing is necessary before interpreting predictive and explanatory performance.

