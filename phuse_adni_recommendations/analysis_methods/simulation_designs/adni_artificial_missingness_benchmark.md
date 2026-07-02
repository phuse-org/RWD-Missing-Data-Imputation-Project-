# ADNI Alzheimer Longitudinal Missing-Data Imputation Benchmark

## Objective
Compare standard, machine-learning, and newer imputation methods for non-IID longitudinal Alzheimer clinical data.

The benchmark evaluates:

1. imputation quality under realistic missingness mechanisms;
2. downstream clinical model performance after imputation.

## Dataset structure
The dataset is subject-visit level. Multiple rows may belong to the same subject. Observations are non-IID and all train/test splitting must be performed by subject ID.

## Primary data type
D2: longitudinal / repeated-measures clinical data.

## Secondary data type
D1: structured/tabular clinical data.

## Missingness types
The benchmark distinguishes:

1. ordinary missingness;
2. structural missingness;
3. planned/protocol-driven missingness;
4. longitudinal dropout;
5. site/phase-related missingness.

## Primary benchmark outcome
Next-visit clinical diagnosis:

- Dementia vs non-Dementia.

Alternative multiclass outcome:

- CN vs MCI vs Dementia.

## Secondary benchmark outcomes
- next-visit MMSE;
- next-visit ADAS13;
- change from baseline in MMSE;
- change from baseline in ADAS13;
- NPI-Q total symptom burden.

## Data split
All splitting must be subject-level:

- 70% subjects for training;
- 15% subjects for validation;
- 15% subjects for testing.

Rows from the same subject must never appear in both training and testing sets.

## Imputation methods
The benchmark may compare:

1. complete-case analysis;
2. median/mode imputation;
3. median/mode imputation with missingness indicators;
4. LOCF/BOCF sensitivity method;
5. MICE / fully conditional specification;
6. longitudinal or multilevel MICE;
7. mixed-model-based imputation;
8. KNN imputation;
9. random-forest imputation / missForest-style methods;
10. gradient-boosting-based imputation;
11. deep-learning or sequence-aware imputation methods, such as BRITS/SAITS-style methods, if implementation is available.

## Artificial missingness scenarios
Observed values will be masked to create benchmark scenarios:

1. MCAR: randomly mask observed cells.
2. MAR: mask values depending on diagnosis, age, visit month, site, or ADNI phase.
3. Block missingness: remove whole clinical domains such as imaging or biomarkers.
4. Longitudinal dropout: remove future visits for selected subjects.
5. Site/phase missingness: remove values depending on site or protocol phase.

Recommended masking rates:

- 10%;
- 20%;
- 30%;
- 40%.

## Imputation-quality metrics
Continuous variables:

- RMSE;
- MAE;
- normalized RMSE;
- distributional similarity.

Categorical variables:

- accuracy;
- balanced accuracy;
- macro-F1.

Longitudinal consistency:

- within-subject trajectory plausibility;
- clinically appropriate smoothness checks.

## Downstream model metrics
Classification:

- AUROC;
- AUPRC;
- balanced accuracy;
- F1 score;
- Brier score;
- calibration slope/intercept.

Regression:

- RMSE;
- MAE;
- R-squared;
- calibration of predicted versus observed values.

Robustness:

- grouped cross-validation by subject;
- site/phase sensitivity analysis;
- feature-importance stability.

## Data leakage prevention
The imputer must be fit only on the training subjects. Validation and test data must be transformed using the fitted imputation process. Full-dataset imputation before train/test split is not allowed.

## Reporting
The final report should include:

1. dataset metadata, not raw data;
2. missingness summary by variable;
3. missingness summary by visit;
4. missingness summary by diagnosis group;
5. missingness summary by site and ADNI phase;
6. description of structural NPI-Q missingness handling;
7. imputation benchmark results;
8. downstream model results;
9. sensitivity analyses;
10. limitations and data-use restrictions.
