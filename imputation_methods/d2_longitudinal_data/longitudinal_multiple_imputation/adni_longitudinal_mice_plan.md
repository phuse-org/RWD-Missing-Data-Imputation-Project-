# ADNI Longitudinal MICE Imputation Plan

## Purpose
Apply multiple imputation to ADNI longitudinal clinical data while respecting subject-level repeated measurements.

## Required design features
- Use subject ID as a clustering variable.
- Include visit month/time as a predictor.
- Include baseline diagnosis.
- Include site and ADNI phase.
- Include previous observed values where available.
- Use variable-specific imputation models.

## Variable-specific methods
Continuous variables:

- predictive mean matching;
- linear regression;
- mixed-effects imputation where available.

Binary variables:

- logistic imputation.

Multicategory variables:

- multinomial imputation.

Ordinal variables:

- proportional odds or ordered categorical imputation.

NPI-Q severity variables:

- conditional imputation based on symptom presence.

## Multiple imputation
Use multiple imputed datasets, for example:

- m = 20 for the main analysis;
- m = 50 for sensitivity analysis if missingness is high.

## Pooling
For statistical models, combine estimates using Rubin's rules.

For ML prediction benchmarks, either:

1. train and evaluate models separately in each imputed dataset and summarize performance; or
2. stack imputations with appropriate subject-level grouping and sensitivity reporting.
