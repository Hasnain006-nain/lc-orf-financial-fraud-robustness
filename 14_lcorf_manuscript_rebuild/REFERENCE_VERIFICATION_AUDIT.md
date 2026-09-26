# Reference Verification Audit

Checked: 2026-09-26

Scope: `main.tex` and `references.bib` in the LC-ORF IEEE Access manuscript folder.

Rule applied: references retained in `references.bib` must have a live source URL or DOI recorded in a `% verified:` comment. Unsupported metadata was corrected or removed.

## Corrections Made

| Key | Status | Action |
|---|---|---|
| `lucas2020survey` | CORRECTED | Author list corrected to Yvan Lucas and Johannes Jurgovsky only, based on the arXiv source. |
| `bahnsen2013cost` | CORRECTED | Author list corrected to include Aleksandar Stojanovic and correct author order. |
| `kaufman2012leakage` | CORRECTED | Replaced incorrect 2012/TKDD-style metadata with the verified KDD 2011 entry and DOI. |
| `bolton2002fraud` | CORRECTED | Page range restricted to the main review article range. |
| `platt1999probabilistic` | REMOVED | Removed because the exact chapter metadata could not be verified cleanly against a primary source in this session. Calibration claims remain supported by verified Zadrozny-Elkan, Niculescu-Mizil-Caruana, and Guo et al. sources. |

## Verified References Retained

| Key | Status | Verification source |
|---|---|---|
| `bolton2002fraud` | VERIFIED | https://doi.org/10.1214/ss/1042727940 |
| `dalpozzolo2014lessons` | VERIFIED | https://doi.org/10.1016/j.eswa.2014.02.026 |
| `lucas2020survey` | VERIFIED | https://arxiv.org/abs/2010.06479 |
| `bahnsen2013cost` | VERIFIED | https://doi.org/10.1109/ICMLA.2013.68 |
| `bahnsen2016feature` | VERIFIED | https://doi.org/10.1016/j.eswa.2015.12.030 |
| `kaufman2012leakage` | VERIFIED | https://doi.org/10.1145/2020408.2020496 |
| `gama2014drift` | VERIFIED | https://doi.org/10.1145/2523813 |
| `dalpozzolo2015drift` | VERIFIED | https://doi.org/10.1109/IJCNN.2015.7280527 |
| `chawla2002smote` | VERIFIED | https://doi.org/10.1613/jair.953 |
| `davis2006pr` | VERIFIED | https://doi.org/10.1145/1143844.1143874 |
| `saito2015precision` | VERIFIED | https://doi.org/10.1371/journal.pone.0118432 |
| `chicco2020mcc` | VERIFIED | https://doi.org/10.1186/s12864-019-6413-7 |
| `elkan2001cost` | VERIFIED | https://www.ijcai.org/Proceedings/01/Papers/089.pdf |
| `zadrozny2002calibrating` | VERIFIED | https://doi.org/10.1145/775047.775151 |
| `niculescu2005predicting` | VERIFIED | https://doi.org/10.1145/1102351.1102430 |
| `guo2017calibration` | VERIFIED | https://proceedings.mlr.press/v70/guo17a.html |
| `ribeiro2016lime` | VERIFIED | https://doi.org/10.1145/2939672.2939778 |
| `lundberg2017shap` | VERIFIED | https://papers.nips.cc/paper_files/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html |
| `lipton2016mythos` | VERIFIED | https://doi.org/10.1145/3236386.3241340 |
| `adebayo2018sanity` | VERIFIED | https://papers.nips.cc/paper_files/paper/2018/hash/294a8ed24b1ad22ec2e7efea049b8737-Abstract.html |
| `alvarez2018robustness` | VERIFIED | https://arxiv.org/abs/1806.08049 |
| `chen2016xgboost` | VERIFIED | https://doi.org/10.1145/2939672.2939785 |
| `ke2017lightgbm` | VERIFIED | https://papers.nips.cc/paper_files/paper/2017/hash/6449f44a102fde848669bdd9eb6b76fa-Abstract.html |
| `creditcard_kaggle` | VERIFIED | https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud |
| `fraudtest_kaggle` | VERIFIED | https://www.kaggle.com/datasets/kartik2112/fraud-detection |
| `lopezrojas2016paysim` | VERIFIED | https://www.msc-les.org/proceedings/emss/emss2016/emss2016_249.html |

## Citation Integrity Result

Every retained bibliography key is cited in `main.tex`, and every `\cite{...}` key in `main.tex` resolves to an entry in `references.bib` as of this audit.
