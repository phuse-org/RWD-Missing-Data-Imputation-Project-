# ADNI Longitudinal Alzheimer Missing-Data Imputation Benchmark

This branch adds a metadata-only benchmark proposal for comparing missing-data imputation methods in longitudinal Alzheimer clinical data.

The use case is based on an ADNI ADNIMERGE + NPI-Q combined dataset. ADNI is controlled-access clinical research data. Therefore, raw participant-level data are **not included** in this repository.

## Purpose

The purpose of this contribution is to define a reusable benchmark structure for missing-value imputation in non-IID clinical data.

The project focuses on:

- longitudinal Alzheimer disease data;
- repeated visits per subject;
- missing clinical, cognitive, imaging, biomarker, and NPI-Q variables;
- structural missingness in NPI-Q severity variables;
- standard, machine-learning, and newer imputation methods;
- downstream clinical model comparison after imputation.

This is designed as a reusable framework, not only as a single-dataset analysis.

## Repository Structure

The proposed contribution uses the following structure:

```text
datasets/
└── 34_adni_adnimerge_npiq/
    └── dataset_card.md

docs/
└── d2_longitudinal_data/
    └── adni_adnimerge_npiq_missingness_profile.md

analysis_methods/
└── simulation_designs/
    └── adni_artificial_missingness_benchmark.md

imputation_methods/
├── d1_structured_data/
│   └── machine_learning_imputation/
│       └── adni_ml_imputation_plan.md
└── d2_longitudinal_data/
    ├── longitudinal_multiple_imputation/
    │   └── adni_longitudinal_mice_plan.md
    └── mixed_model_based_methods/
        └── adni_mixed_model_imputation_plan.md
```

## Dataset Description

The dataset is subject-visit level longitudinal clinical data.

This means:

- one subject can have multiple visits;
- rows from the same subject are correlated;
- subjects can have different numbers of visits;
- missingness may depend on diagnosis, visit, site, protocol, phase, or disease progression;
- the data are non-IID.

Because of this, analysis should use subject-level splitting and grouped validation, not random row-level splitting.

## Main Clinical Domains

The dataset may include:

- demographics;
- diagnosis;
- cognitive assessments;
- functional assessments;
- NPI-Q neuropsychiatric symptoms;
- MRI measurements;
- PET biomarkers;
- CSF biomarkers;
- site and protocol information;
- visit timing variables.

## Missing-Data Types

The benchmark separates missingness into several categories.

### Ordinary Missingness

Missing values in clinical, cognitive, imaging, biomarker, or demographic variables.

These may be handled using standard imputation methods.

### Structural Missingness

Some NPI-Q severity variables are missing because the corresponding symptom is absent. This is not ordinary missingness.

Recommended rule:

```text
If symptom = 0:
    set derived severity = 0

If symptom = 1:
    severity should be 1, 2, or 3

If symptom is missing:
    impute symptom first

If imputed symptom = 0:
    set derived severity = 0

If imputed symptom = 1:
    impute severity conditionally among valid positive severity values
```

### Planned Missingness

Some biomarkers or imaging variables may be missing because they were collected only in specific visits, ADNI phases, protocols, or subcohorts.

These variables should be handled using sensitivity analysis or domain-specific subcohort analysis.

### Longitudinal Dropout

Some subjects may stop contributing later visits. This may be related to disease progression, study withdrawal, loss to follow-up, death, or protocol differences.

### Site- and Phase-Related Missingness

Missingness may depend on site, ADNI phase, protocol, or data-collection procedure. These variables should be considered in imputation models.

## General Analysis Plan

### Phase 1: Data Review

Summarize:

- number of subjects;
- number of rows;
- number of visits per subject;
- variable domains;
- missingness by variable;
- missingness by visit;
- missingness by diagnosis group;
- missingness by site;
- missingness by ADNI phase;
- subject-level dropout patterns.

Expected outputs:

```text
Table 1: Dataset overview
Table 2: Missingness by variable
Table 3: Missingness by visit
Table 4: Missingness by diagnosis group
Figure 1: Missingness heatmap
Figure 2: Subject-level dropout pattern
```

### Phase 2: Variable Classification

Classify variables as:

```text
No missing
Structural missing
Low missing: <10%
Moderate missing: 10% to 40%
High missing: 40% to 80%
Extreme missing: >80%
```

Recommended handling:

```text
0% missing:
    keep directly

<40% missing:
    include in primary imputation analysis

40% to 80% missing:
    include with sensitivity analysis

>80% missing:
    exclude from primary full-data model;
    consider domain-specific subcohort analysis

Structural missing:
    handle using clinical rules
```

### Phase 3: Non-IID Data Splitting

The correct split is by subject ID, not by row.

Recommended split:

```text
70% training subjects
15% validation subjects
15% test subjects
```

Rows from the same subject must not appear in both training and testing sets.

### Phase 4: Imputation Methods

The benchmark compares several groups of imputation methods.

Baseline methods:

- complete-case analysis;
- mean, median, or mode imputation;
- median/mode imputation with missingness indicators;
- diagnosis- and visit-specific median imputation;
- LOCF as sensitivity analysis.

Standard statistical methods:

