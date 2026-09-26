# Dataset Truth Audit

This report audits source CSV structure, label prevalence, duplicates, missingness, time fields, high-cardinality fields, and columns requiring leakage review.

## Dataset Summary

| Dataset | Rows | Columns | Label | Fraud rows | Fraud rate | Duplicate rows | Missing cells |
|---|---:|---:|---|---:|---:|---:|---:|
| D1_creditcard | 284,807 | 31 | Class | 492 | 0.172749% | 1,081 | 0 |
| D2_fraudTest | 555,719 | 23 | is_fraud | 2,145 | 0.385986% | 0 | 0 |
| D3_PaySim | 5,840,046 | 11 | isFraud | 4,497 | 0.077003% | 0 | 2 |

## Review Flags

### D1_creditcard
- Time/date columns: Time
- Leakage-review columns: none detected
- Identifier/high-cardinality review columns: none detected
- High-cardinality columns: Time, V1, V2, V3, V4, V5, V6, V7, V8, V9, V10, V11, V12, V13, V14, V15, V16, V17, V18, V19
- Additional high-cardinality columns omitted from this summary: 10

### D2_fraudTest
- Time/date columns: trans_date_trans_time, dob, unix_time
- Leakage-review columns: none detected
- Identifier/high-cardinality review columns: cc_num, merchant, first, last, street, zip, lat, long, trans_num, merch_lat, merch_long
- High-cardinality columns: Unnamed: 0, trans_date_trans_time, cc_num, merchant, amt, first, last, street, city, zip, lat, long, city_pop, job, dob, trans_num, unix_time, merch_lat, merch_long

### D3_PaySim
- Time/date columns: step
- Leakage-review columns: oldbalanceOrg, newbalanceOrig, oldbalanceDest, newbalanceDest, isFlaggedFraud
- Identifier/high-cardinality review columns: nameOrig, nameDest
- High-cardinality columns: step, amount, nameOrig, oldbalanceOrg, newbalanceOrig, nameDest, oldbalanceDest, newbalanceDest
