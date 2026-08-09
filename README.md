# Age-Aware Hybrid SOC–SOH Estimation

A hybrid physics-informed framework for real-time State of Charge (SOC) 
and State of Health (SOH) estimation of lithium-ion batteries.

## Overview

Accurate SOC estimation becomes challenging as lithium-ion batteries age due 
to capacity degradation, internal resistance growth, nonlinear dynamics, 
and model parameter drift.

This project combines:

- Gaussian Process Regression (GPR) for cycle-dependent capacity degradation
- A second-order Equivalent Circuit Model (ECM) for battery dynamics
- Information Fusion Optimization (INFO) for Particle Filter hyperparameter tuning
- Particle Filtering (PF) for nonlinear and probabilistic SOC estimation
- SOH-aware updates of battery parameters across ageing conditions

## Methodology

The overall pipeline is:

GPR → SOH parameter estimation → 2nd-order ECM → INFO optimization → Particle Filter → SOC estimation

### 1. SOH Estimation

GPR models battery degradation from charge-discharge cycle features and 
predicts the cycle-dependent rated capacity.

### 2. Battery Modeling

A second-order ECM models the battery's electrical dynamics using SOC and 
two RC polarization states.

### 3. INFO Optimization

The INFO algorithm optimizes Particle Filter hyperparameters including 
particle initialization and process-noise parameters.

### 4. Particle Filter

The Particle Filter estimates SOC using the nonlinear ECM dynamics and 
measured battery voltage/current.

### 5. Age-Aware Adaptation

Cycle-dependent capacity and internal resistance information are incorporated 
into the ECM and Particle Filter to account for battery ageing.

## Dataset

Experiments use the NASA Prognostics Center of Excellence lithium-ion battery 
ageing dataset.

Cells B0005, B0006, and B0007 are evaluated across different stages of battery ageing.

## Results

INFO optimization significantly improved Particle Filter performance:

| Metric | Baseline PF | INFO-Optimized PF |
|---|---:|---:|
| SOC RMSE | 0.0678 | 0.0113 |
| Voltage RMSE (V) | 0.3035 | 0.0418 |

The SOH-aware capacity update also prevented substantial SOC drift under ageing.

Using nominal capacity instead of the estimated aged capacity resulted in 
nearly 12% SOC overestimation by the end of the constant-current phase.

## Technologies

- Python
- NumPy
- Pandas
- Scikit-learn
- Gaussian Process Regression
- Particle Filters
- Equivalent Circuit Models
- INFO Optimization
- Matplotlib
- Jupyter / Google Colab

## Repository Structure

```text
age-aware-soc-soh-estimation/
│
├── Age_Aware_SOC_SOH_Estimation.ipynb
└── README.md
