# ADNI Machine-Learning Imputation Plan

## Objective
Compare ML-based imputation methods against standard statistical methods for ADNI subject-visit clinical data.

## Candidate methods
- KNN imputation;
- random-forest imputation;
- gradient-boosting-based imputation;
- iterative imputation with ML estimators;
- matrix factorization for high-dimensional clinical matrices.

## Important restrictions
All ML imputation models must be trained only on the training subjects. Test subjects must not be used to fit imputers.

## Non-IID handling
Because rows are clustered within subjects:

- train/test split must be by RID;
- cross-validation must be grouped by RID;
- longitudinal features should include visit month and previous visit values;
- performance uncertainty should use subject-level bootstrap or grouped cross-validation.

## Benchmark comparison
Each imputation method should be evaluated using:

1. artificial masking accuracy;
2. downstream clinical prediction;
3. calibration;
4. feature-importance stability;
5. runtime and reproducibility.
