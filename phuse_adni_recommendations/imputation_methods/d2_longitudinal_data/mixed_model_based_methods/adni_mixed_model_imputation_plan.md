# ADNI Mixed-Model-Based Imputation Plan

## Purpose
Use mixed-model-based imputation for longitudinal ADNI clinical variables where repeated measures within subjects are important.

## Rationale
Rows are correlated within subjects. Mixed models can represent subject-specific random effects and time trends, which are useful for longitudinal clinical scores such as MMSE, ADAS13, CDRSB, FAQ, and NPI-Q total score.

## Candidate variables
- MMSE
- ADAS11
- ADAS13
- CDRSB
- FAQ
- MOCA
- RAVLT measures
- NPI-Q total score

## Candidate predictors
- baseline diagnosis;
- visit month;
- age;
- sex;
- education;
- APOE4;
- site;
- ADNI phase;
- previous observed clinical score;
- other cognitive and clinical domains.

## Model structure
A basic mixed model may include:

- fixed effects for time, diagnosis, demographics, site, and phase;
- random intercept for subject;
- random slope for time when supported by the data.

## Sensitivity analyses
- compare random-intercept and random-slope models;
- compare models with and without site/phase effects;
- evaluate robustness under dropout-related missingness assumptions.
