# DFT & Raman Spectra Calculations of $\text{ZnGeP}_2$ (ZGP)

This repository contains input and calculation files for first-principles modeling of the crystal lattice, phonon spectrum, and Raman activity of pristine zinc germanium phosphide single crystals ($\text{ZnGeP}_2$, ZGP).

---

## 1. Software Used

The calculations were performed using the **[Quantum ESPRESSO](https://www.quantum-espresso.org/)** package (`pw.x`, `ph.x`, and `dynmat.x` modules):
- **`pw.x` (Plane-Wave Self-Consistent Field)**: Solves the Kohn–Sham equations using pseudopotentials within a plane-wave basis set to determine the ground-state electronic density.
- **`ph.x` (PHonon)**: Implements Density Functional Perturbation Theory (DFPT) to calculate phonon frequencies at the $\Gamma$-point ($q = 0$), the dielectric tensor ($\epsilon_\infty$), Born effective charges ($Z^*$), and non-resonant Raman activities (`lraman = .true.`).
- **`dynmat.x`**: Performs post-processing of the dynamical matrix, applies the Acoustic Sum Rule (ASR), and computes Raman scattering polarization tensors and vibrational modes.

---

## 2. Physical Model and System Parameters

- **Material:** $\text{ZnGeP}_2$ (Chalcopyrite structure, space group $I\overline{4}2d$).
- **Exchange-Correlation Functional:** GGA-PBE (Perdew-Burke-Ernzerhof).
- **Plane-Wave Basis Set:**
  - Wavefunction kinetic energy cutoff: $E_{\text{cut}} = 80.0\text{ Ry}$ (`ecutwfc`)
  - Charge density kinetic energy cutoff: $E_{\text{cut,\rho}} = 320.0\text{ Ry}$ (`ecutrho`)
- **SCF Convergence Threshold:** $10^{-10}\text{ Ry}$ (`conv_thr`).
- **DFPT Convergence Threshold:** $10^{-14}$ (`tr2_ph`).

---

## 3. Repository Structure

```text
zgp-dft-calc/
├── README.md               # Detailed description of calculations, physics, and instructions
├── .gitignore              # Ignores service and heavy binary files
├── pw.in / pw.out          # Ground-state self-consistent field (SCF) calculation
├── ph.in / ph.out          # DFPT phonon and Raman activity calculation
├── dynmat.in / dynmat.out  # Mode calculation and ASR application (crystal symmetry)
├── dyn                     # Dynamical matrix file
├── dynmat.axsf             # Atomic displacement vectors for visualization (XCrySDen / VESTA)
├── dynmat.mold             # Vibrational modes in Molden / Jmol format
├── drho_e1, drho_e2, e3    # Electronic density response to an external electric field (DFPT)
└── pseudo/                 # Pseudopotentials for Zn, Ge, P (UPF format)
    ├── Zn.upf
    ├── Ge.upf
    └── P.upf
