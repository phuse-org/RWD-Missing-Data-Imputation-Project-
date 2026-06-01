# PHUSE: Applying Missing-Value Imputation Methods to Real-World Data (RWD)

This repository is a shared workspace for the PHUSE project team to collaborate on:

- Benchmark specifications: what we evaluate
- Reference implementations: how we run missing-data and imputation benchmarks
- Documentation that helps stakeholders review scope, structure, assumptions, and progress

## What this repo is not

This repository is not a place to store raw patient-level datasets.

We only keep dataset metadata, benchmark definitions, documentation, code templates, and implementation examples in GitHub.

## Quick links

- Dataset registry: `datasets/README.md`
- Missing-data and imputation methods: `imputation_methods/`
- Analysis methods: `analysis_methods/`
- Research and paper reviews: `research/`
- Documentation by data type: `docs/`
- Next steps and roadmap: `next_steps.md`
- Contributing guide: `CONTRIBUTING.md`

## Repo structure

```text
phuseimputation/
├── imputation_methods/                       # Missing-data and imputation method implementations
│   ├── d1_structured_data/                   # Structured/tabular clinical RWD
│   │   ├── missingness_profiling/
│   │   ├── complete_case_analysis/
│   │   ├── single_imputation/
│   │   ├── multiple_imputation/
│   │   ├── mice_fcs/
│   │   ├── model_based_imputation/
│   │   ├── machine_learning_imputation/
│   │   └── sensitivity_analysis/
│   ├── d2_longitudinal_data/                 # Repeated measures / longitudinal RWD
│   │   ├── locf_bocf_methods/
│   │   ├── longitudinal_multiple_imputation/
│   │   ├── mixed_model_based_methods/
│   │   ├── pattern_mixture_models/
│   │   └── tipping_point_analysis/
│   └── d3_time_to_event_data/                # Survival / censoring-related missingness
│       ├── censoring_assumptions/
│       ├── inverse_probability_weighting/
│       ├── multiple_imputation/
│       └── sensitivity_analysis/
├── analysis_methods/                         # Benchmark analysis specifications
├── datasets/                                 # Dataset registry — metadata only
├── docs/                                     # Documentation
├── research/                                 # Paper reviews and implementation reports
├── experiments/                              # Local experiment outputs, ignored by git
├── data/                                     # Local data directory, ignored by git
└── results/                                  # Local outputs directory, ignored by git
```

## Folder conventions

The three core folders — `imputation_methods/`, `docs/`, and `research/` — share the same D1/D2/D3 hierarchy.

| Data type | Folder | Methods |
|---|---|---|
| D1 Structured/tabular RWD | `d1_structured_data/` | missingness profiling, complete-case analysis, single imputation, multiple imputation, MICE/FCS, model-based imputation, machine-learning imputation, sensitivity analysis |
| D2 Longitudinal/repeated measures RWD | `d2_longitudinal_data/` | LOCF/BOCF, longitudinal multiple imputation, mixed-model-based methods, pattern-mixture models, tipping-point analysis |
| D3 Time-to-event RWD | `d3_time_to_event_data/` | censoring assumptions, inverse probability weighting, multiple imputation, sensitivity analysis |

## Contributing

See `CONTRIBUTING.md` for the full guide.

In short:

1. Work in a group branch.
2. Open a Pull Request into `main`.
3. A maintainer reviews and merges.

## License

See `LICENSE`.
