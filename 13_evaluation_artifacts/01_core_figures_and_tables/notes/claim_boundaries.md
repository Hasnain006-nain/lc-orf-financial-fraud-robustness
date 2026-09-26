# LC-ORF Claim Boundaries

This file defines what the paper is allowed to say and what it must avoid. Use it while rewriting the manuscript.

## Safe Claims

### Framework Claim

Safe:

LC-ORF is a framework for auditing operational robustness in fraud-detection evaluation.

Avoid:

LC-ORF is a new fraud-detection algorithm.

### Leakage Claim

Safe:

The leakage stress tests show that unsafe protocol choices can inflate measured fraud-detection performance.

Avoid:

All prior fraud-detection results are invalid because of leakage.

### Temporal Claim

Safe:

The chronological protocol reveals degradation that is partly hidden under random stratified evaluation, especially in `D2_fraudTest`.

Avoid:

The model will fail in every real deployment.

### Prevalence Claim

Safe:

The prevalence stress profile shows that precision, MCC, and operating cost are sensitive to fraud-rate assumptions.

Avoid:

The model is robust to all prevalence shifts.

### Calibration Claim

Safe:

Calibration changes probability quality and can affect operational costs, but its benefits vary by dataset, model, and metric.

Avoid:

Calibration always improves the model.

### Explanation Claim

Safe:

The explanation reliability gap is an artifact-level proxy showing when explanation-rank stability and predictive behavior tell different stories.

Avoid:

The paper proves SHAP explanations are causally correct or causally wrong.

### Alert-Budget Claim

Safe:

Alert-budget summaries translate score behavior into operational workload measures such as precision, recall, false alerts, and cost under fixed budgets.

Avoid:

The paper gives an optimized fraud-investigation policy for banks.

## Red-Flag Words To Avoid

Avoid these unless directly supported by evidence:

- state-of-the-art
- universal
- guaranteed
- proves
- eliminates leakage
- fully robust
- deployment-ready
- real-time banking solution
- causal explanation
- perfect interpretability

## Better Phrases

Use:

- evaluates
- audits
- measures
- reports
- indicates
- suggests
- under the studied protocols
- in these benchmark settings
- artifact-level proxy
- operational robustness profile

## Required Limitation Statements

The final paper must include these limitations:

1. The study uses three public datasets and does not claim universal coverage of banking environments.
2. The framework audits selected operational assumptions; it does not cover every deployment risk.
3. The explanation reliability gap is a proxy derived from existing prediction and explanation artifacts, not a causal test of explanation faithfulness.
4. Alert-budget results depend on the chosen budget levels and cost assumptions.
5. Public fraud datasets may not capture all institutional, regulatory, and adversarial conditions of production systems.

## Reviewer Trap Checks

Before submission, check every section against these questions:

1. Does the section accidentally make LC-ORF sound like a classifier?
2. Does any sentence imply state-of-the-art performance?
3. Does the explanation section overclaim causality?
4. Does the D2 drift section admit that the evidence is dataset-specific?
5. Does every novelty claim point to a figure, table, or formal definition?
6. Are mixed findings presented honestly rather than hidden?

## Final Submission Rule

If a claim cannot be tied to one of the selected figures, selected tables, formal LC-ORF definitions, or related work matrix, remove it or soften it.
