# Quantum-Wave-Packet-TDSE-Solver
Finite Difference Method (FDM) tridiagonal matrix solver for 1D Time-Dependent Schrodinger Equation: quantum tunneling and fractional revival dynamics.
# Quantum Wave Packet Dynamics: Simulating Particle-in-a-Box States using Numerical Matrix Methods

This repository contains the official Python Finite Difference Method (FDM) numerical solvers, simulation scripts, and figure datasets accompanying our research paper:

> **Title:** Quantum Wave Packet Dynamics: Simulating Particle-in-a-Box States using Numerical Matrix Methods  
> **Author:** Hussain Sheikh (Independent Researcher, Mumbai, India)  
> **Contact:** `hussainscientific783@gmail.com`  

---

## 1. Research Background & Objective
Modeling the precise spatial and temporal propagation of localized quantum wave packets inside confining potentials and across scattering barriers requires solving the Time-Dependent Schrödinger Equation (TDSE). When arbitrary potential disruptions or rectangular barriers are introduced, purely analytical approaches become intractable.

**The primary objective of this work is to construct a discrete, unitary tridiagonal matrix solver to simulate quantum tunneling across a central rectangular potential barrier and capture fractional quantum revival dynamics inside a 1D infinite potential well.**

---

## 2. Mathematical Methodology
In atomic units ($\hbar = 1, m = 1$), the continuous TDSE over domain $[0, L]$ is discretized onto a uniform spatial grid of $N$ points with step size $\Delta x = L/(N + 1)$ using the three-point central finite difference stencil:

$$H_{j,j} = \frac{1}{(\Delta x)^2} + V_j, \qquad H_{j,j\pm 1} = -\frac{1}{2(\Delta x)^2}$$

Time evolution is executed via exact matrix diagonalization ($\hat{H} = V D V^\dagger$) to construct the unitary time-evolution operator:

$$\hat{U}(\Delta t) = \exp(-i\hat{H}\Delta t) = V \exp(-i D \Delta t) V^\dagger$$

This single-decomposition architecture strictly preserves total probability norm $\int_0^L |\Psi(x,t)|^2 dx = 1$ to machine precision without iterative linear-system overhead.

---

## 3. Baseline Configuration & Repository Structure
All simulations operate under baseline parameters: **Box Length** $L = 10.0$, **Grid Resolution** $N \in [200, 300]$, **Spatial Variance** $\sigma = 0.4$, **Initial Momentum** $k_0 = 15.0$ ($\langle E \rangle \approx 112.5$), and **Time Step** $\Delta t = 0.005$:

### A. Matrix Solvers & Barrier Scattering Scripts
* **`matrix_solver.py` & `matrix_solver_v2.py`**: Core Finite Difference Method (FDM) solvers constructing the tridiagonal Hamiltonian matrix and unitary propagator $\hat{U}(\Delta t)$.
* **`quantum_scattering.py`**: Simulates Gaussian wave packet incidence ($x_0 = 3.0$) and tunneling across a central rectangular potential barrier ($x \in [5.0, 5.3]$) *(Reproduces **Figure 2** & **Figure 3**)*.
* **`quantum_data_generator.py`**: Computes transmission ($T$) and reflection ($R$) probability coefficients across barrier heights $V_{\max} \in [0.0, 500.0]$ at $t = 1.75$ (350 steps) *(Reproduces **Table 1**)*.

### B. Quantum Revival & Dispersion Scripts
* **`quantum_revival.py`**: Tracks free evolution ($x_0 = 5.0$), phase dispersion, and survival probability $F(t) = |\langle \Psi(x,0) | \Psi(x,t) \rangle|^2$, resolving the constructive fractional revival peak at $t = 1.416$ *(Reproduces **Figure 4** & **Figure 5**)*.
* **`quantum_data_generator_2.py`**: Automated batch script for computing revival fidelity metrics across simulation windows.

### C. Generated Figures
* **`Figure_1_matrix.png` & `Figure_2_matrix.png`**: Initial Gaussian wave packet state ($x_0 = 5.0$) and pre-scattering configuration ($x_0 = 3.0$).
* **`Figure_1_4_quantum.png` & `Figure_3_matrix.png`**: Real-time barrier tunneling, scattering, and hard-wall boundary reflection profiles.
* **`Figure_1_revival.png`**: Long-term survival probability $F(t)$ plot highlighting the fractional quantum revival peak at $t = 1.416$ ($T_{\text{rev}}/90$).

---

## 4. Key Quantitative Findings

| Barrier Height ($V_{\max}$) | Reflection ($R$) | Transmission ($T$) | Total Probability ($R + T$) | Physical Regime |
| :---: | :---: | :---: | :---: | :--- |
| $0.0$ | $0.9874$ | $0.0126$ | $1.0000$ | Free evolution & right-wall reflection |
| $100.0$ | $0.9317$ | $0.0683$ | $1.0000$ | Over-barrier scattering ($V_{\max} < \langle E \rangle$) |
| $200.0$ | $0.7855$ | $0.2145$ | $1.0000$ | Pure quantum tunneling & boundary overlap |
| $300.0$ | $0.9714$ | $0.0286$ | $1.0000$ | Strong exponential barrier attenuation |
| $400.0$ | $0.9994$ | $0.0006$ | $1.0000$ | Near-total barrier reflection |
| $500.0$ | $1.0000$ | $0.0000$ | $1.0000$ | Complete opaque barrier reflection |

* **Strict Unitarity ($R + T = 1.0000$):** Exact matrix diagonalization eliminates numerical dissipation across all barrier heights.
* **Fractional Quantum Revival:** The solver captures a distinct constructive self-interference fidelity peak $F(t) \approx 0.28$ at $t = 1.416$ ($T_{\text{rev}} \approx 127.32$).

---

## 5. Installation & Execution
Install the required Python packages (`numpy`, `scipy`, and `matplotlib`):

```bash
pip install numpy scipy matplotlib
```

Run the simulation scripts directly from your terminal:

```bash
python matrix_solver.py
python quantum_scattering.py
python quantum_data_generator.py
python quantum_revival.py
```

---

## 6. Citation
If you use these numerical solvers or refer to our findings in your research, please cite:

```bibtex
@article{sheikh2026quantum,
  title={Quantum Wave Packet Dynamics: Simulating Particle-in-a-Box States using Numerical Matrix Methods},
  author={Sheikh, Hussain},
  year={2026}
}
```
