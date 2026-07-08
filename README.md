# COSMOS-Web Galaxy Group X-ray Catalog — Public Release (v1.2)

Companion data release for **Gozaliasl et al., Paper I: "The COSMOS-Web Galaxy Group X-ray Catalog:
Construction, Pipeline, and Data Release"**.

This release contains the individually X-ray-detected (SNR ≥ 2.0) groups from the two COSMOS-Web
group catalogs, with the same columns presented in Table 2 of the paper. It is a curated subset of
the full internal pipeline output — see "Scope" below.

## Files

| File | N rows | Description |
|---|---|---|
| `CW-All_xray_catalog_public_v1.2.fits/csv` | 496 | Individually X-ray-detected AMICO groups |
| `CW-HCG_xray_catalog_public_v1.2.fits/csv` | 304 | Individually X-ray-detected Hickson compact groups |

## Columns

| Column | Description | Units |
|---|---|---|
| `ID` | Group ID. For CW-All, identical to the AMICO group ID of Toni et al. (2025). For CW-HCG, identical to the Hickson compact-group ID of Hasinger et al. (in prep.). | — |
| `RA`, `Dec` | Group centroid coordinates | deg |
| `z` | Redshift (photometric or spectroscopic) | — |
| `SNR` | Aperture-photometry detection significance | — |
| `f_X_erg_cm2_s`, `f_X_Error` | Observed-frame 0.5–2 keV flux and 1σ error | erg cm⁻² s⁻¹ |
| `L_X_erg_s`, `L_X_Error` | Rest-frame, K-corrected 0.5–2 keV luminosity and 1σ error | erg s⁻¹ |
| `T_X_keV`, `T_X_Error` | Spectral-model temperature and 1σ error | keV |
| `log_M200_Msun`, `log_M200_Error` | Temperature-based halo mass (log₁₀) and 1σ error | log₁₀(M☉) |
| `R500_kpc` | Temperature-based overdensity radius | kpc |
| `Flag_Contaminated` | True if flagged as projection-contaminated | boolean |
| `Flag_FalsePositive` | True if flagged as a suspected false positive | boolean |

## Scope

This release intentionally reproduces only the columns and (individually detected) sample shown
in Table 2 of the paper. It does **not** include: non-detections/upper limits, background
diagnostics, binned/stacking-analysis columns, alternative (luminosity-based) mass estimates,
membership/BGG information, or AGN/radio classification flags. Those are part of the full internal
pipeline output and are documented in the companion papers of this series (Paper II onward) as they
are used.

## Provenance

Built from `cosmos-web-xray-igm` pipeline output (`xray_pipeline_v1.1_production`,
`configs/config_refined_z_release.yaml`), release tag `xray_release_v1.2`. CW-All rows are drawn
from the pipeline's science-ready detection table (496 rows, SNR ≥ 2.0); CW-HCG rows are the
individually detected subset (304 rows, SNR ≥ 2.0) of the full CW-HCG catalog. See
`PROVENANCE.json` for input catalogs and checksums of the parent (full-column) files.

## Citation

If you use this catalog, please cite Gozaliasl et al. (Paper I, in preparation).
