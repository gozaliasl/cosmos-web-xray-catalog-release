# COSMOS-Web Galaxy Group X-ray Catalog — Public Release (v1.3)

Companion data release for **Gozaliasl et al., Paper I: "The COSMOS-Web Galaxy Group X-ray Catalog:
Construction, Pipeline, and Data Release"**.

This release contains the full group-level X-ray measurements and derived properties for **all**
groups in the two COSMOS-Web group catalogs (both X-ray detections and non-detections, the latter
given as 95% upper limits) — not a curated subset. It supersedes the earlier v1.2 release, which
reproduced only the compact Table 2 columns for individually detected groups.

**Scope note:** this release contains X-ray measurements only. It does **not** include any group
membership, BGG/BCG, dynamical-mass, or cross-group-multiplicity information; those are scoped to a
separate, future companion release and are not part of this catalog.

## Files

| File | N rows | N detected (SNR ≥ 2.0) | Description |
|---|---|---|---|
| `CW-All_xray_catalog_public_v1.3.fits/csv` | 1678 | 499 | All AMICO groups (Toni et al. 2025) |
| `CW-HCG_xray_catalog_public_v1.3.fits/csv` | 993 | 332 | All Hickson compact groups (Hasinger et al., in prep.) |

## Columns

### Group identifiers and provenance
(inherited unchanged from the parent catalogs, not newly derived here)

| Column | Description | Units |
|---|---|---|
| `Group_ID` | Group identifier. For CW-All, identical to the AMICO group ID of Toni et al. (2025). For CW-HCG, identical to the Hickson compact-group ID of Hasinger et al. (in prep.). | — |
| `RA`, `DEC` | Group centroid coordinates | deg |
| `Redshift` | Redshift (photometric or spectroscopic) used for the X-ray analysis | — |
| `Redshift_Tier` (CW-All only) | Redshift source/tier flag | — |
| `Redshift_Spec` (CW-All only) | Spectroscopic redshift, where available | — |
| `Redshift_Phot_ErrLo`, `Redshift_Phot_ErrHi` (CW-All only) | Asymmetric photo-z uncertainty | — |
| `Redshift_Err_Parent` (CW-HCG only) | Redshift uncertainty from the parent Hickson catalog | — |
| `N_Spec_Members` (CW-All only) | Number of spectroscopic members | — |
| `Richness_LambdaStar`, `Richness_Lambda_raw` (CW-All only) | AMICO richness ($\lambda_\star$, raw $\lambda$) | — |
| `Richness_ng` (CW-HCG only) | Hickson richness ($n_g$, number of member galaxies) | — |
| `Velocity_Dispersion_Parent_kms`, `Velocity_Dispersion_Err_Parent_kms` (CW-HCG only) | Velocity dispersion from the parent Hickson catalog | km/s |
| `AMICO_Amplitude`, `AMICO_SN`, `AMICO_SN_NoCluster`, `AMICO_Detection_Flag`, `AMICO_Mask_Fraction` (CW-All only) | AMICO group-finder provenance/quality quantities | — |

### X-ray measurements
| Column | Description | Units |
|---|---|---|
| `Net_Counts`, `Net_Error`, `Source_Counts`, `Source_Error`, `Background` | Aperture-photometry counts | counts |
| `SNR`, `Significance_Sigma`, `P_Value` | Detection significance | — |
| `Is_Detected` | True if SNR ≥ 2.0 | boolean |
| `Flux_erg_cm2_s`, `Flux_Error` | Observed-frame 0.5–2 keV flux (detections) | erg cm⁻² s⁻¹ |
| `Upper_Limit_Flux_erg_cm2_s`, `Upper_Limit_Flux_Error` | 95% upper-limit flux (non-detections) | erg cm⁻² s⁻¹ |
| `Luminosity_erg_s`, `Luminosity_Error` | Rest-frame, K-corrected 0.5–2 keV luminosity | erg s⁻¹ |
| `Upper_Limit_Luminosity`, `Upper_Limit_Luminosity_Error` | 95% upper-limit luminosity | erg s⁻¹ |
| `Luminosity_Distance_Mpc` | Luminosity distance at `Redshift` | Mpc |
| `Temperature_keV`, `Temperature_Error` | Spectral-model temperature | keV |
| `M200_Temp_Msun`, `M200_Temp_Error`, `Log10_M200_Temp`, `Log10_M200_Temp_Error` | Temperature-based $M_{200}$ | $M_\odot$ |
| `M500_Temp_Msun`, `M500_Temp_Error`, `Log10_M500_Temp`, `Log10_M500_Temp_Error` | Temperature-based $M_{500}$ | $M_\odot$ |
| `M200_Luminosity_Msun`, `M200_Luminosity_Error`, `Log10_M200_Luminosity`, `Log10_M200_Luminosity_Error` | Luminosity-based $M_{200}$ | $M_\odot$ |
| `M500_Luminosity_Msun`, `M500_Luminosity_Error`, `Log10_M500_Luminosity`, `Log10_M500_Luminosity_Error` | Luminosity-based $M_{500}$ | $M_\odot$ |
| `R200_Temp_kpc`, `R500_Temp_kpc`, `R200_Luminosity_kpc`, `R500_Luminosity_kpc`, `R200_kpc`, `R500_kpc` | Overdensity radii (temperature- and luminosity-based) | kpc |
| `Mass_Method_Temp`, `Mass_Method_Luminosity` | Scaling relation used for each mass estimate | — |
| `Aperture_Arcsec`, `Aperture_kpc`, `Aperture_Coverage_Fraction`, `Extent_Arcsec`, `Extent_Apply_Mode` | Source aperture geometry | arcsec / kpc |
| `Background_Inner_Arcsec`, `Background_Outer_Arcsec`, `Background_Inner_kpc`, `Background_Outer_kpc`, `Background_Valid_Pixels` | Background annulus geometry | arcsec / kpc |
| `RA_xray_peak`, `Dec_xray_peak` | X-ray surface-brightness peak position | deg |
| `Redshift_Bin_Index`, `*_Binned` columns | Redshift-binned re-measurement, used for the stacking/XLF analyses (Sects. 4–6 of the paper) | — |

### Quality and contamination flags
| Column | Description |
|---|---|
| `Background_Quality` | Reliability flag for the local background estimate |
| `Contamination_Severity` | Severity score for projected-source contamination |
| `Is_Projected_Contaminated` | True if flagged for likely contamination by a projected source |
| `Is_Suspected_False_Positive` | True if flagged as a suspected false-positive detection |
| `Is_Low_Upper_Limit` | True if a non-detection's upper limit falls below the first quartile of the detected-flux distribution (see Sect. 3 of the paper) |
| `Upper_Limit_to_Median_Flux` | Ratio used to compute `Is_Low_Upper_Limit` |
| `Catalog_Name` | `CW-All` or `CW-HCG` |

## Provenance

Built from `cosmos-web-xray-igm` pipeline output (`xray_pipeline_v1.1_production`,
`configs/config_refined_z_release.yaml`), release tag `xray_release_v1.3`, from the full-column
`outputs/release_v1.2` build. CW-HCG richness/provenance columns are merged in from the parent
Hickson catalog (Hasinger et al., in prep.). See `PROVENANCE.json` for file checksums.

## Citation

If you use this catalog, please cite Gozaliasl et al. (Paper I, in preparation).
