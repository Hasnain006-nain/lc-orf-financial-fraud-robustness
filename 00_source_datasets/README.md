# Source Datasets Directory

This directory is the local destination for the three public benchmark datasets utilized in the LC-ORF research study.

> **Note on Data Availability & Repository Size Policy:**  
> In accordance with academic reproducibility best practices and repository size limitations, raw transaction datasets are not tracked directly in this repository (uncompressed size ~800 MB). All processed result CSVs, feature governance summaries, prediction-export manifests, and evaluation checkpoints are provided in the respective audit milestone directories.

To reproduce experiments requiring raw data from scratch, please download the datasets from their official public sources and place the uncompressed CSV files in this directory:

| Dataset Identifier | Canonical Filename | Source / Benchmark | Expected Rows | Raw Fraud Rate | Public Access Link |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **D1** | `creditcard.csv` | ULB Machine Learning Group | 284,807 | 0.173% (492) | [Kaggle: Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) |
| **D2** | `fraudTest.csv` | Kartik Shenoy (Merchant Simulation) | 555,719 | 0.386% (2,145) | [Kaggle: Credit Card Transactions](https://www.kaggle.com/datasets/kartik2112/fraud-detection) |
| **D3** | `PS.csv` | PaySim (Lopez-Rojas et al., EMSS 2016) | 5,840,046 | 0.077% (4,497) | [Kaggle: PaySim1 Synthetic Financial Dataset](https://www.kaggle.com/datasets/ealaxi/paysim1) |

*(Note for D3: PaySim is typically distributed under filenames such as `PS_20174392719_1491204439457_log.csv` or `PS.csv`. Ensure the file is renamed or symlinked as `PS.csv` when running local scripts).*

See [DATASET_ACCESS_NOTE.md](../00_source_datasets_notes/DATASET_ACCESS_NOTE.md) and [01_dataset_truth_audit/](../01_dataset_truth_audit/) for detailed row-level verification, duplicate counts, and feature risk audits.
