# Bayesian Inference of Fat Tails in Bitcoin Returns
### Using the Metropolis–Hastings Algorithm

---

## Overview

Classical financial models assume daily returns follow a Gaussian distribution. For Bitcoin, this assumption fails badly — extreme returns occur far more often than a Gaussian model predicts. This project studies that failure quantitatively and builds a Bayesian solution using the **Metropolis–Hastings MCMC algorithm implemented from scratch**.

Three models are compared:

| Model | Log-Likelihood | 1% Daily VaR |
|-------|---------------|--------------| 
| Gaussian | 3608.51 | −7.61% |
| Classical Student-t (MLE) | 3828.53 | −10.02% |
| Bayesian Student-t (MH) | 3828.50 | −9.90% |

The Gaussian model understates extreme loss risk by **~2.4 percentage points** — roughly one-third in capital requirement terms.

---

## Repository Structure

```
Metropolis-Hastings/
├── Report.ipynb    # Full implementation notebook
├── Metropolis_Hastings.pdf      # Complete project report
└── README.md
```

---

## Technical Highlights

- **Two-stage MH sampler** built from scratch in Python
  - Stage 1: Infers degrees-of-freedom parameter ν alone · acceptance rate ~35%
  - Stage 2: Jointly infers (μ, σ, ν) in 3D · acceptance rate ~30%
- Full **MCMC diagnostics**: trace plots, autocorrelation functions, posterior histograms, burn-in analysis
- Posterior for ν concentrated in **[2.4, 3.2]** — confirming near-infinite kurtosis in Bitcoin returns
- Data: **1,826 days** of BTC-USD daily returns (January 2020 – December 2024) via Yahoo Finance

---

## Dependencies

```bash
pip install numpy scipy matplotlib pandas statsmodels yfinance
```

---

## Running the Notebook

```bash
git clone https://github.com/dokjawho/Metropolis-Hastings
cd Metropolis-Hastings
jupyter notebook Report.ipynb
```

---

## Key Results

The Bayesian posterior for the degrees-of-freedom parameter ν concentrates between 2.4 and 3.2, with mass centred near 2.6. Since kurtosis is only defined for ν > 4, this confirms Bitcoin returns carry **near-infinite kurtosis** — a critical finding for tail-risk estimation and capital allocation.

Both Student-t models outperform the Gaussian baseline by over 220 log-likelihood units and produce VaR estimates roughly one-third more conservative.

---

## Theory Covered

- Conditional probability and Bayes' theorem
- Markov chains, detailed balance, and ergodicity
- MCMC framework: burn-in, mixing, and convergence
- Metropolis–Hastings algorithm derivation
- Student-t distribution and fat tails
- Value at Risk (VaR) as a risk metric
