<div align="center">
  <img src="logo.png" width="90" height="90" alt="Dynamics Lab Logo">
  <h1>Dynamics Lab</h1>
  <p><b>Nonlinear Dynamics & Chaos Engine — Single-File, Zero-Dependency Browser Simulator</b></p>
  
  <p>
    <a href="https://<username>.github.io/dynamics-lab/"><strong>Live Interactive Demo »</strong></a>
  </p>
</div>
---
## Overview
**Dynamics Lab** is an interactive, browser-based numerical laboratory for simulating ordinary differential equations (ODEs), nonlinear dynamics, and chaotic attractors in real time.
Built with pure vanilla JavaScript and HTML5 Canvas, it runs as a **single, self-contained HTML file with zero dependencies, zero build steps, and zero external packages**. Every simulation state lives inside the URL hash, so sharing a link shares a runnable model.
## Features
- **Multi-Solver Architecture:**
  - **RK4:** Classical 4th-Order Runge-Kutta.
  - **RK45 Dormand-Prince:** Adaptive step-size integrator matching MATLAB's `ode45`.
  - **Symplectic Verlet:** Energy-preserving integrator for Hamiltonian oscillators.
- **Chaos Quantification:** Continuous computation of the Maximal Lyapunov Exponent ($\lambda$) using Benettin’s algorithm.
- **Automated Fixed-Point Analysis:** Multi-start Newton-Raphson finder with numerical Jacobian evaluation and exact analytical eigenvalue solving ($2\times2$ and $3\times3$) for node/saddle/spiral stability classification.
- **7 Analysis Views:**
  1. **Phase Portrait:** Vector quiver fields, analytical nullclines, click-to-seed initial conditions, and ensemble swarm spawning.
  2. **3D Attractor:** Orbital camera rotation, dual-finger pinch zoom, velocity-gradient coloring, and comet animation trails.
  3. **Time Series:** Multi-variable trajectory plots with synchronized scrubbing.
  4. **Sensitivity:** Twin trajectories diverging under initial condition perturbations ($10^{-5}$).
  5. **Bifurcation Diagrams:** Automated parameter sweeps detecting limit-cycle period doublings and routes to chaos.
  6. **Poincaré Cross-Sections:** Hyperplane piercing detection with linear interpolation.
  7. **FFT Power Spectrum:** In-place Radix-2 Cooley-Tukey Fast Fourier Transform to distinguish periodic limit cycles from broadband chaos.
- **Interoperability & Code Generation:** One-click export to standalone **MATLAB (`.m`)**, **Python/SciPy (`.py`)**, CSV raw data, and high-resolution PNG captures.
- **Mobile Responsive:** Adaptive touch layout with pinch-to-zoom and full-screen simulation viewports on all screen sizes.
## 14 Built-In Systems
Includes classic and contemporary chaotic models:
* Lorenz System (1963)
* Rössler Attractor (1976)
* Van der Pol Oscillator (1920)
* Duffing Forced Double-Well
* Lotka-Volterra Predator-Prey
* Chua's Physical Circuit (1983)
* Thomas' Cyclically Symmetric Attractor
* Halvorsen Symmetric Attractor
* Aizawa Spherical Attractor
* Chen Dual-Scroll Attractor (1999)
* Rikitake Geomagnetic Dynamo
* Sprott Minimal Quadratic Chaos
* Hindmarsh-Rose Bursting Neuron (1984)
* Forced Damped Chaotic Pendulum
## Quickstart
No Node.js, npm, bundlers, or servers required:
```bash
git clone https://github.com/<username>/dynamics-lab.git
cd dynamics-lab
# Open directly in any browser:
open dynamics-lab.html
```
## License
MIT License.
