# COSMOS-Web Galaxy Group X-ray Catalog — Public Release 

Companion data release for **Gozaliasl et al., Paper I: "The COSMOS-Web Galaxy Group X-ray Catalog: Data Release"**.

This release contains the individually X-ray-detected (SNR ≥ 2.0) groups from the two COSMOS-Web
group catalogs, with the columns shown in Table A.1 (CW-HCG) and Table A.2 (CW-All) of the
paper plus the 300 kpc and R200 comparison columns. 

## Revision notice (2026-10-08) — please re-download

This revision **changes values** in the v1.4 files, because two problems in the earlier files were found and fixed:

1. `L_X`, `f_X`, `T_X`, `log_M200`, `R500`, `R200` in the earlier files were measured in the fixed 300 kpc aperture, not in the
   R500-scaled aperture described in the paper (a merge bug in the pipeline). They are now measured within R500; the 300 kpc luminosity is kept as `L_X_300kpc_*`.
2. The earlier CW-All masses used the Leauthaud et al. (2010) relation. All masses (both catalogs) now follow the Leroy et al. (2026)
   relation, $E(z)\,M_{200} = 10^{0.138}\times10^{14}\,M_\odot\,[L_{\rm X}/E(z)/10^{43}\,{\rm erg\,s^{-1}}]^{0.759}$ (0.133 dex scatter), applied to the R500-aperture luminosity.

Also new: `L_X` within R200 (`L_X_R200_*`), `SNR_R500`, `SNR_R200`. The detected sample (499 / 332 groups) is unchanged.

## How the apertures are defined

1. **Detection:** fixed 300 kpc aperture, SNR ≥ 2 (`SNR`). This defines the sample.
2. **R500 aperture:** R500 is derived once from the 300 kpc luminosity (Leroy et al. 2026), converted to an angle with each group's
   angular-diameter distance, and the counts are re-extracted there (`Aperture_kpc`; 300 kpc kept if within 10%; bounded to 5″–120″,
   binding for only 5 groups). Background annulus 2–3 R500. The measurement is re-centred on the X-ray peak only if the peak is within 0.3 R500 of the optical position.
3. **R200 aperture:** R200 from the same 300 kpc luminosity; counts, flux and L_X re-extracted within it (`Aperture_R200_kpc`, up to 300″).
   `L_X_R200` is **noisier and more affected by unrelated emission** than `L_X`; its median is ≈2× `L_X` (R500). Use `SNR_R200` to judge each value.
4. The reported `R500_kpc`, `R200_kpc` and `log_M200_Msun` are computed from `L_X` (R500), so they differ slightly from the aperture radii used.
   The aperture exceeds the reported R500 by >10% for 44% (CW-All) / 29% (CW-HCG) of the groups.

`T_X` is computed from the Kettula et al. (2015) L–T relation applied to the luminosity *before* the temperature-dependent ECF correction
(flux and luminosity are then rescaled by $(T/3\,{\rm keV})^{0.5}$), so inverting the L–T relation on the released `L_X` does not return `T_X` exactly.

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
| `SNR` | Detection significance in the fixed 300 kpc first-pass aperture (defines the detected sample) | — |
| `f_X_erg_cm2_s`, `f_X_Error` | Observed-frame 0.5–2 keV flux and 1σ error | erg cm⁻² s⁻¹ |
| `L_X_erg_s`, `L_X_Error` | Rest-frame, K-corrected 0.5–2 keV luminosity within the R500-based aperture, and 1σ error | erg s⁻¹ |
| `Aperture_kpc` | Radius of the aperture used for `f_X` and `L_X` (R500 from the first-pass luminosity via Leroy et al. 2026; 300 kpc if within 10%) | kpc |
| `L_X_300kpc_erg_s`, `L_X_300kpc_Error` | Luminosity in the fixed 300 kpc first-pass aperture (for comparison) and 1σ error | erg s⁻¹ |
| `SNR_R500` | Significance of the counts re-extracted within the R500-based aperture | — |
| `Aperture_R200_kpc` | Radius of the R200 aperture (R200 from the 300 kpc luminosity) | kpc |
| `f_X_R200_erg_cm2_s`, `f_X_R200_Error` | Observed-frame 0.5–2 keV flux within R200 and 1σ error | erg cm⁻² s⁻¹ |
| `L_X_R200_erg_s`, `L_X_R200_Error` | Rest-frame, K-corrected 0.5–2 keV luminosity within R200 and 1σ error (noisy; see above) | erg s⁻¹ |
| `SNR_R200` | Significance of the counts re-extracted within R200 | — |
| `T_X_keV`, `T_X_Error` | Spectral-model temperature and 1σ error | keV |
| `log_M200_Msun`, `log_M200_Error` | Halo mass (log₁₀), from the weak-lensing calibrated Leroy et al. (2026, in prep.) $M_{200}$–$L_{\rm X}$ relation | log₁₀(M☉) |
| `R500_kpc`, `R200_kpc` | Overdensity radii, from the same Leroy et al. (2026) relation | kpc |
| `Flag_Contaminated` | True if flagged as likely contaminated by a projected source | boolean |
| `Flag_FalsePositive` | True if flagged as a suspected false-positive detection | boolean |
| `Catalog` | `CW-All` or `CW-HCG` | — |

## Scope

This release intentionally reproduces only the (individually detected) sample and the columns shown in
Tables A.1/A.2 of the paper. It does **not** include: non-detections/upper limits, background
diagnostics, binned/stacking-analysis columns, the temperature-based mass alternative, or
membership/richness/provenance information. Those remain part of the full internal pipeline output
and are documented in the companion papers of this series as they are used.


## Citation

If you use this catalog, please cite Gozaliasl et al. (Paper I).
for further info contact ghassem.gozaliasl@aalto.fi
