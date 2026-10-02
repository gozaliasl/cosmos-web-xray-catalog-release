# COSMOS-Web Galaxy Group X-ray Catalog — Public Release 

Companion data release for **Gozaliasl et al., Paper I: "The COSMOS-Web Galaxy Group X-ray Catalog: Data Release"**.

This release contains the individually X-ray-detected (SNR ≥ 2.0) groups from the two COSMOS-Web
group catalogs, with exactly the columns shown in Table A.1 (CW-HCG) and Table A.2 (CW-All) of the
paper. 

## Files

| File | N rows | Description |
|---|---|---|
| `CW-All_xray_catalog_public_v1.4.fits/csv` | 499 | Individually X-ray-detected AMICO groups |
| `CW-HCG_xray_catalog_public_v1.4.fits/csv` | 332 | Individually X-ray-detected Hickson compact groups |

## Columns

| Column | Description | Units |
|---|---|---|
| `ID` | Group identifier. For CW-All, identical to the AMICO group ID of Toni et al. (2025). For CW-HCG, identical to the Hickson compact-group ID of Hasinger et al. (in prep.). | — |
| `RA`, `Dec` | Group centroid coordinates | deg |
| `z` | Redshift (photometric or spectroscopic) used for the X-ray analysis | — |
| `SNR` | Aperture-photometry detection significance | — |
| `f_X_erg_cm2_s`, `f_X_Error` | Observed-frame 0.5–2 keV flux and 1σ error | erg cm⁻² s⁻¹ |
| `L_X_erg_s`, `L_X_Error` | Rest-frame, K-corrected 0.5–2 keV luminosity and 1σ error | erg s⁻¹ |
| `T_X_keV`, `T_X_Error` | Spectral-model temperature and 1σ error | keV |
| `log_M200_Msun`, `log_M200_Error` | Halo mass (log₁₀), from the weak-lensing calibrated Leroy et al. (2026, in prep.) $M_{200}$–$L_{\rm X}$ relation | log₁₀(M☉) |
| `R500_kpc`, `R200_kpc` | Overdensity radii, from the same Leroy et al. (2026) relation | kpc |
| `Flag_Contaminated` | True if flagged as likely contaminated by a projected source | boolean |
| `Flag_FalsePositive` | True if flagged as a suspected false-positive detection | boolean |
| `Catalog` | `CW-All` or `CW-HCG` | — |

## Scope

This release intentionally reproduces only the columns and (individually detected) sample shown in
Tables A.1/A.2 of the paper. It does **not** include: non-detections/upper limits, background
diagnostics, binned/stacking-analysis columns, the temperature-based mass alternative, or
membership/richness/provenance information. Those remain part of the full internal pipeline output
and are documented in the companion papers of this series as they are used.


## Citation

If you use this catalog, please cite Gozaliasl et al. (Paper I).
for further info contact ghassem.gozaliasl@aalto.fi
