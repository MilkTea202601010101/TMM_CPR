# Cycle and Phase Recovery (CPR) Framework for Periodic Time-Series under Local Differential Privacy
---

## English

This repository provides the official publication-grade implementation of the **CPR (Cycle and Phase Recovery)** framework for protecting and recovering 1D continuous periodic time-series and motion trajectories under Local Differential Privacy (LDP) constraints. 

Unlike naive temporal smoothers, the CPR framework addresses the **SW-LDP coupling distortion**—where coordinate-wise Square Wave (SW) randomization disrupts spectral signals, shifts phase markers, and creates edge discontinuities—by integrating a joint spectral-temporal period search with a dedicated expectation-maximization (EM) and kernel density estimation (KDE) statistical inversion solver.

---

### 📂 Complete Codebase Structure

The project contains four highly specialized modules:

1.  **`cpr.py` (Core Mathematical Engine)**:
    *   *Multi-Scale Period Probing* (`stable_period_search`): Couples rFFT spectral estimates with temporal residual variance minimization.
    *   *Unsupervised Phase Synchronization* (`phase_template_reconstruct_sw`): Uses circular cross-correlation to align shifted cycles without a clean reference.
    *   *SW-Aware Denoising* (`sw_em_kde_estimation`): The complete, mathematically rigorous solver implementing the **SW-EM-KDE** mixture model, posterior updates, and density profiling.
2.  **`main.py` (System Evaluation Utility)**:
    *   Runs Monte Carlo iterations over varying LDP budgets ($\varepsilon \in [0.5, 5.0]$) scaled through a coefficient.
    *   Compares CPR against **LBD**, **DPRP**, and **CLDP** benchmarks using the **Reconstruction Cosine Distance** metric. Evaluated output is stored in `performance_plot.png`.
3.  **`LC.py` (Boundary Continuity Evaluator)**:
    *   Focuses exclusively on the smoothness of cyclic boundaries by logging the **Boundary Jump** ($\Delta_B$) metric over trajectory sequences (e.g., `taxi_7m.xlsx` / `taxi_2m.xlsx`). Output is plotted in `Boundary_Jump.png` without terminal print pollution.
4.  **`test.py` (Functional Sandbox & Visualizer)**:
    *   Runs a visual simulation test displaying the exact trajectory recovery curves.
    *   Integrates Savitzky-Golay post-refinement and directly prints Reconstruction **MSE** and **Correlation Coefficients** while saving `ldp_recon_result.png`.

---

### 🚀 Getting Started

#### System Setup

Verify your environment contains the required scientific computing libraries:

```bash
pip install numpy pandas torch matplotlib scipy openpyxl
