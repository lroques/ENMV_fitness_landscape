# ENMV host adaptation model

This repository contains the code and posterior samples used to analyse host adaptation in Endive necrotic mosaic virus (ENMV) using a mechanistic approach derived from Fisher's geometric model.

The analysis infers host optima in an $n$-dimensional phenotypic space and compares models with different phenotype dimensions ($n = 1, 2, 3$).

The code produces all figures in the main text and appendices of the revised manuscript *Inferring the multi-host fitness landscape of endive necrotic mosaic virus from cross-inoculation experiments*.

---

# Repository contents

## Data

- `Data_RESISTE_ENMV.xlsx`  
  Experimental cross-inoculation dataset used in the analysis.

---

## Notebooks

### 1. Data exploration and statistical diagnostics

`ENMV_statistical_analysis.ipynb`

This notebook performs descriptive and diagnostic analyses of the experimental data without fitting the mechanistic model. It:

- reconstructs infection counts from the raw dataset
- visualizes infection success rates
- examines lineage variability
- quantifies overdispersion relative to a binomial model
- estimates the beta-binomial dispersion parameter $\kappa$

The notebook generates several diagnostic figures saved as PNG files.

---

### 2. Descriptive analysis of the cross-inoculation matrix

`descriptive_cross_inoculation_matrix_mds.ipynb`

This notebook performs model-free analyses of the aggregated cross-inoculation matrix. It:

- fits binomial generalized linear models with source, target, and sympatric effects
- tests whether the CL, CH, LA, and SA source profiles differ after accounting for target effects
- computes an empirical-logit transformation of the infection rates
- performs classical multidimensional scaling of the source infectivity profiles

The notebook generates the descriptive MDS figure reported in the appendix.

---

### 3. Bayesian inference of the mechanistic model

- `ENMV_MCMC_n1.ipynb`
- `ENMV_MCMC_n2.ipynb`
- `ENMV_MCMC_n3.ipynb`

These notebooks perform Bayesian inference of the mechanistic model for phenotype dimensions $n = 1, 2, 3$. They generate several figures saved as PNG files for use in the manuscript.

Each notebook:

- loads the experimental data
- runs a Metropolis MCMC sampler
- produces posterior predictive checks and summary figures
- saves posterior samples

Output files:

- `posterior_n1.pkl`
- `posterior_n2.pkl`
- `posterior_n3.pkl`

---

### 4. Model comparison

`Compare_dimensions.ipynb`

This notebook compares models with phenotype dimensions $n = 1, 2, 3$ using posterior samples.

For each model, it computes:

- WAIC (Widely Applicable Information Criterion)
- PSIS-LOO approximate leave-one-out cross-validation

---

### 5. Posterior decomposition of infection pathways

`posterior_pathway_decomposition_n2.ipynb`

This notebook uses the posterior samples from the $n = 2$ model to decompose the establishment intensity for each source-target pair into:

- direct establishment of the dominant source strain ($\mathrm{EST}$)
- rescue from standing variation in the source inoculum ($\mathrm{SV}$)
- de novo rescue in the target host ($\mathrm{DN}$)

The notebook generates the figure showing posterior mean infection probabilities and posterior mean pathway contributions.

Required input:

- `posterior_n2.pkl`

---

### 6. Sensitivity analysis for source standing variation

- `ENMV_MCMC_n2_alphaSV_0p5.ipynb`
- `ENMV_MCMC_n2_alphaSV_0p0.ipynb`

These notebooks refit the $n = 2$ mechanistic model after multiplying the contribution of source standing variation by a fixed factor $\alpha_{\mathrm{SV}}$.

The two values considered are:

- $\alpha_{\mathrm{SV}} = 0.5$, corresponding to a reduced contribution of source standing variation
- $\alpha_{\mathrm{SV}} = 0$, corresponding to complete removal of the source-standing-variation pathway

Each notebook:

- runs the Metropolis MCMC sampler
- produces posterior predictive checks
- computes posterior distance matrices
- produces MDS representations and parameter summaries
- saves posterior samples

Output files:

- `posterior_n2_alphaSV_0p5.pkl`
- `posterior_n2_alphaSV_0p0.pkl`

---

### 7. Alternative model with CL-like CH, LA, and SA source inocula

`ENMV_MCMC_n2_CL.ipynb`

This notebook fits an alternative $n = 2$ model in which the effective source phenotypes of CH-, LA-, and SA-evolved inocula are fixed at the clonal phenotype. CH, LA, and SA remain distinct target hosts with their own optima, radii, and infection-efficiency parameters.

The notebook:

- runs the Metropolis MCMC sampler
- produces posterior predictive checks
- computes posterior distance matrices
- produces an MDS representation and parameter summaries
- saves posterior samples

Output file:

- `posterior_n2_sources_CH_LA_SA_at_CL.pkl`

---

### 8. Individual-based validation of the branching-process approximations

`IBM_validation.nb`

This is a Mathematica notebook.

This notebook uses discrete burst-death simulations to validate the analytical approximations.

---

### 9. Numerical check of the approximations of $\overline{r_{jk}^{+}}$

`ENMV_closed_form.ipynb`

This notebook compares the exact quantity $\overline{r_{jk}^{+}}$ to the Gaussian and Laplace analytic approximations discussed in the manuscript.

---

# Posterior sample files

The repository contains the following posterior sample files:

- `posterior_n1.pkl`
- `posterior_n2.pkl`
- `posterior_n3.pkl`
- `posterior_n2_alphaSV_0p5.pkl`
- `posterior_n2_alphaSV_0p0.pkl`
- `posterior_n2_sources_CH_LA_SA_at_CL.pkl`

These files can be used to reproduce posterior summaries and figures without rerunning the MCMC analyses.

---

# Requirements

The notebooks require Python (tested with Python 3.9.0) and the following packages:

- numpy
- pandas
- scipy
- matplotlib
- openpyxl
- jupyter

To run the notebooks interactively, install Jupyter Notebook or JupyterLab in the same Python environment.

The notebook `IBM_validation.nb` requires Wolfram Mathematica (or Wolfram Player)
