# SOC_Simulation_PIML_db4-Wavelets
Soil Organic Carbon (SOC) simulation under Shared Socioeconomic Pathways (SSP126, SSP245, SSP370 &amp; SSP585) using XGBoost-based Physics-informed Machine Learning (PIML) and Daubechies-4 wavelet decomposition.

## Repository Overview

This repository contains Python scripts used to simulate and analyse future trajectories of soil organic carbon (SOC) stocks using a physics-informed machine learning (PIML) framework combined with wavelet-based time-series analysis.

The workflow consists of three major components:

1. **Dataset construction**
   - Spatial datasets (soil, land use, and climate variables) are integrated from multiple sources including LUH2 land-use projections and bias-corrected climate model outputs.
   - Multi-model ensemble climate variables are aggregated seasonally and annually.
   - Baseline and future datasets are generated for each grid cell using rolling temporal windows.

2. **Physics-informed machine learning modelling**
   - SOC stock is modelled using XGBoost regression with monotonic constraints representing known soil–climate relationships.
   - Bias correction is applied using smearing estimators and national SOC stock anchoring.
   - Ensemble modelling and quantile regression are used to quantify predictive uncertainty.
   - Model explainability is analysed using SHAP values.

3. **SOC projection and temporal analysis**
   - The trained PIML model is used to generate SOC projections for SSP126, SSP245, SSP370, and SSP585 scenarios.
   - Time-series signals are decomposed using Daubechies-4 wavelet decomposition.
   - Long-term SOC trends are analysed using Mann–Kendall tests, Sen’s slope, generalized additive models (GAM), and breakpoint detection.

The scripts also generate all tables and figures used in the analysis, including uncertainty diagnostics, SHAP feature importance, and wavelet-derived trend trajectories.

## Scripts / Notebooks

### `S1_PIML_Modelling.ipynb`

Builds the physics-informed machine learning model for SOC prediction.  
The script:

- constructs baseline and future predictor datasets
- trains constrained and unconstrained XGBoost models
- applies bias correction and anchoring to match national SOC totals
- quantifies prediction uncertainty using ensemble and quantile models
- generates SOC projections for SSP scenarios
- produces diagnostic plots, SHAP analysis, and learning curves

---

### `S2_Wavelet_Approximation.ipynb`

Performs wavelet-based analysis of projected SOC trajectories.  
The script:

- decomposes SOC time series using Daubechies-4 wavelets
- extracts low-frequency SOC trend signals (A3 and A5 approximations)
- detects structural breakpoints using the PELT algorithm
- evaluates trend significance using Mann–Kendall tests and Sen’s slope
- fits GAM smoothers to compare long-term trajectories
- analyses regime-wise SOC sequestration rates
- generates visualisations and statistical summaries of SOC trends.

## Data Availability
The datasets required to run the scripts are archived on Zenodo accessible at https://doi.org/10.5281/zenodo.18884892. The archive contains the processed spatial datasets used for SOC modelling, including climate forcings, LUH2 land-use forcings, and other static geoenvironmental features required to reproduce the simulations.

**Data Citation:** Majid, S. I. (2026). Geostatistical Dataset for Topsoil Organic Carbon Modelling in India Using CMIP6 Climate Projections and LUH2 Land Use Data [Data set]. Zenodo. https://doi.org/10.5281/zenodo.18884892
