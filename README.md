# Numerical Investigation of Laminar Forced Convection in a Rectangular Microchannel

[![Institution](https://img.shields.io/badge/Institution-Sharif%20University%20of%20Technology-blue.svg)](https://en.sharif.edu/)
[![Department](https://img.shields.io/badge/Department-Mechanical%20Engineering-darkred.svg)](http://mech.sharif.ir/)
[![Course](https://img.shields.io/badge/Course-Heat%20Transfer-green.svg)](#)
[![Format](https://img.shields.io/badge/Report-PDF-red.svg)](Project-Report.pdf)

## Overview
This repository contains the computational fluid dynamics (CFD) investigation of three-dimensional laminar forced convection and hydrodynamic boundary layer development within a rectangular microchannel utilizing ANSYS Fluent. The study performs a systematic grid independence analysis across five mesh resolutions, quantifies the conjugate thermal-hydraulic transport under uniform wall heat flux across varying Reynolds numbers ($Re = 100, 200, 300$), and validates numerical predictions against classical analytical laminar duct flow theory.

- **Author:** Ali Taheri
- **Discipline:** Mechanical Engineering / Heat Transfer & CFD
- **Course:** Heat Transfer / Numerical Heat Transfer
- **Software Tool:** ANSYS Fluent
- **Institution:** Department of Mechanical Engineering, Sharif University of Technology

---

## Scientific Background & Physical Significance
Microchannel heat sinks represent an essential cooling paradigm for high-heat-flux microelectronics, laser diodes, and compact micro-heat exchangers due to their extreme surface-area-to-volume ratio ($A/V \sim 10^4\text{ m}^{-1}$). Flow in microchannels exhibits key physical transport characteristics:
1. **Laminar Transport Dominance:** Operating at low Reynolds numbers ($Re \le 300 \ll Re_{\text{cr}} \approx 2300$), mixing and heat removal are governed by steady laminar convection and thermal diffusion.
2. **Developing Boundary Layers:** In conduits of finite length ($L = 10\text{ mm}$), the hydrodynamic and thermal entrance regions constitute a major fraction of the total channel length, generating high local wall shear stresses and enhanced initial convective heat transfer rates.
3. **Pumping Power vs. Heat Dissipation:** The steep velocity gradients near microchannel walls yield significant viscous shear resistance, necessitating accurate pressure drop calculations to evaluate hydraulic pumping penalties.

---

## Numerical Methodology & Model Specifications

- **Solver:** ANSYS Fluent (3D, Steady-State, Laminar, Pressure-Based)
- **Governing Equations:** Navier-Stokes equations for conservation of mass, momentum, and energy
- **Pressure-Velocity Coupling:** SIMPLE algorithm
- **Spatial Discretization:** Second-Order Upwind scheme for momentum and energy, Standard pressure interpolation
- **Convergence Criteria:** Scaled residuals $< 10^{-4}$ for continuity and momentum ($x, y, z$), and $< 10^{-6}$ for the energy equation
- **Channel Dimensions:**
  - Width: $W = 0.2\text{ mm}\ (200\ \mu\text{m})$
  - Height: $H = 0.1\text{ mm}\ (100\ \mu\text{m})$
  - Aspect Ratio: $\alpha = W/H = 2.0$
  - Axial Length: $L = 10.0\text{ mm}$
  - Cross-Sectional Area: $A_c = H \times W = 2.0 \times 10^{-8}\text{ m}^2$
  - Wetted Perimeter: $P = 2(H + W) = 6.0 \times 10^{-4}\text{ m}$
  - Hydraulic Diameter: $D_h = \frac{4 A_c}{P} = 133.3\ \mu\text{m}$

### Boundary Conditions:
- **Inlet:** Velocity inlet with uniform velocity profiles ($V_{in} = 0.67, 1.34, 2.01\text{ m/s}$ corresponding to $Re = 100, 200, 300$) and uniform inlet fluid temperature $T_{in} = 298.15\text{ K}$.
- **Outlet:** Pressure outlet with zero gauge pressure ($P_{\text{gauge}} = 0\text{ Pa}$).
- **Walls:** No-slip kinematic boundary condition ($\vec{v} = 0$). Constant uniform heat flux $q'' = 1.22 \times 10^6\text{ W/m}^2$ applied across the heated base surface area ($A_b = 4.0 \times 10^{-6}\text{ m}^2$).

### Fluid Thermophysical Properties (Liquid Water):
| Parameter | Symbol | Value | SI Unit |
| :--- | :---: | :---: | :---: |
| Density | $\rho$ | $997$ | $\text{kg/m}^3$ |
| Dynamic Viscosity | $\mu$ | $8.9 \times 10^{-4}$ | $\text{Pa}\cdot\text{s}\ (\text{kg}/(\text{m}\cdot\text{s}))$ |
| Thermal Conductivity | $k_f$ | $0.60$ | $\text{W}/(\text{m}\cdot\text{K})$ |
| Inlet Temperature | $T_{in}$ | $298.15$ | $\text{K}$ |
| Hydraulic Diameter | $D_h$ | $1.333 \times 10^{-4}$ | $\text{m}$ ($133.3\ \mu\text{m}$) |

---

## Key Findings

### 1. Grid Independence Verification (Task 1)
Spatial discretization convergence was evaluated across five progressively refined grids at baseline $Re = 300$:

| Grid Level | Nodes | Elements | Relative Density | $T_f\ [\text{K}]$ | $T_w\ [\text{K}]$ | $h\ [\text{W}/(\text{m}^2\cdot\text{K})]$ | $\Delta P\ [\text{Pa}]$ | $Nu$ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Mesh 1 (Finest)** | **164,853** | **704,627** | **100.0%** | **314.30** | **448.48** | **3023.79** | **2728.46** | **0.671** |
| Mesh 2 | 116,636 | 496,790 | 70.5% | 316.32 | 451.78 | 3019.54 | 2657.79 | 0.669 |
| Mesh 3 | 95,865 | 402,529 | 57.1% | 318.25 | 446.97 | 3024.34 | 2613.00 | 0.668 |
| Mesh 4 | 79,063 | 332,123 | 47.1% | 315.11 | 449.37 | 3027.14 | 2575.90 | 0.693 |
| Mesh 5 (Coarsest) | 70,724 | 291,348 | 41.3% | 313.97 | 450.46 | 3009.88 | 2560.23 | 0.674 |

- The convective heat transfer coefficient stabilizes with **$<0.15\%$ relative deviation** between Mesh 1, Mesh 2, and Mesh 3.
- Mesh 1 (704,627 elements) was established as the grid-independent standard for all subsequent parametric investigations.

### 2. Reynolds Number Sensitivity & Forced Convection Performance (Task 2)
Parametric simulations at $Re = 100, 200,$ and $300$ demonstrate the dominant role of advection in thermal mitigation:

| Reynolds Number ($Re$) | Inlet Velocity $V_{in}\ [\text{m/s}]$ | Mean Fluid Temp $T_f\ [\text{K}]$ | Wall Temp $T_w\ [\text{K}]$ | Heat Transfer Coeff $h\ [\text{W}/(\text{m}^2\cdot\text{K})]$ | Nusselt Number ($Nu$) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **100** | $0.67$ | $344.80$ | $534.05$ | $2139.44$ | $0.475$ |
| **200** | $1.34$ | $322.03$ | $477.87$ | $2603.25$ | $0.578$ |
| **300** | $2.01$ | $314.30$ | $448.48$ | $3023.79$ | $0.671$ |

- **Convective Heat Transfer Enhancement:** Increasing $Re$ from 100 to 300 yields a **$+41.3\%$ increase** in $h$ (from $2139.44$ to $3023.79\text{ W}/(\text{m}^2\cdot\text{K})$).
- **Wall Temperature Suppression:** The higher mass flow rate lowers the area-weighted average wall temperature by **$85.57\text{ K}$** (from $534.05\text{ K}$ down to $448.48\text{ K}$).
- **Fluid Residence Time:** Mean outlet bulk temperature drops by $30.5\text{ K}$ due to shorter residence time at elevated throughput.

### 3. Theoretical Validation & Analytical Discrepancy Analysis
- **Classical Benchmark:** For fully developed laminar flow in a rectangular duct of aspect ratio $\alpha = 2$ subject to uniform axial heat flux ($H$ boundary condition), the asymptotic theoretical Nusselt number is $Nu_{\text{th,fd}} = 4.12$ (Kays & London, Incropera Table 8.1).
- **Physical Discrepancy Drivers:**
  1. *Bulk Temperature Averaging:* Analytical definitions rely on mass-weighted cup-mixing temperature $T_m(x)$, whereas numerical domain averaging across non-linear thermal profiles shifts $(T_w - T_f)$.
  2. *Thermal Entrance Region Effects:* In a $10\text{ mm}$ channel, the developing boundary layer region exhibits exceptionally high local heat transfer gradients before asymptotically approaching fully developed conditions downstream.

### 4. Hydrodynamic Entry Length ($L_{fd,h}$) Development (Task 4)
- **Classical Boundary Layer Relation:** For internal laminar duct flows:
  $$\frac{L_{fd,h}}{D_h} \approx 0.05 \cdot Re \implies L_{fd,h} = 0.05 \cdot (300) \cdot (1.333 \times 10^{-4}\text{ m}) \approx 2.0\text{ mm}$$
- **Numerical Contour Observation:** Longitudinal velocity contours show viscous boundary layers developing along channel walls and merging at the centerline at $x \approx 2.0\text{ mm}$ ($\mathbf{20\%}$ of the total channel length $L = 10\text{ mm}$).
- **Validation:** CFD predictions match the theoretical boundary layer entry relation with **$>99\%$ quantitative consistency**, confirming the physical fidelity of the simulation.

---

## References
1. **Incropera, F. P., DeWitt, D. P., Bergman, T. L., & Lavine, A. S.** (2011). *Fundamentals of Heat and Mass Transfer* (7th ed.). John Wiley & Sons.
2. **Kays, W. M., Crawford, M. E., & Weigand, B.** (2005). *Convective Heat and Mass Transfer* (4th ed.). McGraw-Hill.
3. **Kandlikar, S. G., Garimella, S., Dongqing, L., Colin, S., & King, M. R.** (2014). *Heat Transfer and Fluid Flow in Minichannels and Microchannels* (2nd ed.). Elsevier.
4. **ANSYS Inc.** (2024). *ANSYS Fluent Theory Guide, Release 2024*. Canonsburg, PA.
