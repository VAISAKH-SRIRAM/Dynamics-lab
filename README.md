<div align="center">
  <br>
  <img src="logo.png" alt="Dynamics Lab Logo" width="160">
  <br><br>
  <h1>Dynamics Lab</h1>
  <p><strong>Nonlinear Dynamics, Chaos & Continuum PDE Engine</strong></p>
  <p><em>Zero-dependency, standalone browser laboratory for real-time ODE integration, 113,400-variable Navier-Stokes fluid continuum, DDE delays, hybrid event resets, 3D attractors, and DO-178C flight code generation.</em></p>
  <br>

  [![License: MIT](https://img.shields.io/badge/License-MIT-18181b.svg?style=flat-square)](LICENSE)
  [![Dependencies: None](https://img.shields.io/badge/Dependencies-0-18181b.svg?style=flat-square)](#)
  [![Engine: Vanilla JS](https://img.shields.io/badge/Engine-Vanilla%20JS%20%2F%20Canvas2D-18181b.svg?style=flat-square)](#)
  [![Platform: Web & Mobile](https://img.shields.io/badge/Platform-Desktop%20%7C%20Mobile-18181b.svg?style=flat-square)](#)
  [![Benchmarks: Verified](https://img.shields.io/badge/Benchmarks-Dynamics%20Lab%20vs%20MATLAB-18181b.svg?style=flat-square)](benchmarks/BENCHMARKS.md)

  <br><br>

  <a href="https://vaisakh-sriram.github.io/Dynamics-lab/">
    <img src="https://img.shields.io/badge/LAUNCH%20INTERACTIVE%20SIMULATOR-18181b?style=for-the-badge&logoColor=white" alt="Launch Interactive Simulator">
  </a>
  <br><br>
</div>

---

## Overview

**Dynamics Lab** is an interactive numerical laboratory for simulating ordinary differential equations (ODEs), delay differential equations (DDEs), hybrid event-driven systems, chaotic attractors, and **100,000-variable Navier-Stokes fluid continuum PDEs** in real time.

Engineered entirely in pure vanilla JavaScript and HTML5 Canvas2D, it operates as a **single, self-contained HTML file with zero dependencies, zero npm packages, and zero build pipelines**. Every model equation, parameter state, and view configuration is encoded directly into the URL hash permalink, allowing instantaneous sharing and offline execution.

---

## Features Beyond Standard Desktop Numerical Tools (MATLAB / Simulink / ANSYS)

| Capability | Dynamics Lab (In-Browser) | Typical MATLAB / Simulink Setup |
|---|---|---|
| **Zero Install & Distribution** | **Single standalone `.html` file** (runs offline on desktop & mobile) | 20+ GB install, proprietary license ($2,000+), account required |
| **100K+ Variable Spatial Continuum** | **113,400 Continuum State Variables (LBM D2Q9)** Navier-Stokes fluid at 60 FPS | Requires heavy CFD mesh solvers (ANSYS Fluent / OpenFOAM) |
| **von Kármán Vortex Shedding** | Real-time vortex wake generation behind **Cylinder & NACA Airfoils** | Takes minutes to calculate and render offline in MATLAB |
| **DO-178C Aerospace Code Generator** | **1-Click Flight C Code (`.c`)** with DAL-A traceability & MISRA-C:2012 | Requires $15,000+ Simulink DO-178C Tool Qualification Kit |
| **Delay Differential Equations (DDEs)** | Continuous history ring buffer with **`delay(var, tau)`** support | Requires specialized `dde23` / `ddensd` script setups |
| **Hybrid Events & State Resets** | Native in-loop **`when condition => action`** state mutation | Requires `odeset('Events', ...)` with manual loop restarts |
| **Boundary Value Problems (BVPs)** | **Interactive 10th Tab (`BVP SHOOTING`)** with Newton slope convergence | Requires `bvp4c` / `bvp5c` with manual mesh guess initialization |
| **Real-Time Chaos Sonification** | **Built-in Web Audio FM synthesizer** driven live by $(x,y,z)$ coordinates | Requires complex external DSP pipelines or non-realtime WAV writes |
| **Recurrence Plots (RQA)** | **Interactive 8th Tab** with live $N \times N$ matrix & threshold slider | Requires 3rd-party toolboxes (e.g., CRP Tool) |
| **1D Poincaré Return Map** | **Sub-step quadratic peak detection** + cobweb iteration staircase | Requires custom peak finders and array shift scripts |
| **Stereoscopic 3D Anaglyph** | **Real-time Red-Cyan 3D projection** for standard 3D glasses | Requires custom OpenGL shader pipelines |
| **Stiff & Symplectic Engines** | **Implicit Midpoint (A-stable)**, RK4, RK45 (`ode45`), Verlet | Requires switching between multiple toolbox routines |
| **Hamiltonian Conservation HUD** | **Live $\Delta E / E_0$ drift comparison** (Verlet vs RK4) | Manual analytical derivations and manual plotting |
| **Fractal Dimension** | **Kaplan-Yorke dimension $D_{KY}$** & phase divergence $\nabla \cdot \mathbf{f}$ | Requires offline phase space post-processing |
| **Universal Exporters** | Standalone MATLAB (`.m`), Python (`.py`), **LaTeX Paper (`.tex`)**, and **Aerospace Flight C (`.c`)** | Manual script writing and LaTeX document preparation |

---

## Core Capabilities

### 1. 100,000-Variable Continuum PDE Fluid Wind Tunnel (Lattice Boltzmann D2Q9)
* **Continuum Navier-Stokes at 60 FPS:** Discretizes spatial fluid flow onto a $180 \times 70$ lattice with 9 discrete microscopic velocity vectors ($\mathbf{c}_0 \dots \mathbf{c}_8$). Total coupled continuum state space:
  $$180 \times 70 \times 9 = \mathbf{113,400 \text{ State Variables}}$$
* **Kármán Vortex Shedding & Aerodynamics:** Computes local fluid vorticity ($\omega = \nabla \times \mathbf{u}$) and velocity magnitude across solid boundary geometries:
  * **Circular Cylinder ($Re \approx 160$):** Demonstrates periodic boundary layer separation and alternating vortex street shedding.
  * **NACA Cambered Airfoil Profile:** Demonstrates aerodynamic lift pressure differentials and turbulent trailing-edge wakes.
  * **Flat Plate Normal to Flow:** Demonstrates blunt-body bluff recirculation eddies.

### 2. Multi-Solver Integration Suite
* **RK4:** Classical 4th-order Runge-Kutta integrator with deterministic fixed step-size.
* **RK45 Dormand-Prince (`ode45`):** 7-stage Butcher tableau adaptive step-size integrator matching MATLAB's standard numerical engine.
* **Symplectic Verlet:** Time-reversible, energy-preserving leapfrog scheme for Hamiltonian and orbital mechanics.
* **Implicit Midpoint (Stiff Solver):** Unconditionally A-stable, symplectic implicit scheme with Newton-Raphson nonlinear algebraic solve and numerical Jacobian updates at every sub-step (handles stiff chemical kinetics without numerical explosion).
* **Symplectic Energy Drift Monitor:** Real-time percentage conservation readout ($\Delta E / E_0$) comparing Symplectic Verlet vs RK4.

### 3. Delay Differential Equations (DDEs) Engine
* **Continuous History Ring Buffer:** Evaluates lag terms via `delay(var, tau)` with sub-step linear/Hermite interpolation.
* **Infinite Memory Window:** Accurately models incubation latencies, physiological feedback loops, and laser cavity delays (e.g. the canonical Mackey-Glass attractor).

### 4. Hybrid Automata & Discrete Event Resets
* **In-Loop Event Interception:** Declared via simple syntax `when <condition> => <assignments>` (e.g., `when y <= 0 and v < 0 => y = 0, v = -0.85*v`).
* **Instantaneous State Mutation:** Accurately models physical impact oscillators (chaotic bouncing balls), relay switches, and biological integrate-and-fire spiking neurons.

### 5. Real-Time Chaos Sonification (Web Audio FM Synthesis)
* **Microtonal Frequency Mapping:** The state coordinate $x(t)$ modulates carrier frequency in real time ($140\text{ Hz} - 660\text{ Hz}$).
* **Chaotic Timbral Modulation:** Derivative velocity $\|d\mathbf{y}/dt\|$ controls frequency modulation index ($I_{\text{FM}}$), producing metallic harmonic bursts during chaotic transits.
* **Dynamic Resonant Filtering:** Coordinate $z(t)$ drives a 2nd-order resonant lowpass filter cutoff ($350\text{ Hz} - 4200\text{ Hz}$).
* **Stereo Spatialization:** Trajectory position pans dynamically across the stereo field.

### 6. Chaos Diagnostics, Lyapunov Spectrum & Fractal Dimension
* **Maximal Lyapunov Exponent ($\lambda$):** Continuous measurement of trajectory divergence under infinitesimal perturbation ($d_0 = 10^{-8}$) with Benettin reorthonormalization.
* **Phase Space Divergence ($\nabla \cdot \mathbf{f}$):** Continuous calculation of the Jacobian trace $\text{Tr}(J)$, quantifying the volume contraction rate of the flow.
* **Kaplan-Yorke Fractal Dimension ($D_{KY}$):** Computes the exact fractional dimension of chaotic strange attractors (e.g. $D_{KY} \approx 2.062$ for the Lorenz attractor).
* **Regime Classification:** Automatically categorizes dynamics into **Stable Equilibrium**, **Limit Cycle / Torus**, or **Deterministic Chaos ($\lambda > 0$)**.

### 7. Automated Equilibrium & Stability Analysis
* **Newton-Raphson Root Finding:** Multi-start search discovering fixed points across phase space ($F(x^*) = 0$).
* **Exact Analytical Eigenvalues:** Quadratic discriminant classification for 2D systems, plus **Cardano / Viète cubic solver** for 3D systems.
* **Hyperbolic Point Classification:** Differentiates Saddle Points, Stable Nodes, Spiral Sinks, and Saddle-Foci.

### 8. 11 Scientific Analysis Workspaces
1. **2D Phase Portrait:** Direction quiver vector fields, analytical nullclines, click-to-seed trajectories, Monte Carlo particle swarms, and **dynamic fluid dye streamlines**.
2. **3D Attractor:** 3-axis spherical orbital rotation, two-finger pinch-to-zoom, velocity-gradient coloring, scrubbable playback, and **Red-Cyan Stereoscopic 3D Anaglyph**.
3. **Time Series:** Multi-variable synchronous trajectory plotting with scrubbable playback.
4. **Sensitivity:** Real-time demonstration of the butterfly effect with twin perturbed trajectories ($10^{-5}$).
5. **Bifurcation Diagrams:** Automated parameter sweeps detecting period-doubling cascades and transitions to chaos.
6. **Poincaré Cross-Sections:** Hyperplane piercing detection with sub-step linear interpolation.
7. **Poincaré Return Map ($z_{n+1}$ vs $z_n$):** 1D local peak tent map with cobweb stepping lines and diagonal $y = x$ fixed-point reference.
8. **Recurrence Plot (RQA):** Full $N \times N$ recurrence matrix visualization ($R_{i,j} = \Theta(\varepsilon - \|\mathbf{y}_i - \mathbf{y}_j\|)$), adjustable threshold $\varepsilon$, and Recurrence Rate ($RR$).
9. **BVP Shooting:** Two-point boundary value solver ($y(x_a) = y_a, y(x_b) = y_b$) displaying iterative Newton-Raphson shooting trajectories converging onto exact boundary pins.
10. **100K PDE Fluid Wind Tunnel:** 113,400-variable 2D Lattice Boltzmann (D2Q9) Navier-Stokes fluid dynamics engine simulating aerodynamic wake vortices at 60 FPS.
11. **FFT Power Spectrum:** In-place Radix-2 Cooley-Tukey Fast Fourier Transform for identifying discrete harmonic frequencies vs. chaotic broadband noise.

### 9. Interoperability & Code Generation
* **Aerospace Flight C Code (`.c` --- DO-178C DAL-A & MISRA-C:2012):** Generates standalone, zero-allocation C99 code with formal requirement traceability (`REQ-HLR-01`), finite-math anomaly latches, and an automated MC/DC self-test suite for NASA F' (F-Prime) and avionics MCUs.
* **Academic LaTeX Paper (`.tex`):** Generates a complete publication-ready article draft with mathematical formulations, parameter tables, equilibrium eigenvalues, and citations.
* **MATLAB / GNU Octave:** Generates complete, runnable standalone `.m` scripts utilizing `ode45`.
* **Python / SciPy:** Exports ready-to-run `.py` scripts utilizing `scipy.integrate.solve_ivp` and `matplotlib`.
* **Raw CSV & Snapshots:** Instant export to CSV tabular time-series and high-resolution PNG captures.

---

## 21 Pre-Loaded Dynamic Systems

| Model | Dimensions | Category | Solver | Description |
|---|---|---|---|---|
| **Lorenz System (1963)** | 3D | Chaotic Attractor | RK4 / RK45 | Canonical atmospheric convection butterfly attractor |
| **Mackey–Glass Attractor** | 1D (DDE) | Delay Differential | RK4 (Delay) | Physiological chaos in white blood cell production ($\tau = 17$) |
| **Chaotic Bouncing Ball** | 2D (Hybrid) | Event-Driven | RK4 (Event) | Holmes impact oscillator with floor collision reset |
| **Spiking LIF Neuron** | 1D (Hybrid) | Event-Driven | RK4 (Event) | Lapicque biological neuron with membrane potential spike reset |
| **Rössler Attractor (1976)** | 3D | Chaotic Attractor | RK4 / RK45 | Minimal chemical reaction model with folded chaotic band |
| **Chua's Circuit (1983)** | 3D | Electronic Chaos | RK4 / RK45 | Non-linear electronics circuit exhibiting double-scroll chaos |
| **Kepler Gravitational Orbit** | 4D | Hamiltonian | Symplectic Verlet | Celestial two-body planetary motion demonstrating energy conservation |
| **Robertson Chemical Reaction** | 3D | Stiff Kinetics | Implicit Midpoint | Classic stiff benchmark (A-stable integration required) |
| **Hénon–Heiles System (1964)** | 4D | Hamiltonian | Symplectic Verlet | Stellar galactic orbits with non-integrable chaotic transitions |
| **Shimizu-Morioka Attractor** | 3D | Laser Chaos | RK4 / RK45 | Laser dynamics and subharmonic Lorenz-family bifurcations |
| **Sprott Minimal Chaos (B)** | 3D | Chaotic Attractor | RK4 | Minimal 5-term quadratic chaotic flow with single nonlinearity |
| **Van der Pol Oscillator (1920)** | 2D | Limit Cycle | RK4 / Implicit | Non-conservative triode oscillator with nonlinear damping |
| **Forced Duffing Oscillator** | 2D (Forced) | Chaos | RK4 / RK45 | Periodically forced oscillator with double-well potential |
| **Lotka–Volterra (1925)** | 2D | Conservative | Symplectic Verlet | Nonlinear ecological predator-prey dynamics |
| **Aizawa Attractor (1995)** | 3D | Chaotic Attractor | RK4 / RK45 | Rotating spherical core attractor with axial jet outflow |
| **Chen Attractor (1999)** | 3D | Chaotic Attractor | RK4 / RK45 | Dual-vortex attractor with complex topological structure |
| **Halvorsen Attractor** | 3D | Chaotic Attractor | RK4 / RK45 | Cyclic permutation system with 3-fold lobe symmetry |
| **Thomas' Cyclic Attractor** | 3D | Chaotic Attractor | RK4 / RK45 | Dissipative labyrinth chaotic flow with 3-fold symmetry |
| **Hindmarsh–Rose (1984)** | 3D | Bursting Neuron | RK4 / RK45 | Neuronal membrane potential bursting and spike train model |
| **FitzHugh–Nagumo** | 2D | Excitable | RK4 | Simplified Hodgkin-Huxley neuronal action potential model |
| **SIR Epidemic Model** | 3D | Dissipative | RK4 | Kermack-McKendrick infectious disease transmission model |

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
├── dynamics-lab.html   # Standalone single-file distribution copy
├── logo.png            # Official monochrome brand asset
├── favicon.png         # Browser favicon icon
├── benchmarks/         # Scientific benchmark test suite & telemetry
│   ├── benchmark_suite.js  # Reproducible test runner
│   ├── results.json        # Machine-readable benchmark telemetry
│   └── BENCHMARKS.md       # Official comparison whitepaper vs. MATLAB
└── README.md           # Project documentation
```

---

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.
