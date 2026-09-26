# Related Work Gap Analysis For LC-ORF

## Purpose

This note explains how the related-work matrix should be used in the manuscript. The goal is not to attack prior work. The goal is to show a clean technical gap: existing studies cover important pieces of fraud-model evaluation, but they usually do not combine leakage control, temporal evaluation, prevalence stress, calibration, explanation reliability, and alert-budget behavior into one auditable profile.

## Matrix Location

Main table source:

- `01_main_paper_assets/tables/table09_related_work_matrix.csv`

## Main Gap Statement

Prior work gives strong foundations for fraud detection, class imbalance, leakage, concept drift, probability calibration, explainable AI, and cost-sensitive decision-making. However, these strands are usually evaluated separately. LC-ORF contributes a unified operational robustness audit in which the same model family is evaluated under controlled scenario shifts and summarized through a final audit profile.

## What Prior Work Already Covers

### Fraud Detection Foundations

Bolton and Hand provide the classical statistical-fraud-detection foundation. Dal Pozzolo et al. and Bahnsen et al. show that real card-fraud systems face imbalance, non-stationarity, feature-engineering, and cost-sensitive assessment issues.

Use these works to show that the problem is real and technically difficult.

### Leakage

Kaufman, Rosset, and Perlich define leakage as a serious evaluation failure mode in data mining. LC-ORF uses this foundation but applies it directly to fraud-detection protocols through strict and unsafe stress scenarios.

Use this to justify why leakage control is not a cosmetic detail.

### Temporal Shift

Gama et al. cover concept drift broadly. Dal Pozzolo et al. discuss non-stationarity from a card-fraud perspective. LC-ORF operationalizes this concern through chronological stress testing and D2 drift diagnostics.

Use this to justify why random splits are not enough.

### Class Imbalance And Prevalence

Chawla et al. establish SMOTE as a key imbalance method. Davis and Goadrich, plus Saito and Rehmsmeier, justify precision-recall and average-precision style evaluation under skewed classes. LC-ORF adds prevalence stress to show that fraud-rate assumptions alter operational conclusions.

Use this to explain why prevalence sensitivity belongs in the paper.

### Calibration

Platt, Niculescu-Mizil and Caruana, and Guo et al. establish calibration as a separate reliability concern. LC-ORF includes calibration as one axis rather than treating it as an isolated post-processing step.

Use this to defend the calibration/recalibration milestone.

### Explanations

Ribeiro et al. and Lundberg and Lee support post-hoc explanation methods. Lipton, Adebayo et al., and Alvarez-Melis and Jaakkola support caution: explanations require validation and can be unstable or misleading. LC-ORF uses this basis to report an artifact-level explanation reliability gap.

Use this section carefully. Do not claim causal explanation validation.

### Alert Budget And Cost

Elkan and Bahnsen et al. support cost-sensitive evaluation. LC-ORF extends this into alert-budget summaries so the paper is not only about aggregate metrics.

Use this to connect model scores with fraud-investigation workload.

## Strong Manuscript Paragraph

Existing fraud-detection research has examined many of the individual risks addressed in this paper. Prior studies discuss class imbalance, non-stationarity, cost-sensitive decisions, leakage, calibration, and post-hoc explanations. These contributions are essential, but they are usually reported as separate methodological concerns. LC-ORF differs by treating them as coordinated audit axes: for each dataset, model, seed, and scenario pair, it records metric deltas, uncertainty intervals, alert-budget behavior, and explanation-reliability evidence in a final profile. The framework therefore shifts the evaluation question from whether a model obtains a high score under one protocol to how its conclusions change when operational assumptions are perturbed.

## Table Usage Recommendation

Use `table09_related_work_matrix.csv` as a compact related-work table if page budget allows. If the table is too wide for the main paper, include a reduced version with these columns:

- reference
- fraud_detection
- leakage_control
- temporal_protocol
- prevalence_shift
- calibration
- explanation_stability
- alert_budget
- unified_audit_profile

Move the full matrix to supplementary material.

## No-Sugarcoating Assessment

This matrix helps novelty framing, but it does not automatically prove acceptance-level novelty. The manuscript still needs a strong framework section with definitions, scenario-pair notation, delta formulas, bootstrap interpretation, and careful claim boundaries. Without that formal method section, the related work alone will not save the paper.
