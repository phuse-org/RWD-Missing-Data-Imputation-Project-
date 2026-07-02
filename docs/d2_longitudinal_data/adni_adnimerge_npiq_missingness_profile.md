# ADNI ADNIMERGE + NPI-Q Missingness Profile

## Purpose
This document defines how missingness should be interpreted and handled for the ADNI ADNIMERGE + NPI-Q longitudinal benchmark.

## Missingness types

### 1. Structural missingness
NPI-Q symptom variables and severity variables require special handling. For each NPI-Q symptom domain, the symptom variable is binary and the severity variable is meaningful only when the symptom is present.

Recommended rule:

1. If symptom = 0, derive severity_for_model = 0.
2. If symptom = 1, severity should be 1, 2, or 3.
3. If symptom is missing, impute symptom first.
4. If symptom is imputed as 0, set severity_for_model = 0.
5. If symptom is imputed as 1, impute severity conditionally among valid positive severity levels.
6. Do not apply ordinary continuous imputation directly to raw severity fields without respecting this structure.

### 2. Planned or protocol-driven missingness
Some biomarker and imaging variables may be missing because they were collected only in selected ADNI phases, visits, substudies, or modality-specific cohorts.

Recommended handling:

- keep missingness indicators;
- perform primary models without extreme-missing variables;
- perform domain-specific subcohort analyses for biomarkers or imaging;
- avoid forcing full-dataset imputation for variables with extreme planned missingness.

### 3. Ordinary clinical missingness
Clinical and cognitive variables may be imputed using standard or ML methods, but the imputation model should include subject, visit, diagnosis, site, and phase information.

### 4. Longitudinal dropout
Later visits may be missing because of dropout, disease progression, loss to follow-up, death, or administrative reasons. Sensitivity analyses should evaluate dropout-related assumptions.

## Non-IID rule
All splitting and resampling must respect the subject-level structure. Rows from the same RID must not be split across training and testing datasets.
