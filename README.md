# SFC Variant Prioritization Benchmarking

## Overview
This repository contains the computational validation pipeline, benchmark datasets, and diagnostic figures for the **SFC (SFARI Functional Consequence)** variant prioritization algorithm. The SFC score is a lightweight, deterministic algorithm designed to rank rare variants by integrating functional consequence severity with SFARI gene-level risk tiers. 

This repository serves as the supplementary data and reproducibility framework for our ICEEICT 2027 manuscript.

## Key Findings
1. **Full-Cohort Validation:** SFC outperforms the baseline CADD (v1.3) predictor on a multi-consequence cohort of 5,502 variants (AUROC 0.8421 vs. 0.8070, $p < 0.001$).
2. **Missense-Only Boundary Condition:** On a matched subset of 836 missense variants, SFC underperforms dedicated missense predictors (AlphaMissense, CADD), demonstrating that SFC's primary utility lies in inter-class multi-consequence prioritization rather than missense-only applications.
3. **Subject-Level Aggregation:** Evaluation of 8 patient-level aggregation schemes across 2,866 subjects confirmed that while simple summation is partially confounded by total variant count, significant independent biological signal persists ($\rho_{\text{partial}} = 0.5387, p < 10^{-215}$ for the Rank-Sum formulation).

## Repository Contents
Click on any file below to view it directly in this repository:

* 📄 **[`SFC_Master_Pipeline.ipynb`](./SFC_Master_Pipeline.ipynb)**: The complete Jupyter/Kaggle notebook containing the algorithm logic, variant-level AUROC/AUPRC calculations, AlphaMissense coordinate matching, and subject-level partial Spearman correlation diagnostics.
* 📊 **[`path_a_benchmark.csv`](./path_a_benchmark.csv)**: Head-to-head missense benchmarking results (CADD vs. SFC vs. AlphaMissense).
* 📊 **[`path_b_aggregation_diagnostic.csv`](./path_b_aggregation_diagnostic.csv)**: Statistical matrix evaluating the 8 subject-level aggregation schemes (Raw $\rho$, Partial $\rho$, 95% CIs, and $p$-values).
* 📈 **[`Figure_PathB_BarChart.png`](./Figure_PathB_BarChart.png)**: Publication-ready bar chart of the subject-level confounding diagnostics. *(Note: Additional visualizations like ROC/PR curves can be found in the root directory).*

## Reproducibility & Datasets
The pipeline is designed to execute within a standard Kaggle environment to manage memory overhead when parsing large external datasets. 

* **Primary Dataset:** [VariCarta](https://varicarta.msl.ubc.ca/) (Coordinates standardized to the hg19 reference genome).
* **Clinical Truth Labels:** [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/).
* **External Benchmarks:** 
  * CADD v1.3 (embedded dynamically in the VariCarta INFO field).
  * [AlphaMissense](https://zenodo.org/records/8208688) (hg19 TSV release, processed dynamically via `awk` in the notebook to minimize memory footprint).
