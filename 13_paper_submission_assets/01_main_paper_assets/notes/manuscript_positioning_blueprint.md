# Manuscript Positioning Blueprint

## Target Identity

The paper should read as an evaluation-framework paper for financial fraud detection, not as a model leaderboard paper.

## Core Message

Fraud detection models can look reliable under one evaluation setup and fragile under another. LC-ORF makes those changes visible by auditing leakage, time, prevalence, calibration, explanation reliability, and alert-budget behavior in one profile.

## Recommended Title Options

1. LC-ORF: A Leakage-Controlled Operational Robustness Framework for Financial Fraud Detection
2. Auditing Operational Robustness in Financial Fraud Detection Through Leakage-Controlled Multi-Axis Evaluation
3. Beyond Model Scores: Leakage-Controlled Operational Robustness Auditing for Financial Fraud Detection

Recommended title: option 1.

## Recommended Abstract Structure

1. One sentence on the evaluation problem.
2. One sentence saying the paper introduces LC-ORF.
3. One sentence listing the six audit axes.
4. One sentence describing datasets, models, seeds, bootstrap intervals, and alert budgets.
5. One sentence with key findings: leakage inflation, D2 temporal degradation, prevalence fragility, and explanation reliability gap.
6. One restrained conclusion: LC-ORF provides an auditable basis for comparing fraud models under changing operational assumptions.

## Recommended Section Structure

1. Introduction
2. Related Work
3. LC-ORF Framework
4. Experimental Design
5. Results
6. Discussion
7. Threats to Validity and Limitations
8. Conclusion

## Main Figures Placement

- Figure 1, LC-ORF workflow: end of Introduction or start of Framework section.
- Figure 2, final audit profile heatmap: start of Results.
- Figure 3, leakage inflation heatmap: Leakage subsection.
- Figure 4, D2 drift versus temporal drop: Temporal subsection.
- Figure 5, prevalence profile heatmap: Prevalence subsection.
- Figure 6, alert-budget precision: Operational subsection.
- Figure 7, explanation reliability gap: Explanation subsection or Discussion if space is tight.

## Main Tables Placement

- Table 1, LC-ORF audit axes: Framework section.
- Table 2, final profile axis summary: Results overview.
- Table 3, key bootstrap findings: Results overview or leakage/temporal subsections.
- Table 4 and Table 5, D2 drift and prevalence by split: Temporal subsection.
- Table 6, explanation reliability gap: Explanation subsection.
- Table 7, alert-budget compact summary: Operational subsection.
- Table 8, prevalence profile component: supplementary if page budget is tight.

## Writing Tone

Use restrained technical language. The paper should sound careful and evidence-driven. Do not use promotional phrases. Strong claims should be carried by tables and figures, not adjectives.

## Highest-Risk Reviewer Objections

1. "This is only another fraud detection comparison."
   Response in paper: Make LC-ORF the central method, and keep model performance secondary.

2. "The novelty is not clear."
   Response in paper: Show the related work matrix and explain that the contribution is a unified operational audit profile.

3. "The explanation analysis is overclaimed."
   Response in paper: Call it an artifact-level reliability proxy and state the limitation.

4. "The datasets are public and limited."
   Response in paper: Present this as a benchmark audit study and state deployment limitations clearly.

5. "There are too many figures."
   Response in paper: Keep five to seven main figures and move the rest to supplementary.

## Immediate Rewrite Priority

Start with the Introduction and Framework sections. If those two sections do not make LC-ORF feel like the real contribution, the rest of the paper will still look like a conventional ML benchmark.
