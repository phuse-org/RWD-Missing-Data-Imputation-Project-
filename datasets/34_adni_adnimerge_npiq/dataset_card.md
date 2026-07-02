# ADNI ADNIMERGE + NPI-Q Longitudinal Dataset Card

## Dataset name
ADNI ADNIMERGE + NPI-Q Combined Longitudinal Dataset

## Data source
Alzheimer's Disease Neuroimaging Initiative (ADNI).

## Access status
Controlled access. Data are available through ADNI/LONI only after approval and acceptance of the applicable ADNI Data Use Agreement.

## GitHub data policy
No raw participant-level ADNI data are included in this repository. This folder contains metadata only.

## Dataset type
D2: longitudinal / repeated-measures clinical data.

Secondary type: D1 structured/tabular clinical data, because each subject-visit row contains structured clinical, cognitive, imaging, biomarker, and neuropsychiatric variables.

## Clinical area
Alzheimer's disease, mild cognitive impairment, cognitive decline, and neuropsychiatric symptoms.

## Unit of observation
Subject-visit level.

## Non-IID structure
Rows are not independent. A single subject may contribute multiple visits. Analyses must therefore split data by subject identifier rather than by row.

## Key identifiers
- RID: subject identifier
- ADNI_EXAMDATE: ADNI visit date
- NPIQ_VISDATE: NPI-Q visit date
- ADNI_VISCODE: visit code
- ADNI_SITE: clinical site
- ADNI_COLPROT / ADNI_ORIGPROT: ADNI phase/protocol

## Main clinical domains
- Demographics
- Diagnosis
- Cognitive scores
- Neuropsychiatric symptoms
- MRI measures
- PET biomarkers
- CSF biomarkers

## Missing-data relevance
This dataset is suitable for benchmarking missing-data imputation because it contains repeated measures, subject-level correlation, irregular visit patterns, site and protocol effects, structural missingness in NPI-Q severity variables, and high missingness in selected imaging and biomarker variables.

## Recommended benchmark use
Approved ADNI users may run the benchmark in a secure local environment. GitHub materials should include only metadata, code templates, benchmark definitions, and aggregate results.
