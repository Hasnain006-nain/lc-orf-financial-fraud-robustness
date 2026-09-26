LC-ORF GitHub reviewer package

This folder is intended for a reviewer-facing repository or archive.

Included:

- dataset audit and feature-governance summaries
- leakage, temporal, prevalence, calibration, and explanation notebooks
- result CSV files and exported audit artifacts
- manuscript source and supplementary assets
- reference-verification and project-status notes
- dataset-access notes

Not included:

- raw source datasets from the Datasets folder

Reason:

The raw public CSV files are large:

- creditcard.csv: about 151 MB
- fraudTest.csv: about 150 MB
- PS.csv: about 494 MB

These files are not suitable for ordinary GitHub upload. Reviewers should download them from the public sources cited in the manuscript, then use the feature-governance and artifact workflow provided here.

Recommended repository structure:

- Keep notebooks and result CSV artifacts.
- Keep supplementary tables and figures.
- Add public dataset links in the repository README.
- Do not commit large raw datasets unless using Git LFS or an external artifact store.
