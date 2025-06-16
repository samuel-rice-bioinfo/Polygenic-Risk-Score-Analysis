# Polygenic Risk Score Analysis for Blood Pressure Using PLINK and R

## Overview

This project demonstrates a complete PRS analysis pipeline applied to a genotype dataset related to blood pressure. It uses the PLINK toolset for quality control, SNP clumping, and PRS computation, followed by R-based statistical analysis to evaluate predictive performance.

## Objectives

* Perform quality control on genotype data
* Conduct linkage disequilibrium (LD) clumping
* Build PRS models using SNPs filtered by p-value thresholds
* Assess PRS performance using R² statistics and logistic regression
* Visualize and interpret prediction outputs

## Tools Used

* **PLINK v1.9** for GWAS data processing and PRS computation
* **AWK** for text and file manipulation
* **R** for statistical modeling, PRS evaluation, and visualizations
* **ggplot2** for plots
* **Ubuntu Terminal** as the execution environment

## Pipeline Summary

### 1. Quality Control

* Computed genotyping rates with `--missing`
* Extracted SNP and sample counts using `.bim` and `.fam`
* Identified samples with >5% missing data

### 2. Linkage Disequilibrium (LD) Clumping

* Performed LD clumping with parameters:

  * `--clump-p1 0.9`
  * `--clump-r2 0.3`
  * `--clump-kb 350`
* Extracted index SNPs post-clumping

### 3. PRS Computation

* Built PRS models at 8 p-value thresholds (1 to 0.001) using `--score` and `--q-score-range`
* Addressed SNP mismatches in predictor files

### 4. PRS Evaluation in R

* Merged PRS scores with phenotype data
* Ran linear regression models for each threshold
* Calculated R², beta, SE, and p-values
* Saved a summary table of PRS performance
* Visualized predictive power across thresholds using `ggplot2`

### 5. Logistic Regression & Prediction

* Modeled case/control status using best PRS (p ≤ 0.001)
* Predicted probabilities and plotted PRS vs true outcome
* Extracted predicted probability for individual samples

## Key Results

| P-Value Threshold | R²       | P-value  | Beta     | SE       |
| ----------------- | -------- | -------- | -------- | -------- |
| ≤ 0.001           | 0.002975 | 0.014974 | 0.666076 | 0.273528 |
| ≤ 0.05            | 0.002351 | 0.030584 | 2.515925 | 1.162633 |
| ≤ 1               | 0.001306 | 0.107072 | 5.395585 | 3.346667 |

* Best predictive power achieved with p ≤ 0.001 threshold.
* Logistic regression confirmed weak but statistically significant PRS signal (AUC not included here).
* Predicted probability for individual #10: **0.509**

## File Contents

* `plink_commands.txt` – all PLINK terminal commands used
* `awk_scripts.txt` – text processing steps for count summaries
* `prs_analysis.R` – full R script for evaluating and plotting PRS
* `prs_results_summary.csv` – PRS performance results
* `prs_plot.png` – PRS predictive performance plot
* `blood_pressure_prs.range*.profile` – PRS score files by threshold

## References

* [PLINK v1.9](https://www.cog-genomics.org/plink/)
* Choi & O’Reilly (2019). *PRSice-2: Polygenic Risk Score software*
* Wray et al. (2013). *Pitfalls of predicting complex traits from SNPs*
* Osterman et al. (2024). *Cross-validation for PRS robustness*
