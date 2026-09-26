# Feature Governance Table

This table converts the dataset audit into modeling rules for the revised paper. The main point is to separate deployable features from identifier, temporal, and leakage-risk fields before running new experiments.

## Feature Sets

| Feature set | Purpose | Definition |
|---|---|---|
| strict | Main publishable protocol. | Only features defensibly available at scoring time, with identifiers removed and fitted preprocessing restricted to training data. |
| chronology | Temporal robustness evaluation. | Uses source time fields for ordering train/validation/test windows. Raw time fields are not automatically model inputs. |
| operational | Context-rich but still plausible deployment setting. | Allows carefully encoded merchant/job/location fields when available at scoring time; requires min-frequency grouping and explicit reporting. |
| ledger_state | D3 leakage/availability stress test. | Compares strict pre-transaction features with post-transaction balance fields to quantify possible inflation. |
| strict_sensitive | Fairness/sensitivity transparency. | Demographic or proxy variables are reported and tested with ablation, not silently mixed into the main result. |

## Required Rules

- The main paper must use the `strict` feature set as the primary protocol.
- Identifier and label columns must be removed before preprocessing, splitting-dependent fitting, or oversampling.
- Time fields are used for chronological split. If raw time is used as a model input, the manuscript must say so explicitly.
- D3 `isFlaggedFraud`, `nameOrig`, and `nameDest` are excluded from all main models.
- D3 post-transaction balance fields are not allowed in the strict feature set. They belong only in a leakage/ledger-state stress test.
- D2 `Unnamed: 0` and `trans_num` are always removed.

## Column Governance

