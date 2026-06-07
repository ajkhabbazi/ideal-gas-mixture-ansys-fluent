# Ideal Gas Mixture UDF for Ansys Fluent

[![Language](https://img.shields.io/badge/language-C-blue)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Fluent UDF](https://img.shields.io/badge/Ansys-Fluent%20UDF-orange)](https://www.ansys.com/products/fluids/ansys-fluent)
[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.ijhydene.2023.11.038-blue)](https://doi.org/10.1016/j.ijhydene.2023.11.038)

---

## Overview

A compiled C UDF that plugs into Ansys Fluent's `RGAS_Functions` interface to provide full thermodynamic and transport property evaluation for ideal gas mixtures. Developed and used in CFD simulations of hydrogen injection into natural gas distribution pipelines.

---

## What it provides

The UDF supplies Fluent with custom mixture property routines at every cell and time step:

| Property | Function |
|----------|----------|
| Density | ideal gas law |
| Specific heat *C*ₚ | 4th-order polynomial in *T* |
| Enthalpy, Entropy | integrated from *C*ₚ polynomial |
| Speed of sound | derived from *C*ₚ and *R*ₘᵢₓ |
| Viscosity | Stiel–Thodos correlation |
| Thermal conductivity | Eucken relation |
| ∂ρ/∂*T*\|ₚ, ∂ρ/∂*p*\|_T, ∂*h*/∂*T*\|ₚ, ∂*h*/∂*p*\|_T | analytical derivatives |

All quantities are in SI units. The mixture averages are mass-fraction weighted.

---

## Getting started

**Requirements:** Ansys Fluent with compiled UDF support (any recent version).

1. Open your Fluent case.
2. Go to **User-Defined → Functions → Compiled UDFs** and add `ideal_gas_mixture_v2.c`.
3. Build and load the library.
4. Under **Materials**, select the loaded UDF as the real-gas equation of state for your mixture.

**Species configuration** is set in `MIXTURE_Setup` via the `gas[]` array and the property functions `Mw()`, `Cp_Parameters()`, `Tcrit()`, `Pcrit()`, `Vcrit()`. The default configuration is H₂/CH₄. To add or swap species, update `n_specs` and the corresponding property arrays.

---

## Citation

This UDF was developed for the ideal gas simulation cases in:

> Khabbazi, A.J., Zabihi, M., Li, R., Hill, M., Chou, V., & Quinn, J. (2024).
> **Mixing hydrogen into natural gas distribution pipeline system through Tee junctions.**
> *International Journal of Hydrogen Energy*, 49, 1332–1344.
> https://doi.org/10.1016/j.ijhydene.2023.11.038

The paper numerically investigates hydrogen injection into natural gas distribution pipelines via Tee junctions, using both ideal and Soave–Redlich–Kwong (SRK) real gas models. It quantifies mixing homogeneity length across distribution-pressure and intermediate-pressure operating conditions, examining the effects of side pipe diameter, injection direction, and momentum ratio on mixing quality.

```bibtex
@article{khabbazi2024h2,
  title   = {Mixing hydrogen into natural gas distribution pipeline system through {Tee} junctions},
  author  = {Khabbazi, Arash J. and Zabihi, Mojtaba and Li, Ri and Hill, Matthew and Chou, Vincent and Quinn, John},
  journal = {International Journal of Hydrogen Energy},
  volume  = {49},
  pages   = {1332--1344},
  year    = {2024},
  doi     = {10.1016/j.ijhydene.2023.11.038}
}
```

---

## Legal notice

The base framework (`RGAS_Functions` interface) originates from proprietary ANSYS, Inc. source code (© 1988–1998). This fork extends it for academic and demonstrative use only, without distributing or linking against any Fluent binary. Do not use, copy, or disclose beyond the terms of the original license agreement.

---

## Contact

For questions about the UDF or its implementation, please reach out to:

**Arash J. Khabbazi** — School of Mechanical Engineering, Purdue University
[arashjkh@gmail.com](mailto:arashjkh@gmail.com)
