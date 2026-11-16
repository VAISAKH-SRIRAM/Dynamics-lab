# Dynamics Lab

> **Zero-Dependency Nonlinear Dynamics & Chaos Engine in a Single Self-Contained HTML File**

[![License: MIT](https://img.shields.io/badge/License-MIT-white.svg?style=flat-square)](LICENSE)
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-0-white.svg?style=flat-square)](#)
[![Pure Vanilla JS](https://img.shields.io/badge/Engine-Vanilla%20JS%20%2F%20Canvas2D-white.svg?style=flat-square)](#)

[**Live Interactive Demo »**](https://vaisakh-sriram.github.io/dynamics-lab/)

---

## Overview

**Dynamics Lab** is an interactive, browser-based numerical laboratory for simulating ordinary differential equations (ODEs), nonlinear dynamics, and chaotic attractors in real time.

Built in pure vanilla JavaScript and HTML5 Canvas, it runs as a **single, self-contained HTML codefile with zero dependencies, zero npm packages, and zero build pipelines**. Every model, parameter set, and view configuration is encoded directly into the URL hash, making any simulation an instantaneously runnable permalink.

---

## Key Features

### 1. Multi-Solver Integration Engine
* **RK4:** Classical 4th-order Runge-Kutta integrator with fixed time-step.
* **RK45 Dormand-Prince (`ode45`):** 7-stage Butcher tableau adaptive step-size integrator matching MATLAB's standard `ode45`.
* **Symplectic Verlet:** Reversible, energy-conserving leapfrog integrator designed for Hamiltonian physical systems and celestial orbits.

### 2. Real-Time Chaos Diagnostics
* **Maximal Lyapunov Exponent ($\lambda$):** Continuous tracking of twin trajectories separated by an infinitesimal perturbation ($d_0 = 10^{-8}$) with Benettin step-by-step reorthonormalization.
* **Instant Regimes Classification:** Categorizes solutions as Stable Fixed Point, Limit Cycle / Torus, or Deterministic Chaos ($\lambda > 0$).

### 3. Automated Fixed-Point & Stability Analysis
* **Root Finding:** Multi-start Newton-Raphson finder with finite-difference Jacobian evaluation.
* **Exact Eigenvalue Solver:** Analytical 2D trace-determinant classification and 3D Cardano/Viète characteristic cubic equation solver.
* **Stability Classification:** Automatic identification of Saddle Points, Stable Nodes, Spiral Sinks, and Saddle-Foci.

### 4. 7 Scientific Analysis Views
1. **2D Phase Portrait:** Vector quiver fields, analytical nullclines, click-to-seed trajectories, and Monte Carlo swarm particle dispersion.
2. **3D Attractor:** Full spherical orbital rotation, multi-touch dual-finger pinch zoom, velocity-gradient coloring, and playback comet trails.
3. **Time Series:** Multi-variable synchronous trajectory graphs with time scrubbing.
4. **Sensitivity:** Real-time demonstration of the butterfly effect with twin perturbed trajectories ($10^{-5}$).
5. **Bifurcation Diagrams:** Automated parameter sweeps detecting period-doubling cascades and transitions to chaos.
6. **Poincaré Cross-Sections:** Hyperplane piercing detection with linear interpolation.
7. **FFT Power Spectrum:** In-place Radix-2 Cooley-Tukey Fast Fourier Transform for identifying discrete frequencies vs. chaotic broadband noise.

### 5. Seamless Code Generation & Export
* **MATLAB / GNU Octave:** Generates complete, runnable standalone `.m` scripts utilizing `ode45`.
* **Python / SciPy:** Exports ready-to-run `.py` scripts utilizing `scipy.integrate.solve_ivp` and `matplotlib`.
* **Raw Data & Visuals:** Instant export to CSV tabular time-series and high-resolution PNG snapshots.

### 6. Fully Mobile Responsive
* Adaptive two-mode architecture: switches seamlessly between a full-screen simulation canvas (`100dvh`) and a dedicated controls drawer.
* Native multi-touch gestures: 1-finger 3D orbital drag, 2-finger pinch-to-zoom, and 2-finger pan.

---

## 14 Built-In Systems

| Model | Classification | Description |
|---|---|---|
| **Lorenz System (1963)** | 3D Chaos | Atmospheric thermal convection model with classic butterfly attractor |
| **Rössler Attractor (1976)** | 3D Chaos | Minimal chemical kinetics model with single-band spiral chaos |
| **Van der Pol Oscillator (1920)** | 2D Limit Cycle | Vacuum tube relaxation oscillator with non-conservative nonlinear damping |
| **Duffing Oscillator (1918)** | 2D/Non-autonomous | Double-well potential oscillator under periodic sinusoidal forcing |
| **Lotka-Volterra (1925)** | 2D Biological | Nonlinear predator-prey population dynamics |
| **Chua's Circuit (1983)** | 3D Physical Chaos | Physical non-linear electronic circuit producing double-scroll attractor |
| **Thomas' Attractor** | 3D Symmetric Chaos | Dissipative cyclically symmetric labyrinth chaos |
| **Halvorsen Attractor** | 3D Cyclic Chaos | Highly symmetric cyclic chaotic system with triple lobes |
| **Aizawa Attractor** | 3D Toroidal Chaos | Spherical core attractor with vertical axial jet outflow |
| **Chen Attractor (1999)** | 3D Dual-Scroll | Dual-scroll chaotic attractor with complex topological structure |
| **Rikitake Dynamo** | 3D Geomagnetic Chaos | Two-disk geomagnetic field reversal dynamo |
| **Sprott Case B** | 3D Minimal Chaos | Simplest 3-variable quadratic chaotic differential system |
| **Hindmarsh-Rose (1984)** | 3D Neurodynamics | Neural bursting and action-potential firing model |
| **Forced Damped Pendulum** | 2D/Non-autonomous | Rigid pendulum with damping and sinusoidal periodic drive torque |

---

## Quickstart

No dependencies, no bundlers, no npm, and no servers required.

```bash
# Clone the repository
git clone https://github.com/VAISAKH-SRIRAM/dynamics-lab.git
cd dynamics-lab

# Open directly in any web browser
open dynamics-lab.html
```

---

## Project Structure

```text
dynamics-lab/
├── dynamics-lab.html   # Complete, self-contained single-file application
├── index.html          # Entrypoint for GitHub Pages hosting
├── logo.png            # Official brand logo
├── favicon.png         # Browser favicon icon
└── README.md           # Project documentation
```

---

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for more details.
