# Temporal Bisection Task: HDDM Parameter Recovery Pipeline

This repository contains computational workflows for Bayesian parameter recovery and hierarchical model fitting using the **Hierarchical Drift-Diffusion Model (HDDM)** framework. The project evaluates model estimation accuracy across 1-stage and 2-stage Drift-Diffusion processes, as well as adaptive staircase protocols.

---

## ⚠️ Prerequisites & Environment Setup (`dockerHDDM`)

Due to specialized C/Cython extension dependencies and specific `kabuki`/`PyMC` backend requirements, **all notebooks in this repository must be run inside the official `dockerHDDM` container environment** to prevent compilation errors and ensure reproducible MCMC sampling.

### Running with Docker

Run the following command in your terminal to spin up the container environment mapping your current directory:

```bash
# Pull the latest dockerHDDM image
docker pull panlab/dockerhddm:latest

# Launch Jupyter Lab inside dockerHDDM
docker run -it --rm \
  -p 8888:8888 \
  -v "$(pwd)":/home/jovyan/work \
  panlab/dockerhddm:latest
```

Once running, navigate to `http://localhost:8888` in your web browser to open the notebooks.

---

## 📓 Notebook Architecture & Workflow

This repository consists of three core parameter recovery notebooks:

### 1. `Parameter_recovery-1and2StageDDM.ipynb`
* **Focus:** Comparative evaluation of 1-Stage vs. 2-Stage Drift-Diffusion dynamics.
* **Key Operations:**
  * Simulates synthetic behavioral datasets under single-stage and dual-stage drift accumulation architectures.
  * Fits hierarchical Bayesian models to recover baseline parameters: Drift Rate ($v$), Boundary Separation ($a$), Non-Decision Time ($t_0$), and Starting Point Bias ($z$).
  * Compares model fit and recovery precision between single and multi-stage decision assumptions.

### 2. `Parameter_recovery-HDDMgenerated.ipynb`
* **Focus:** Validation of parameter recovery using standard HDDM-generated datasets.
* **Key Operations:**
  * Uses built-in HDDM simulation tools to construct ground-truth hierarchical datasets across multiple subjects and condition levels.
  * Runs multi-chain MCMC sampling to assess posterior convergence using Gelman-Rubin ($\hat{R}$) diagnostics.
  * Computes correlation metrics ($r^2$, RMSE) and constructs ground-truth vs. estimated parameter recovery scatter plots ($y = x$).

### 3. `Parameter_recovery-STAIRCASE_2stageDDM.ipynb`
* **Focus:** Parameter recovery under adaptive psychometric staircase data collection protocols.
* **Key Operations:**
  * Models decision dynamics resulting from adaptive staircase stimulus presentation routines.
  * Evaluates how non-uniform trial distributions (focused around threshold boundaries) impact parameter estimation stability in 2-stage DDM architectures.
  * Quantifies boundary recovery confidence intervals and parameter shrinkage under adaptive sampling conditions.

---

## 📊 Notebook Comparison Overview

| Notebook File | Core Focus | Primary Modeling Objective |
| :--- | :--- | :--- |
| **`Parameter_recovery-1and2StageDDM.ipynb`** | Model Architecture Comparison | Compare 1-stage vs. 2-stage DDM parameter recovery performance. |
| **`Parameter_recovery-HDDMgenerated.ipynb`** | Synthetic Ground-Truth Recovery | Validate HDDM posterior estimation against HDDM-generated synthetic data. |
| **`Parameter_recovery-STAIRCASE_2stageDDM.ipynb`** | Adaptive Sampling Assessment | Evaluate 2-stage DDM recovery under adaptive staircase stimulus selection. |

---

## 🛠️ Key Dependencies (Pre-installed in `dockerHDDM`)

* `hddm` & `kabuki`
* `pymc` & `arviz`
* `numpy`, `scipy`, `pandas`
* `matplotlib`, `seaborn`

---

## 🚀 References

* **Pan et al. (2025):** *dockerHDDM: A User-Friendly Environment for Bayesian Hierarchical Drift-Diffusion Modeling.*
* **Wiecki, TV., Sofer, I., & Frank, MJ. (2013):** *HDDM: Hierarchical Bayesian estimation of the Drift-Diffusion Model in Python.*