## 🔬 Uncertainty-Aware Stacked Physics-Informed Neural Networks  
### Permeability Prediction in Deep Coal Reservoirs

*Physics-consistent, uncertainty-calibrated, and interpretable machine learning framework*

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/)  
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.5.2-yellow.svg)](https://scikit-learn.org/stable/)  
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)](https://pytorch.org/)  
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📖 Overview

This repository contains the complete, reproducible implementation of an
uncertainty-aware stacked physics-informed learning framework for predicting permeability in data-scarce deep coal reservoirs.

The framework integrates:

- Data-driven neural networks (ANN)
- Physics-informed neural networks (PINN1, PINN2)
- A stacked meta-learner (Stacked_PINN)
- Gaussian Process Regression (GPR) baseline
- Rigorous uncertainty quantification, physics-violation diagnostics, and interpretability

The objective is not only predictive accuracy, but also physical consistency, calibrated uncertainty, and identifiable governing parameters, enabling trustworthy deployment in subsurface energy applications such as coalbed methane (CBM) and CO₂-enhanced coalbed methane (CO₂-ECBM).

--

## 🧭 Scientific Objectives

- Predict coal permeability using NMR-derived pore structure descriptors
- Embed physically motivated permeability laws into neural networks
- Quantify epistemic uncertainty using ensemble learning and MC dropout
- Evaluate physics consistency beyond pointwise error metrics
- Assess parameter identifiability and recoverability
- Provide exact, faithful interpretability using Shapley values

---

## 🧱 Input Features & Target

The NMR-derived pore descriptors are found in "Liu_et_al_2024.xlsx" and can also be found in Table 2 of Ref ([Integrated NMR Analysis for Evaluating Pore-Fracture Structures and Permeability in Deep Coals: A One-Stop Approach](https://doi.org/10.1021/acs.energyfuels.3c05166))

- Inputs (no measured permeability used):
    . Seepage pore porosity, φₛ (%)
    . Adsorption pore porosity, φₐ (%)
    . Seepage pore fractal dimension, Dₛ
    . Reservoir Quality Index, RQI (μm)

- Target:
    . Seepage-pore permeability, (kₚ (10⁻³ μm²))

This ensures predictions arise solely from intrinsic pore-structure information, avoiding implicit calibration.

---

⚙️ Model Architecture
1️⃣ Artificial Neural Network (ANN)

- Fully data-driven baseline
- Optimized via Bayesian NAS (Optuna)
- Provides a performance benchmark

2️⃣ Physics-Informed Neural Networks

- PINN1 – Seepage porosity constraint
- PINN2 – Dual-porosity constraint

. Physics enforced via soft-constrained loss terms
. Physical parameters learned during training
. Positivity enforced using softplus transformations

3️⃣ Stacked Physics-Informed Network (Stacked_PINN)

- Combines predictions from PINN1 and PINN2
- Uses predictive mean and uncertainty as meta-features
- Learns a robust permeability estimate while preserving physical structure
- Acts as a regularized physics-consistent surrogate

4️⃣ Gaussian Process Regression (GPR)

- Probabilistic benchmark with closed-form uncertainty
- Strong interpolation capability
- Limited scalability and extrapolation

🔁 Training & Uncertainty Quantification

- 70/15/15 train–validation–test split
- Standardization using training statistics only
- Bayesian neural architecture search (Optuna)
- Bootstrap ensembling with out-of-bag validation
- Monte Carlo dropout for epistemic uncertainty
- Predictive mean ± kσ intervals for coverage analysis

---

## 🧪 Diagnostics & Evaluation

✔️ Accuracy
- RMSE, MAE, MAPE, R²
- Probabilistic dominance analysis

✔️ Physics Consistency

- Physics-violation metric:
- Evaluated across feature subspaces:
    . φₛ–φₐ
    . φₛ–Dₛ
    . φₛ–RQI

✔️ Uncertainty Calibration

- Coverage probability tests
- Violation–uncertainty correlation analysis

---

## 🔍 Interpretability

- Exact Shapley values via full subset enumeration
- No approximation bias
- Consistent local and global explanations
- Applied to both base models and stacked meta-model

---

## 🧬 Physics Parameter Identifiability

- Extract learned parameters:
    . PINN1: a, b
    . PINN2: c, m, n
- Back-fit analytical permeability equations to Stacked-PINN predictions
- Bootstrap confidence intervals (95%)
- Demonstrates recoverability without bias, even under stacking

---

## 📊 Key Findings

- ANN achieves competitive accuracy but violates physics
- Standalone PINNs reduce violations but remain sensitive
- Stacked-PINN provides the best balance:
    . Suppressed physics violations
    . Calibrated uncertainty
    . Stable residuals
    . Preserved physical interpretability
- GPR performs strongly locally but lacks scalability
- Learned physics parameters remain identifiable and recoverable

---

## 📁 Repository Structure

model_outputs/
├── models/        # Trained ensembles + GPR
├── preds/         # Predictions & uncertainties
├── shap/          # Exact Shapley values
├── params/        # Physics parameter analysis
├── nas/           # Optuna studies & plots
├── figures/       # Diagnostic plots
├── data/          # Raw & processed datasets

---

## ⚙️ Installation & Reproducibility

git clone https://github.com/HRNBEnninful/Uncertainty-Aware-Stacked-PINN-Permeability.git
cd Permeability_Final
pip install -r requirements.txt

All experiments are fully reproducible via saved artifacts and manifest files.

---

## 📜 License

MIT License – free to use and modify.

---

## 📬 Author

- Developed By: Henry Reynolds Nana Benyin Enninful
- 📧 Email: hrnbenninful@gmail.com
- 🐙 GitHub: @HRNBEnninful
- 💼 LinkedIn: https://www.linkedin.com/in/henryrnbenninful/

---

## 📌 Related Publications

Applied Energy (under review)
