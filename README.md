# ENMV host adaptation model

This repository contains the code and posterior samples used to analyse host adaptation in **Endive necrotic mosaic virus (ENMV)** using a mechanistic approach derived from Fisher's geometric model.

The analysis infers host optima in an $n$-dimensional phenotypic space and compares models with different phenotype dimensions ($n = 1, 2, 3$).

The code produces all figures in the main text and appendices of the manuscript *Inferring the multi-host fitness landscape of endive necrotic mosaic virus from cross-inoculation experiments*.

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

### 2. Bayesian inference of the mechanistic model

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

### 3. Model comparison

`Compare_dimensions.ipynb`

This notebook compares models with phenotype dimensions $n = 1, 2, 3$ using posterior samples.

For each model, it computes:

- WAIC (Widely Applicable Information Criterion)
- PSIS-LOO approximate leave-one-out cross-validation

---

### 4. Numerical check of the approximations of $\Pi_{jk}$

`ENMV_closed_form.ipynb`

This notebook compares the exact quantity $\Pi_{jk}$ to the two analytic approximations discussed in the manuscript.

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

