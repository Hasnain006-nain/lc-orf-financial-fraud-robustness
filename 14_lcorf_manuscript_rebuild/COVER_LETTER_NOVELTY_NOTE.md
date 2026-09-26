Dear Editor,

We submit the manuscript "LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection" for consideration in IEEE Access.

The manuscript does not claim a new fraud classifier. Its contribution is an evaluation framework for fraud-detection claims. LC-ORF treats evaluation design as part of the scientific claim by testing controlled scenario pairs across six operational axes: leakage, temporal robustness, prevalence sensitivity, calibration behavior, explanation reliability, and alert-budget behavior.

The main novelty is the unified claim-audit profile. For each scenario pair, the framework records metric direction, materiality thresholds, uncertainty labels, evidence type, saved prediction artifacts, and explicit claim boundaries. This lets a reader distinguish robust, fragile, and inconclusive conclusions instead of relying on one leaderboard-style model score.

The study instantiates LC-ORF on three public fraud datasets using LightGBM and XGBoost across five random seeds. The evidence shows that unsafe preprocessing can inflate measured performance, chronological evaluation can materially reduce apparent skill, prevalence changes can alter operational metrics, and explanation rankings can remain stable even when predictive behavior changes. These findings support the need for operational robustness auditing in financial fraud detection.

We have kept the manuscript's claims bounded. The paper does not claim state-of-the-art fraud detection, universal deployment robustness, or causal explanation validation. Instead, it provides an auditable framework and artifact workflow that other researchers can reuse with different models, datasets, and institution-specific operating assumptions.

Sincerely,

Hasnain Haider