- MICE;
- predictive mean matching;
- logistic imputation;
- multinomial imputation;
- ordinal imputation;
- longitudinal or multilevel MICE;
- mixed-model-based imputation.

Machine-learning methods:

- KNN imputation;
- random-forest imputation;
- missForest-style imputation;
- gradient-boosting-based imputation;
- XGBoost-based iterative imputation;
- matrix-factorization-based imputation.

Newer methods:

- GAIN-style tabular imputation;
- VAE-based imputation;
- BRITS-style longitudinal imputation;
- SAITS-style transformer imputation;
- mask-aware neural-network imputation.

### Phase 5: Artificial Missingness Benchmark

Because the true value of real missing data is unknown, artificial missingness should be created from observed values.

Scenarios:

```text
MCAR:
    randomly mask observed values

MAR:
    mask values depending on age, diagnosis, visit, site, or ADNI phase

Block missingness:
    remove whole groups of variables such as imaging or biomarkers

Longitudinal dropout:
    remove later visits for selected subjects

Site/phase missingness:
    remove values depending on site, protocol, or ADNI phase
```

Masking rates:

```text
10%
20%
30%
40%
```

### Phase 6: Imputation-Quality Evaluation

Continuous variables:

- RMSE;
- MAE;
- normalized RMSE;
- bias;
- distributional similarity.

Categorical variables:

- accuracy;
- balanced accuracy;
- macro-F1;
- weighted-F1.

Ordinal variables:

- mean absolute ordinal error;
- weighted kappa;
- ordinal accuracy.

Longitudinal checks:

- within-subject trajectory plausibility;
- visit-to-visit clinical consistency;
- extreme value checks;
- distribution by visit and diagnosis group.

### Phase 7: Downstream Clinical Model Evaluation

After each imputation method, train the same downstream model.

Primary classification outcome:

```text
Next-visit Dementia vs non-Dementia
```

Alternative outcome:

```text
CN vs MCI vs Dementia
```

Secondary regression outcomes:

```text
Next-visit MMSE
Next-visit ADAS13
Change from baseline in MMSE
Change from baseline in ADAS13
NPI-Q total symptom burden
```

Candidate models:

- logistic regression;
- elastic net;
- linear regression;
- mixed-effects model;
- random forest;
- gradient boosting;
- XGBoost or LightGBM;
- simple neural network as sensitivity analysis.

Classification metrics:

- AUROC;
- AUPRC;
- balanced accuracy;
- sensitivity;
- specificity;
- F1 score;
- Brier score;
- calibration slope;
- calibration intercept.

Regression metrics:

- RMSE;
- MAE;
- R-squared;
- prediction bias;
- calibration of predicted versus observed values.

## Data Leakage Prevention

Correct workflow:

```text
1. Split subjects into train, validation, and test sets.
2. Fit preprocessing only on training subjects.
3. Fit imputation only on training subjects.
4. Apply the fitted imputation pipeline to validation and test subjects.
5. Train the clinical model on imputed training data.
6. Evaluate the model on imputed test data.
```

Incorrect workflow:

```text
1. Impute the full dataset.
2. Split rows randomly.
3. Train and test on rows from the same subjects.
```

The incorrect workflow causes data leakage and can inflate model performance.

## Sensitivity Analyses

Recommended sensitivity analyses:

- exclude variables with more than 80% missingness;
- compare models with and without biomarker variables;
- compare models with and without imaging variables;
- analyze subjects with at least two visits;
- analyze subjects with baseline and follow-up diagnosis;
- evaluate by ADNI phase;
- evaluate by clinical site;
- evaluate by baseline diagnosis group;
- compare complete-case and imputed-data results;
- compare single imputation and multiple imputation.

## Proposed New Method Direction

A possible original contribution is:

```text
Subject-Aware Hybrid Imputation for Longitudinal Alzheimer Clinical Data
```

This approach would combine:

- rule-based handling of structural NPI-Q missingness;
- MICE or missForest for structured tabular variables;
- mixed-model imputation for repeated cognitive outcomes;
- sequence-aware imputation for longitudinal variables;
- missingness-mask features;
- subject-level and visit-level information.

The aim is to respect clinical meaning, repeated visits, subject-level correlation, structural missingness, and non-IID data structure.

## Expected Outputs

The benchmark should produce:

- dataset metadata card;
- missingness profile document;
- artificial missingness simulation design;
- imputation method comparison table;
- downstream model comparison table;
- sensitivity analysis report;
- code templates for reproducible analysis;
- aggregate results only.

## Data Use and Privacy

Raw ADNI participant-level data must not be committed to this repository.

Allowed materials:

- metadata;
- analysis plans;
- code templates;
- synthetic examples;
- aggregate results;
- documentation.

Not allowed:

- raw ADNI CSV files;
- participant-level records;
- subject-level predictions;
- imputed patient-level datasets;
- protected or controlled-access data.

## Summary

This contribution proposes a longitudinal Alzheimer missing-data imputation benchmark for controlled-access clinical research data.

The main scientific idea is:

```text
Missing-value imputation in Alzheimer clinical data should not only fill empty cells.
It should respect clinical meaning, subject-level correlation, longitudinal trajectories, structural missingness, and non-IID data structure.
```
