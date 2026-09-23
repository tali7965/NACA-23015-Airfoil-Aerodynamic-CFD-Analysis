# Aerodynamic CFD Analysis of NACA 23015 Airfoil

Fluid Mechanics II Project (پروژه مکانیک سیالات ۲)  
**Author:** Ali Taheri (علی طاهری) — ID: `401170875`

---

## Overview

This repository contains the complete computational fluid dynamics (CFD) simulation and validation study for external flow over a **NACA 23015** airfoil. The simulation was modeled and solved using **ANSYS Workbench 2019 R1 (Fluent)**, investigating aerodynamic performance, boundary layer separation, and flow characteristics across varying angles of attack and flow regimes.

---

## Key Features & Simulation Setup

- **Airfoil Geometry:** NACA 23015 5-digit airfoil profile (chord length $c = 1000\text{ mm}$).
- **Computational Domain:** C-grid topology domain ensuring proper upstream inlet distance and downstream wake development.
- **Mesh Independence Study:**
  - **Coarse Mesh:** 7,800 elements | 7,956 nodes ($C_l \approx 0.342, C_d \approx 0.026$)
  - **Medium Mesh:** 81,300 elements | 81,892 nodes ($C_l \approx 0.612, C_d \approx 0.028$)
  - **Fine Mesh:** 199,500 elements | 200,398 nodes ($C_l \approx 0.620, C_d \approx 0.029$)
  - *Outcome:* Medium mesh confirms asymptotic grid convergence, balancing computational efficiency and numerical precision.
- **Physics & Turbulence Modeling:**
  - Viscous models: Laminar vs. **$k\text{-}\omega\text{ SST}$ (Shear Stress Transport)** two-equation turbulence model.
  - Incompressible flow using air properties ($\rho = 1.225\text{ kg/m}^3$, $\mu = 1.802 \times 10^{-5}\text{ kg/(m}\cdot\text{s)}$).
  - Double precision solver with parallel processing.
- **Angles of Attack (AoA):**
  - Evaluated at $\alpha = 6^\circ$ and $\alpha = 10^\circ$.
  - Post-processing outputs include:
    - Static and dynamic pressure contours
    - Velocity magnitude distributions
    - Vorticity fields and boundary-layer separation detection
    - Streamlines (velocity vectors colored by stream function)
    - Surface pressure coefficient distribution ($C_p$ vs. $x/c$)
- **Validation:**
  - Numerical results evaluated against empirical wind tunnel polar data for the NACA 23015 airfoil.

---

## Repository Structure

```text
├── NACA23015.wbpj                 # ANSYS Workbench master project file
├── NACA23015_files/               # ANSYS database, meshes, cases, and solutions
│   ├── dp0/
│   │   ├── FFF/                   # Baseline simulation system (mesh, cases, dat)
│   │   ├── FFF-1/                 # System 1 run (k-omega SST / AoA variations)
│   │   ├── FFF-2/                 # System 2 run
│   │   ├── FFF-3/                 # System 3 run
│   │   └── global/MECH/           # Mesh database files (.mshdb)
│   ├── session_files/             # Workbench journals (.wbjn)
│   └── progress_files/            # Solution monitors, reports, and generated plots
├── NACA23015.csv                  # Airfoil coordinate table (CSV format)
├── NACA23015.txt                  # Airfoil coordinates formatted for ANSYS DesignModeler
├── Fm2-project.pdf                # Full technical report (figures, tables, and analysis)
├── .gitignore                     # Git ignore rules for CAD/CFD and OS files
└── README.md                      # Project documentation
```

---

## Getting Started

### Prerequisites

- **ANSYS Workbench & Fluent:** Version `19.3 (2019 R1)` or newer.

### Opening the Project

1. Clone this repository:
   ```bash
   git clone <repo-url>
   cd Fm2-project
   ```
2. Launch ANSYS Workbench.
3. Open `NACA23015.wbpj` (ensure `NACA23015_files/` is kept in the same directory).
4. Review the Workbench project schematic containing the geometry, mesh, and Fluent systems (`FFF`, `FFF-1`, `FFF-2`, `FFF-3`).
5. Open **Solution** or **Results** in Fluent/CFD-Post to inspect the converged fields or re-run calculations.

---

## License & Attribution

Academic project developed for the Fluid Mechanics II course.
Feel free to use and reference the geometry coordinates, journals, and simulation setups for academic and research purposes.
