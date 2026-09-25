# Aerodynamic CFD Analysis of NACA 23015 Airfoil

[![Institution](https://img.shields.io/badge/Institution-Sharif%20University%20of%20Technology-blue.svg)](https://en.sharif.edu/)
[![Department](https://img.shields.io/badge/Department-Mechanical%20Engineering-darkred.svg)](http://mech.sharif.ir/)
[![Course](https://img.shields.io/badge/Course-Fluid%20Mechanics%20II-green.svg)](#)
[![Format](https://img.shields.io/badge/Report-PDF-red.svg)](project_report.pdf)

## Overview
This repository contains the computational fluid dynamics (CFD) aerodynamic investigation and experimental validation of external incompressible flow over a NACA 23015 airfoil. Modeled in ANSYS Workbench 2019 R1 (Fluent) using a structured C-grid computational topology, the study examines spatial discretization convergence, aerodynamic polar validation against empirical wind tunnel data, boundary layer separation physics under adverse pressure gradients, and the comparative mechanics of laminar versus turbulent ($k\text{-}\omega\text{ SST}$) flow regimes across varying angles of attack ($\alpha = 6^\circ$ and $\alpha = 10^\circ$).

- **Author:** Ali Taheri 
- **Supervising Professor:** Dr. Kamran
- **Teaching Assistant:** Eng. Sajjad Fartash
- **Academic Year:** 2025–2026
- **Institution:** Department of Mechanical Engineering, Sharif University of Technology

---

## Scientific Background & Aerodynamic Theory
The NACA 23015 is a 5-digit cambered airfoil renowned in aeronautical engineering for generating high maximum lift coefficients with exceptionally low pitching moments ($C_{m,c/4}$):
1. **5-Digit Geometry Characterization:**
   - **2:** Design lift coefficient $C_{l,\text{design}} = 0.3$ ($2 \times 0.15$).
   - **30:** Position of maximum camber far forward along the chord ($x/c = 0.15$), creating strong leading-edge suction.
   - **15:** Maximum thickness-to-chord ratio of $15\%$ ($t/c = 0.15$), providing gentle stall characteristics and internal structural volume.
2. **Adverse Pressure Gradients & Separation Mechanics:** As fluid travels along the suction surface downstream of the suction peak, static pressure rises ($dp/dx > 0$). Viscous shear dissipates kinetic energy within the boundary layer; once wall shear stress vanishes ($\tau_w = \mu (\partial u/\partial y)_{y=0} = 0$), the flow detaches, precipitating aerodynamic stall.
3. **Turbulent Boundary Layer Resistance:** Unlike laminar layers which detach rapidly under adverse pressure gradients, turbulent boundary layers leverage turbulent kinetic energy ($k$) and Reynolds shear stresses ($-\rho \overline{u'v'}$) to transport high-speed momentum from the freestream into the near-wall region, suppressing premature detachment.

---

## Numerical Methodology & Model Specifications

- **Solver:** ANSYS Fluent 2019 R1 (Double precision, Pressure-based, Steady)
- **Pressure-Velocity Coupling:** SIMPLE algorithm
- **Spatial Discretization:** Second-Order Upwind scheme for momentum, turbulent kinetic energy ($k$), and specific dissipation rate ($\omega$); Standard scheme for pressure interpolation
- **Convergence Criteria:** Continuity and momentum scaled residuals $< 10^{-4}$ (residual plateau $< 10^{-6}$, verified asymptotic $C_l$ and $C_d$ monitors)
- **Computational Domain:** Structured C-grid topology domain; semi-circular inlet arc placed $10c$ upstream; rectangular wake domain extending $15c$ downstream of the trailing edge ($c = 1.0\text{ m}$)
- **Boundary Conditions:** Velocity Inlet at upstream arc ($u_\infty = 0.735\text{ m/s}$), Pressure Outlet at wake exit ($p_{\text{gauge}} = 0\text{ Pa}$), stationary No-Slip Wall on airfoil surface, zero-gradient farfield boundaries

### Test Cases & Simulation Matrix:
1. **Grid Independence Study ($\alpha = 6^\circ$):** Coarse ($7,800$ elements), Medium ($81,300$ elements), Fine ($199,500$ elements) under $k\text{-}\omega\text{ SST}$.
2. **Angle of Attack Variations:** Moderate incidence ($\alpha = 6^\circ$, linear lift regime) and elevated incidence ($\alpha = 10^\circ$, near-stall non-linear regime).
3. **Viscous Regime Comparison ($\alpha = 10^\circ$):** Pure Laminar vs. Two-Equation Turbulent ($k\text{-}\omega\text{ SST}$).

### Fluid Thermophysical Properties & Operating Parameters:
| Parameter | Value | Unit | Description |
| :--- | :---: | :---: | :--- |
| Working Fluid | Air | — | Incompressible continuum fluid |
| Density ($\rho$) | $1.225$ | $\text{kg/m}^3$ | Standard sea-level air density |
| Dynamic Viscosity ($\mu$) | $1.802 \times 10^{-5}$ | $\text{Pa}\cdot\text{s}$ | Atmospheric molecular dynamic viscosity |
| Airfoil Chord Length ($c$) | $1.000$ | $\text{m}$ | Discretized profile chord |
| Freestream Velocity ($u_\infty$) | $0.735$ | $\text{m/s}$ | Evaluated freestream inlet velocity |
| Reynolds Number ($\text{Re}_c$) | $\sim 5.0 \times 10^4$ | — | Chord-based Reynolds number ($\text{Re}_c = \rho u_\infty c / \mu$) |
| Outlet Static Gauge Pressure | $0.000$ | $\text{Pa}$ | Ambient atmospheric discharge |

---

## Key Findings

### 1. Spatial Grid Convergence Verification
Spatial discretization error was evaluated at $\alpha = 6^\circ$ across three systematically refined mesh levels:
| Mesh Level | Elements | Nodes | Lift Coeff. ($C_l$) | Drag Coeff. ($C_d$) | Relative Error $\Delta C_l$ |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Coarse** | $7,800$ | $7,956$ | $0.342$ | $0.026$ | $-44.8\%$ |
| **Medium** | $81,300$ | $81,892$ | $0.612$ | $0.028$ | **$-1.3\%$** |
| **Fine (Reference)** | $199,500$ | $200,398$ | $0.620$ | $0.029$ | Baseline |

- The coarse grid suffers severe spatial discretization error ($\Delta C_l = -44.8\%$), failing to resolve the leading-edge suction peak.
- Refining the grid $2.45\times$ from medium to fine produces only a **$1.3\%$** change in $C_l$ and $3.5\%$ in $C_d$, while doubling solution runtime. The **Medium Mesh ($81,300$ elements)** achieves asymptotic grid independence and provides the optimal balance of accuracy and computational cost.

### 2. Experimental Validation against Wind Tunnel Polars
CFD predictions at $\alpha = 6^\circ$ were compared against empirical wind tunnel polar data for the NACA 23015 airfoil (Abbott & von Doenhoff, *Theory of Wing Sections*):
| Aerodynamic Parameter | CFD ($k\text{-}\omega\text{ SST}$) | Experimental Benchmark | Discrepancy / Error |
| :--- | :---: | :---: | :---: |
| **Section Lift Coefficient ($C_l$)** | **$0.612$** | $\approx 0.700$ | **$12.5\%$** |
| **Section Drag Coefficient ($C_d$)** | **$0.028$** | $\approx 0.014$ | $\approx 50\%$ |

- Lift prediction shows close agreement with experimental data ($12.5\%$ error).
- Drag overprediction is physically attributed to the fully turbulent assumption of standard $k\text{-}\omega\text{ SST}$, which bypasses the natural laminar-to-turbulent transition zone and overestimates forward turbulent skin friction.

### 3. Turbulence Physics & Separation Collapse at $\alpha = 10^\circ$
Comparative investigation between laminar and turbulent regimes at $\alpha = 10^\circ$ highlighted critical boundary layer mechanisms:
- **Laminar Flow:** Lacks turbulent cross-stream momentum transport. Under the intense upper-surface adverse pressure gradient, the laminar boundary layer detaches prematurely near the forward chord, inducing catastrophic stall, complete loss of suction, and massive pressure drag.
- **Turbulent Flow ($k\text{-}\omega\text{ SST}$):** Reynolds shear stress diffusion continuously transports high-momentum fluid from the outer stream into the near-wall region, keeping the boundary layer attached across the majority of the chord and preserving aerodynamic lift.

### 4. Angle of Attack Dynamics & Pressure Suction Amplification
- **Suction Peak Drop:** Increasing angle of attack from $6^\circ$ to $10^\circ$ drops the leading-edge minimum pressure coefficient from **$C_{p,\text{min}} \approx -1.6$** to **$-2.55$**, markedly widening the enclosed $C_p$ loop area and increasing section lift.
- **Velocity Acceleration:** Peak local velocity near the suction crest reaches **$1.35\text{ m/s}$** ($1.84\times$ freestream speed).
- **Wake Growth & Shear Layer Dynamics:** At $\alpha = 10^\circ$, streamline divergence over the aft $25\%$ of the chord, combined with enhanced vorticity production and wake shear layer broadening, signals boundary layer thickening prior to full stall.

---

## References
1. **Abbott, I. H., & von Doenhoff, A. E.** (1959). *Theory of Wing Sections: Including a Summary of Airfoil Data*. Dover Publications, New York.
2. **Menter, F. R.** (1994). Two-equation eddy-viscosity turbulence models for engineering applications. *AIAA Journal*, 32(8), 1598–1605.
3. **Wilcox, D. C.** (2006). *Turbulence Modeling for CFD* (3rd ed.). DCW Industries, La Cañada, CA.
4. **White, F. M.** (2011). *Fluid Mechanics* (7th ed.). McGraw-Hill Education.
5. **ANSYS Inc.** (2019). *ANSYS Fluent Theory Guide, Release 19.3*. ANSYS Inc., Canonsburg, PA.