| Dataset | Column | Role | Action | Feature set | Rationale | Paper rule |
|---|---|---|---|---|---|---|
| D1_creditcard | `Class` | label | target_only | all | Binary fraud label. | Never include as input. |
| D1_creditcard | `Time` | time | derive_or_temporal_only | strict, chronology | Seconds elapsed in source data. Useful for chronological split, but may encode collection order. | Use for temporal ordering. If used as feature, report it explicitly; otherwise derive bounded time-context features or exclude in strict ablation. |
| D1_creditcard | `V1` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V2` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V3` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V4` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V5` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V6` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V7` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V8` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V9` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V10` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V11` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V12` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V13` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V14` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V15` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V16` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V17` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V18` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V19` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V20` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V21` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V22` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V23` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V24` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V25` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V26` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V27` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `V28` | anonymized_numeric | keep | strict | PCA/anonymized transaction feature with no direct identifier in source schema. | Keep after train-only preprocessing. |
| D1_creditcard | `Amount` | transaction_amount | keep | strict | Transaction amount is available at scoring time and operationally meaningful. | Keep; scale using train-only preprocessing. |
| D2_fraudTest | `is_fraud` | label | target_only | all | Binary fraud label. | Never include as input. |
| D2_fraudTest | `Unnamed: 0` | source_index | remove | all | Fully unique index-like artifact; no deployment meaning. | Drop before split/modeling. |
| D2_fraudTest | `trans_num` | transaction_identifier | remove | all | Fully unique transaction ID. Memorization risk and no generalizable signal. | Drop before split/modeling. |
| D2_fraudTest | `cc_num` | customer_identifier | remove | strict | Card/customer identifier can let random splits memorize cardholder-specific fraud propensity. | Drop in strict protocol; optional ID-stress ablation only. |
| D2_fraudTest | `first` | personal_identifier | remove | strict | PII-like name field and proxy for customer identity. | Drop in strict protocol. |
| D2_fraudTest | `last` | personal_identifier | remove | strict | PII-like name field and proxy for customer identity. | Drop in strict protocol. |
| D2_fraudTest | `street` | personal_location_identifier | remove | strict | Address-level field identifies a customer and can leak split-specific identity. | Drop in strict protocol. |
| D2_fraudTest | `zip` | location_identifier | coarsen_or_remove | strict | ZIP can identify customer geography; useful but high-cardinality. | Prefer state/city_pop. If ZIP retained, use grouped/coarsened encoding and report it. |
| D2_fraudTest | `lat` | customer_location | coarsen_or_remove | strict | Precise customer coordinates are identity proxies. | Drop in strict protocol or coarsen into broad region bins. |
| D2_fraudTest | `long` | customer_location | coarsen_or_remove | strict | Precise customer coordinates are identity proxies. | Drop in strict protocol or coarsen into broad region bins. |
| D2_fraudTest | `city` | location | coarsen_or_remove | strict | High-cardinality customer location; may proxy identity under random split. | Use state/city_pop in strict protocol; city only in location-rich ablation. |
| D2_fraudTest | `merchant` | merchant_identifier | conditional_keep | operational | Merchant can be available at scoring time but has 693 categories and can dominate model behavior. | Keep only with min-frequency grouping/unknown handling. Include no-merchant ablation. |
| D2_fraudTest | `category` | merchant_category | keep | strict | Low-cardinality transaction context available at scoring time. | Keep. |
| D2_fraudTest | `amt` | transaction_amount | keep | strict | Transaction amount is available at scoring time. | Keep. |
| D2_fraudTest | `gender` | demographic | conditional_keep | strict_sensitive | Available in source but potentially sensitive and not always operationally acceptable. | Report whether included. Prefer sensitivity ablation with and without demographic fields. |
| D2_fraudTest | `state` | coarse_location | keep | strict | Coarse geography with 50 values; less identity-specific than address/coordinates. | Keep with train-only one-hot/min-frequency handling. |
| D2_fraudTest | `city_pop` | area_context | keep | strict | Aggregate contextual feature, not a direct identifier. | Keep. |
| D2_fraudTest | `job` | occupation | conditional_keep | operational | High-cardinality occupation may be available but can act as demographic proxy. | Keep only with grouped encoding and include sensitivity note. |
| D2_fraudTest | `dob` | date_of_birth | derive_then_remove | strict | Raw date of birth identifies customer; age is a safer derived feature. | Derive age at transaction time using training-safe transformation; drop raw dob. |
| D2_fraudTest | `trans_date_trans_time` | transaction_time | derive_or_temporal_only | strict, chronology | Transaction time is available and needed for chronological split. | Use for chronological ordering; derive hour/day/month features; drop raw timestamp as model input unless explicitly reported. |
| D2_fraudTest | `unix_time` | transaction_time_numeric | derive_or_temporal_only | chronology | Duplicate numeric timestamp; can encode collection order. | Use for chronological ordering; avoid using raw unix_time as model input in strict protocol. |
| D2_fraudTest | `merch_lat` | merchant_location | conditional_keep | operational | Merchant coordinates can be available at scoring time but very high-cardinality. | Prefer distance/coarse bins if customer location is allowed; otherwise use only in location-rich ablation. |
| D2_fraudTest | `merch_long` | merchant_location | conditional_keep | operational | Merchant coordinates can be available at scoring time but very high-cardinality. | Prefer distance/coarse bins if customer location is allowed; otherwise use only in location-rich ablation. |
| D3_PaySim | `isFraud` | label | target_only | all | Binary fraud label with one missing row in current file. | Drop missing-label row; never include as input. |
| D3_PaySim | `isFlaggedFraud` | rule_based_flag | remove | all | Source rule flag, not a normal predictive feature; only four positives and directly related to fraud rules. | Drop from every model input. May be described as excluded leakage/rule signal. |
| D3_PaySim | `nameOrig` | origin_identifier | remove | strict | Near-unique account identifier; memorization/generalization risk. | Drop before split/modeling. |
| D3_PaySim | `nameDest` | destination_identifier | remove | strict | High-cardinality account identifier; memorization/generalization risk. | Drop before split/modeling. |
| D3_PaySim | `step` | time | derive_or_temporal_only | strict, chronology | Simulation time step; needed for chronological validation and possibly time-context features. | Use for chronological ordering. If used as feature, report it explicitly. |
| D3_PaySim | `type` | transaction_type | keep | strict | Low-cardinality transaction type available at scoring time. | Keep. |
| D3_PaySim | `amount` | transaction_amount | keep | strict | Transaction amount available at scoring time. | Keep. |
| D3_PaySim | `oldbalanceOrg` | pre_transaction_balance | keep | strict | Origin balance before transaction; defensibly available before execution. | Keep in strict pre-transaction feature set. |
| D3_PaySim | `oldbalanceDest` | pre_transaction_balance | conditional_keep | strict | Destination balance before transaction may be available to platform operator, but not always to all deployers. | Keep only if paper defines platform-operator setting; otherwise include ablation without destination balance. |
| D3_PaySim | `newbalanceOrig` | post_transaction_balance | leakage_stress_only | ledger_state | Post-transaction balance can encode outcome/state after the event. | Exclude from strict protocol. Include only in ledger-state/leakage-stress ablation. |
| D3_PaySim | `newbalanceDest` | post_transaction_balance | leakage_stress_only | ledger_state | Post-transaction destination balance can encode outcome/state after the event. | Exclude from strict protocol. Include only in ledger-state/leakage-stress ablation. |

## Immediate Modeling Decision

Use `strict` as the new main protocol. Then run two explicit stress tests:

1. Leakage pipeline stress: safe split-first pipeline vs unsafe preprocessing/SMOTE-before-split variants.
2. D3 ledger-state stress: strict pre-transaction features vs adding `newbalanceOrig` and `newbalanceDest`.

This converts feature handling from an implementation detail into a publishable methodological contribution.
