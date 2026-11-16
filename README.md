<div align="center">
  <br>
  <img src="logo.png" alt="Dynamics Lab Logo" width="160">
  <br><br>
  <h1>Dynamics Lab</h1>
  <p><strong>Nonlinear Dynamics & Chaos Simulation Engine</strong></p>
  <p><em>Zero-dependency, standalone browser laboratory for real-time ODE integration, 3D attractors, chaos sonification, recurrence quantification, and bifurcation analysis.</em></p>
  <br>

  [![License: MIT](https://img.shields.io/badge/License-MIT-18181b.svg?style=flat-square)](LICENSE)
  [![Dependencies: None](https://img.shields.io/badge/Dependencies-0-18181b.svg?style=flat-square)](#)
  [![Engine: Vanilla JS](https://img.shields.io/badge/Engine-Vanilla%20JS%20%2F%20Canvas2D-18181b.svg?style=flat-square)](#)
  [![Platform: Web & Mobile](https://img.shields.io/badge/Platform-Desktop%20%7C%20Mobile-18181b.svg?style=flat-square)](#)

  <br><br>

  <a href="https://vaisakh-sriram.github.io/Dynamics-lab/">
    <img src="https://img.shields.io/badge/LAUNCH%20INTERACTIVE%20SIMULATOR-18181b?style=for-the-badge&logoColor=white" alt="Launch Interactive Simulator">
  </a>
  <br><br>
</div>

---

## Overview

**Dynamics Lab** is an interactive numerical laboratory for simulating ordinary differential equations (ODEs), nonlinear dynamics, and chaotic attractors in real time.

Engineered entirely in pure vanilla JavaScript and HTML5 Canvas2D, it operates as a **single, self-contained HTML file with zero dependencies, zero npm packages, and zero build pipelines**. Every model equation, parameter state, and view configuration is encoded directly into the URL hash permalink, allowing instantaneous sharing and offline execution.

---

## Features Beyond Standard Desktop Numerical Tools (MATLAB / Python)

| Capability | Dynamics Lab (In-Browser) | Typical MATLAB / Python Setup |
|---|---|---|
| **Distribution** | Single self-contained HTML file (0 npm, 0 install) | Gigabytes of runtime, toolboxes, environments |
| **Real-Time Chaos Sonification** | Built-in Web Audio FM synthesizer driven by $(x,y,z)$ coordinates | Requires complex DSP pipelines or audio toolboxes |
| **Recurrence Plots (RQA)** | Live recurrence matrix blitting with $RR$ metrics & $\varepsilon$ slider | Requires specialized 3rd-party packages (e.g., CRP Tool) |
| **1D Poincaré Return Map** | Automatic peak detection, cobweb iteration steps, $y=x$ fixed points | Requires custom peak finders and array shift indexing |
| **3D Stereoscopic Anaglyph** | Real-time dual-eye Red-Cyan 3D projection for 3D glasses | Requires custom OpenGL rendering passes |
| **Flow Streamlines** | Dynamic fluid tracer dye particles flowing through vector fields | Static quiver vector arrows |
| **Stiff & Symplectic Engines** | RK4, Adaptive RK45 (`ode45`), Symplectic Verlet, **Implicit Midpoint** | Requires selecting between multiple toolbox routines |
| **Hamiltonian Conservation HUD** | Live $\Delta E / E_0$ energy drift comparison (Verlet vs RK4) | Manual analytical derivation and manual plotting |
| **Fractal Dimension** | Kaplan-Yorke dimension $D_{KY}$ & phase divergence $\nabla \cdot \mathbf{f}$ | Requires offline phase space post-processing |
| **Fixed Point Stability** | Exact analytical Cardano / Viète $3\times3$ cubic eigenvalue roots | Often falls back to purely numeric approximations |
| **Code & Report Exporters** | Standalone MATLAB (`.m`), Python (`.py`), and **Academic LaTeX Paper (`.tex`)** | Manual script writing and LaTeX authoring |
| **Mobile Interactivity** | Multi-touch 3D orbit rotation, pinch-zoom, and phase seeding | Desktop keyboard/mouse only |

---

## Core Capabilities

### 1. Multi-Solver Integration Suite
* **RK4:** Classical 4th-order Runge-Kutta integrator with deterministic fixed step-size.
* **RK45 Dormand-Prince (`ode45`):** 7-stage Butcher tableau adaptive step-size integrator matching MATLAB's standard numerical engine.
* **Symplectic Verlet:** Time-reversible, energy-preserving leapfrog scheme for Hamiltonian and orbital mechanics.
* **Implicit Midpoint (Stiff Solver):** Unconditionally A-stable, symplectic implicit scheme with Newton-Raphson nonlinear algebraic solve and numerical Jacobian updates at every sub-step (handles stiff chemical kinetics without numerical explosion).
* **Symplectic Energy Drift Monitor:** Real-time percentage conservation readout ($\Delta E / E_0$) comparing Symplectic Verlet vs RK4.

### 2. Real-Time Chaos Sonification (Web Audio FM Synthesis)
* **Microtonal Frequency Mapping:** The state coordinate $x(t)$ modulates carrier frequency in real time ($140\text{ Hz} - 660\text{ Hz}$).
* **Chaotic Timbral Modulation:** Derivative velocity $\|d\mathbf{y}/dt\|$ controls frequency modulation index ($I_{\text{FM}}$), producing metallic harmonic bursts during chaotic transits.
* **Dynamic Resonant Filtering:** Coordinate $z(t)$ drives a 2nd-order resonant lowpass filter cutoff ($350\text{ Hz} - 4200\text{ Hz}$).
* **Stereo Spatialization:** Trajectory position pans dynamically across the stereo field.

### 3. Chaos Diagnostics, Lyapunov Spectrum & Fractal Dimension
* **Maximal Lyapunov Exponent ($\lambda$):** Continuous measurement of trajectory divergence under infinitesimal perturbation ($d_0 = 10^{-8}$) with Benettin reorthonormalization.
* **Phase Space Divergence ($\nabla \cdot \mathbf{f}$):** Continuous calculation of the Jacobian trace $\text{Tr}(J)$, quantifying the volume contraction rate of the flow.
* **Kaplan-Yorke Fractal Dimension ($D_{KY}$):** Computes the exact fractional dimension of chaotic strange attractors (e.g. $D_{KY} \approx 2.06$ for the Lorenz attractor).
* **Regime Classification:** Automatically categorizes dynamics into **Stable Equilibrium**, **Limit Cycle / Torus**, or **Deterministic Chaos ($\lambda > 0$)**.

### 4. Automated Equilibrium & Stability Analysis
* **Newton-Raphson Root Finding:** Multi-start search discovering fixed points across phase space ($F(x^*) = 0$).
* **Exact Analytical Eigenvalues:** Quadratic discriminant classification for 2D systems, plus **Cardano / Viète cubic solver** for 3D systems.
* **Hyperbolic Point Classification:** Differentiates Saddle Points, Stable Nodes, Spiral Sinks, and Saddle-Foci.

### 5. 9 Scientific Analysis Workspaces
1. **2D Phase Portrait:** Direction quiver vector fields, analytical nullclines, click-to-seed trajectories, Monte Carlo particle swarms, and **dynamic fluid dye streamlines**.
2. **3D Attractor:** 3-axis spherical orbital rotation, two-finger pinch-to-zoom, velocity-gradient coloring, scrubbable playback, and **Red-Cyan Stereoscopic 3D Anaglyph**.
3. **Time Series:** Multi-variable synchronous trajectory plotting with scrubbable playback.
4. **Sensitivity:** Real-time demonstration of the butterfly effect with twin perturbed trajectories ($10^{-5}$).
5. **Bifurcation Diagrams:** Automated parameter sweeps detecting period-doubling cascades and transitions to chaos.
6. **Poincaré Cross-Sections:** Hyperplane piercing detection with sub-step linear interpolation.
7. **Poincaré Return Map ($z_{n+1}$ vs $z_n$):** 1D local peak tent map with cobweb stepping lines and diagonal $y = x$ fixed-point reference.
8. **Recurrence Plot (RQA):** Full $N \times N$ recurrence matrix visualization ($R_{i,j} = \Theta(\varepsilon - \|\mathbf{y}_i - \mathbf{y}_j\|)$), adjustable threshold $\varepsilon$, and Recurrence Rate ($RR$).
9. **FFT Power Spectrum:** In-place Radix-2 Cooley-Tukey Fast Fourier Transform for identifying discrete harmonic frequencies vs. chaotic broadband noise.

### 6. Interoperability & Code Generation
* **MATLAB / GNU Octave:** Generates complete, runnable standalone `.m` scripts utilizing `ode45`.
* **Python / SciPy:** Exports ready-to-run `.py` scripts utilizing `scipy.integrate.solve_ivp` and `matplotlib`.
* **Academic LaTeX Paper (`.tex`):** Generates a complete publication-ready article draft with mathematical formulations, parameter tables, equilibrium eigenvalues, and citations.
* **Raw CSV & Snapshots:** Instant export to CSV tabular time-series and high-resolution PNG captures.

### 7. Mobile Responsive Interface
* Adaptive two-mode layout: switches between a full-screen simulation canvas (`100dvh`) and a dedicated controls drawer.
* Native multi-touch gestures: 1-finger 3D orbital drag, 2-finger pinch-to-zoom, and 2-finger pan.

---

## 18 Pre-Loaded Dynamic Systems

| Model | Dimensions | Regime | Solver Recommendation | Description |
|---|---|---|---|---|
| **Lorenz System (1963)** | 3D | Chaos | RK4 / RK45 | Canonical atmospheric convection butterfly attractor |
| **Rössler Attractor (1976)** | 3D | Chaos | RK4 / RK45 | Minimal chemical reaction model with folded chaotic band |
| **Chua's Circuit (1983)** | 3D | Chaos | RK4 / RK45 | Non-linear electronics circuit exhibiting double-scroll chaos |
| **Kepler Gravitational Orbit** | 4D | Conservative | Symplectic Verlet | Celestial two-body planetary motion demonstrating energy conservation |
| **Robertson Chemical Reaction** | 3D | Stiff Kinetics | Implicit Midpoint | Classic stiff benchmark (A-stable integration required) |
| **Hénon–Heiles System (1964)** | 4D | Hamiltonian | Symplectic Verlet | Stellar galactic orbits with non-integrable chaotic transitions |
| **Shimizu-Morioka Attractor** | 3D | Chaos | RK4 / RK45 | Laser dynamics and subharmonic Lorenz-family bifurcations |
| **Sprott Minimal Chaos (B)** | 3D | Chaos | RK4 | Minimal 5-term quadratic chaotic flow with single nonlinearity |
| **Van der Pol Oscillator (1920)** | 2D | Limit Cycle | RK4 / Implicit | Non-conservative triode oscillator with nonlinear damping |
| **Forced Duffing Oscillator** | 2D (Forced) | Chaos | RK4 / RK45 | Periodically forced oscillator with double-well potential |
| **Lotka–Volterra (1925)** | 2D | Conservative | Symplectic Verlet | Nonlinear ecological predator-prey dynamics |
| **Aizawa Attractor (1995)** | 3D | Chaos | RK4 / RK45 | Rotating spherical core attractor with axial jet outflow |
| **Chen Attractor (1999)** | 3D | Chaos | RK4 / RK45 | Dual-vortex attractor with complex topological structure |
| **Halvorsen Attractor** | 3D | Chaos | RK4 / RK45 | Cyclic permutation system with 3-fold lobe symmetry |
| **Thomas' Cyclic Attractor** | 3D | Chaos | RK4 / RK45 | Dissipative labyrinth chaotic flow with 3-fold symmetry |
| **Hindmarsh–Rose (1984)** | 3D | Bursting | RK4 / RK45 | Neuronal membrane potential bursting and spike train model |
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
└── README.md           # Project documentation
```

---

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.
