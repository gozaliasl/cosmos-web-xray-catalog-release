# xray_release_v1.2 — Catalog Release

Pipeline: xray_pipeline_v1.1_production (unchanged science code from v1.1)
Release tag: xray_release_v1.2
Release date: 2026-07-03
Cosmology: Planck18 (H0=67.4, Om0=0.315, Ode0=0.685)
Config: configs/config_refined_z_release.yaml
Membership release used for redshift input: membership_release_v1.0 (authoritative, frozen)

## What changed from v1.1

- **v1.1** = X-ray bug-fix release (Bugs #7, #2, #4, #6) using the group
  redshift from `membership_dztier` (an intermediate/diagnostic Project B
  output) or the raw/original catalog redshift where dztier refinement
  hadn't run -- this wiring was unintentional, found in a 2026-07-03 audit.
- **v1.2** = the exact same X-ray pipeline code and bug fixes, rerun with
  the group redshift input corrected to come from `membership_release_v1.0`
  (the frozen, authoritative Project B production release). No X-ray
  photometry, detection, spectral-fitting, or stacking code was modified.
- **v1.2 supersedes v1.1 for Papers I and II.**

## v1.1 -> v1.2 empirical impact (measured, not predicted)

| Catalog | N groups | Detection flips | Newly detected | Lost detection | Contamination flag flips | median &#124;Δz&#124; | max &#124;Δz&#124; |
|---|---|---|---|---|---|---|---|
| CW-All | 1678 | 5 | 4 | 1 | 43 | 0.0015 | 0.0700 |
| CW-HCG | 912 | 0 | 0 | 0 | 1 | 0.0005 | 0.0220 |

Median per-group changes in flux/L_X/temperature/M200/R200/R500 are ~0 for
the bulk of the sample, but non-negligible tails exist among detected
groups (see docs/RELEASE_NOTES.md and docs/Xray_Catalog_Release_Report.md
for the full per-quantity breakdown): ~3-4% of CW-All detected groups show
>10% flux/L_X shifts (aperture is defined in fixed physical kpc, so a
redshift change moves the angular aperture and resamples different pixels),
while R200/R500 are stable (0/495 changed by >10%).

## Catalogs in this release

| File | N rows | Description |
|---|---|---|
| CW-All_xray_catalog_v1.2.fits | 1678 | All COSMOS-Web groups with X-ray properties |
| CW-HCG_xray_catalog_v1.2.fits | 912 | All HCG groups with X-ray properties |
| XRAY_science_catalog_v1.2.fits | 496 | Science-ready X-ray detections |
| XRAY+SPECZ_catalog_v1.2.fits | 395 | X-ray detections with spec-z |
| STACKED_XRAY_catalog_v1.2.fits | 10 | Redshift-binned stacking results |

## Provenance

See PROVENANCE.json for: git commit hashes (both repos), config file, input
group catalog paths, membership release version, and SHA-256 checksums of
every FITS file in this release.

## v1.1 Bugfixes carried forward (unchanged)

- Bug #7: Duplicate YAML config block removed
- Bug #2: Leauthaud+2010 pivot points rescaled WMAP5->Planck18
- Bug #4: Temperature-dependent ECF correction implemented
- Bug #6: Background_Quality column added

See docs/VERSION_HISTORY.md and docs/RELEASE_VALIDATION_v1.1.md for v1.1
bugfix details, and docs/RELEASE_NOTES.md / docs/Xray_Catalog_Release_Report.md
for the full v1.1->v1.2 wiring-audit and rerun writeup.
