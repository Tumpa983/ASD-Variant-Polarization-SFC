# SFC Variant Prioritization Pipeline

## Overview
This repository contains the computational validation pipeline, benchmark datasets, and diagnostic figures for the **SFC (SFARI × Func × CADD)** variant prioritization algorithm. The SFC score is a lightweight, deterministic algorithm designed to rank rare variants by integrating functional consequence severity with SFARI gene-level risk tiers. 

This repository serves as the supplementary data and reproducibility framework for a forthcoming peer-reviewed manuscript, demonstrating a high-accuracy, low-resource alternative to compute-heavy deep learning genomic models.

## Methodology
The SFC algorithm provides a transparent, CPU-efficient alternative to black-box deep learning predictors. It operates by applying a deterministic multiplier matrix to variants based on their Ensembl VEP consequence (e.g., frameshift, stop-gained, missense) and the biological risk tier of the host gene (derived from the SFARI Gene database). This approach isolates severe pathogenic signals without requiring GPU acceleration or massive model training.

## Key Findings
1. **Full-Cohort Validation:** SFC outperforms the baseline CADD (v1.3) predictor on a diverse multi-consequence cohort of 5,502 variants (AUROC 0.8421 vs. 0.8070, *p* < 0.001).
2. **Clinical Utility (Precision at K):** In a simulated diagnostic review, SFC achieved 100.0% precision within the Top 10 and Top 50 ranked variants, successfully isolating high-confidence pathogenic variants and drastically outperforming the CADD baseline (70.0% precision at Top 10).
3. **Score Calibration:** Decile binning confirms a strong upward relationship between the SFC score and real-world pathogenicity rates, ensuring clinical reliability at extreme score thresholds.
4. **Missense-Only Boundary Condition:** On a strictly matched subset of 836 missense variants, SFC underperforms dedicated missense predictors (AlphaMissense), demonstrating that its primary utility lies in inter-class multi-consequence prioritization rather than missense-only applications.
5. **Subject-Level Aggregation:** Evaluation across 2,866 subjects confirmed that while simple summation is partially confounded by total variant count, significant independent biological signal persists (Partial Spearman rho = 0.501, *p* < 0.001).

## Repository Structure
Click on any file below to view it directly in this repository:

- 📄 **[`SFC_Master_Pipeline.ipynb`](./SFC_Master_Pipeline.ipynb)**: The complete Jupyter notebook containing algorithm logic, AUROC/AUPRC calculations, AlphaMissense benchmarking, subject-level partial correlations, and clinical utility analyses.
- 🐳 **[`Dockerfile`](./Dockerfile)** & 📦 **[`requirements.txt`](./requirements.txt)**: Containerization configuration locked to exact environment versions for guaranteed reproducibility.
- 📊 **[`path_a_benchmark.csv`](./path_a_benchmark.csv)**: Head-to-head missense benchmarking results (CADD vs. SFC vs. AlphaMissense).
- 📊 **[`path_b_aggregation_diagnostic.csv`](./path_b_aggregation_diagnostic.csv)**: Statistical matrix evaluating the 8 subject-level aggregation schemes.
- 📈 **[`Precision_at_K.png`](./Precision_at_K.png)**: Clinical utility visualization comparing Top K review yields.
- 📈 **[`Calibration_Plot_Decile.png`](./Calibration_Plot_Decile.png)**: Calibration curve using decile binning.
- 📈 **[`Figure_PathB_BarChart.png`](./Figure_PathB_BarChart.png)**: Publication-ready bar chart of subject-level confounding diagnostics.

## Installation & Usage
The pipeline is designed to be highly accessible and can be executed via the provided Docker container to ensure environment consistency. 

**Method 1: Docker (Recommended)**
```bash
# 1. Build the container
docker build -t sfc-pipeline .

# 2. Run the container
docker run -p 8888:8888 sfc-pipeline
