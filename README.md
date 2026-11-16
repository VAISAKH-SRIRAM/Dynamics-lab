<div align="center">
  <img src="logo.png" alt="Dynamics Lab Logo" width="96" height="96">
</div>

```text
  ____  __   __ _   _    _    __  __ ___ ____ ____    _        _    ____  
 |  _ \ \ \ / /| \ | |  / \  |  \/  |_ _/ ___/ ___|  | |      / \  | __ ) 
 | | | | \ V / |  \| | / _ \ | |\/| || | |   \___ \  | |     / _ \ |  _ \ 
 | |_| |  | |  | |\  |/ ___ \| |  | || | |___ ___) | | |___ / ___ \| |_) |
 |____/   |_|  |_| \_/_/   \_\_|  |_|____\____|____/  |_____/_/   \_\____/ 
```

<div align="center">

**Nonlinear Dynamics & Chaos Engine — Single-File, Zero-Dependency Browser Simulator**

[![License: MIT](https://img.shields.io/badge/License-MIT-black.svg?style=flat-square)](LICENSE)
[![Dependencies: 0](https://img.shields.io/badge/Dependencies-0-black.svg?style=flat-square)](#)
[![Engine: Vanilla JS](https://img.shields.io/badge/Engine-Vanilla%20JS%20%2F%20Canvas2D-black.svg?style=flat-square)](#)
[![Platform: Web & Mobile](https://img.shields.io/badge/Platform-Web%20%7C%20Mobile-black.svg?style=flat-square)](#)

[**Launch Interactive Simulator**](https://vaisakh-sriram.github.io/Dynamics-lab/)

</div>

---

## Overview

**Dynamics Lab** is an interactive numerical laboratory for simulating ordinary differential equations (ODEs), nonlinear dynamics, and chaotic attractors in real time.

Engineered entirely in pure vanilla JavaScript and HTML5 Canvas2D, it operates as a **single, self-contained HTML file with zero dependencies, zero npm packages, and zero build pipelines**. Every model equation, parameter state, and view configuration is encoded directly into the URL hash permalink, allowing instantaneous sharing and offline execution.

---

## System Architecture

```text
+-----------------------------------------------------------------------------------------+
|                                 DYNAMICS LAB ENGINE                                     |
+-----------------------------------------------------------------------------------------+
                                             |
                              [ Mathematical Expression Stream ]
                                             |
                                             v
+---------------------------+   +---------------------------+   +-------------------------+
|     RECURSIVE-DESCENT     |-->|       JIT COMPILER        |-->|     SOLVER SELECTOR     |
|   Tokenizer & AST Engine  |   |     F(t, y, p, out)       |   |   RK4 / RK45 / Verlet   |
+---------------------------+   +---------------------------+   +-------------------------+
                                                                             |
                                             +-------------------------------+------------+
                                             v                                            v
+--------------------------------------------------------+   +--------------------------------------------+
|                 NUMERICAL INTEGRATION                  |   |             CHAOS & STABILITY              |
|  * Classical 4th-Order Runge-Kutta (RK4)               |   |  * Maximal Lyapunov Exponent (Benettin)    |
|  * Dormand-Prince 5(4) Adaptive Integrator (ode45)     |   |  * Multi-Start Newton-Raphson Root Finder  |
|  * Symplectic Leapfrog (Energy-Conserving Verlet)      |   |  * Analytical Cardano/Viete 3x3 Eigenvalues|
+--------------------------------------------------------+   +--------------------------------------------+
                                             |                                            |
                                             +-------------------------------+------------+
                                                                             v
+-----------------------------------------------------------------------------------------+
|                                   7 SCIENTIFIC VIEWPORTS                                |
|   [2D Phase Flow]   [3D Attractor]   [Time Series]   [Sensitivity]   [Bifurcation] ...  |
+-----------------------------------------------------------------------------------------+
                                             |
                                             v
+-----------------------------------------------------------------------------------------+
|                   HARDWARE-ACCELERATED CANVAS2D  +  URL HASH PERMALINK                  |
+-----------------------------------------------------------------------------------------+
```

---

## Core Capabilities

### 1. Multi-Solver Integration Suite
* **RK4:** Classical 4th-order Runge-Kutta integrator with deterministic fixed step-size.
* **RK45 Dormand-Prince (`ode45`):** 7-stage Butcher tableau adaptive step-size integrator matching MATLAB's standard numerical engine.
* **Symplectic Verlet:** Time-reversible, energy-preserving leapfrog scheme for Hamiltonian and orbital mechanics.

### 2. Chaos Quantification & Lyapunov Exponents
* **Maximal Lyapunov Exponent ($\lambda$):** Continuous measurement of trajectory divergence under infinitesimal perturbation ($d_0 = 10^{-8}$) with Benettin reorthonormalization.
* **Regime Classification:** Automatically categorizes dynamics into **Stable Equilibrium**, **Limit Cycle / Torus**, or **Deterministic Chaos ($\lambda > 0$)**.

### 3. Automated Equilibrium & Stability Analysis
* **Newton-Raphson Root Finding:** Multi-start search discovering fixed points across phase space ($F(x^*) = 0$).
* **Exact Analytical Eigenvalues:** Quadratic discriminant classification for 2D systems, plus **Cardano / Viete cubic solver** for 3D systems.
* **Hyperbolic Point Classification:** Differentiates Saddle Points, Stable Nodes, Spiral Sinks, and Saddle-Foci.

### 4. 7 Scientific Analysis Workspaces
1. **2D Phase Portrait:** Direction quiver vector fields, analytical nullclines, click-to-seed trajectories, and Monte Carlo particle swarms.
2. **3D Attractor:** 3-axis spherical orbital rotation, two-finger pinch-to-zoom, velocity-gradient coloring, and comet animation trails.
3. **Time Series:** Multi-variable synchronous trajectory plotting with scrubbable playback.
4. **Sensitivity:** Real-time demonstration of the butterfly effect with twin perturbed trajectories ($10^{-5}$).
5. **Bifurcation Diagrams:** Automated parameter sweeps detecting period-doubling cascades and transitions to chaos.
6. **Poincaré Cross-Sections:** Hyperplane piercing detection with sub-step linear interpolation.
7. **FFT Power Spectrum:** In-place Radix-2 Cooley-Tukey Fast Fourier Transform for identifying harmonic frequencies vs. chaotic broadband noise.

### 5. Interoperability & Code Generation
* **MATLAB / GNU Octave:** Generates complete, runnable standalone `.m` scripts utilizing `ode45`.
* **Python / SciPy:** Exports ready-to-run `.py` scripts utilizing `scipy.integrate.solve_ivp` and `matplotlib`.
* **Raw CSV & Snapshots:** Instant export to CSV tabular time-series and high-resolution PNG captures.

### 6. Mobile Responsive Interface
* Adaptive two-mode layout: switches between a full-screen simulation canvas (`100dvh`) and a dedicated controls drawer.
* Native multi-touch gestures: 1-finger 3D orbital drag, 2-finger pinch-to-zoom, and 2-finger pan.

---

## 14 Pre-Loaded Dynamic Systems

| Model | Dimensions | Regime | Description |
|---|---|---|---|
| **Lorenz System (1963)** | 3D | Chaos | Atmospheric convection model exhibiting the canonical butterfly attractor |
| **Rössler Attractor (1976)** | 3D | Chaos | Minimal chemical reaction model with a single folded band |
| **Van der Pol Oscillator (1920)** | 2D | Limit Cycle | Non-conservative triode oscillator with nonlinear damping |
| **Duffing Oscillator (1918)** | 2D (Forced) | Chaos | Periodically forced oscillator with a double-well potential |
| **Lotka-Volterra (1925)** | 2D | Conservative | Nonlinear ecological model of predator-prey dynamics |
| **Chua's Circuit (1983)** | 3D | Chaos | Physical electronic circuit producing double-scroll chaos |
| **Thomas' Attractor** | 3D | Chaos | Cyclically symmetric dissipative labyrinth system |
| **Halvorsen Attractor** | 3D | Chaos | Cyclic permutation system with three symmetric lobes |
| **Aizawa Attractor** | 3D | Chaos | Spherical core attractor with vertical axial jet outflow |
| **Chen Attractor (1999)** | 3D | Chaos | Dual-scroll attractor with complex topological structure |
| **Rikitake Dynamo** | 3D | Chaos | Two-disk geomagnetic field reversal dynamo |
| **Sprott Case B** | 3D | Chaos | Minimal 3-variable quadratic chaotic differential system |
| **Hindmarsh-Rose (1984)** | 3D | Bursting | Neuronal membrane potential bursting and spike train model |
| **Forced Damped Pendulum** | 2D (Forced) | Chaos | Physical rigid pendulum under periodic driving torque |

---

## Quickstart

No Node.js, npm, bundlers, or servers required:

```bash
# Clone the repository
git clone https://github.com/VAISAKH-SRIRAM/Dynamics-lab.git
cd Dynamics-lab

# Open directly in any web browser
open index.html
```

---

## Project Structure

```text
Dynamics-lab/
├── index.html          # Main application (served on GitHub Pages)
├── dynamics-lab.html   # Standalone codefile copy
├── logo.png            # Official monochrome brand asset
├── favicon.png         # Browser favicon icon
└── README.md           # Technical documentation & architecture diagrams
```

---

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.
