---
title: "Source: Onačillová et al. 2022 — LST Downscaling L8+S2 in GEE"
type: source
tags: [remote-sensing, lst, landsat, sentinel-2, downscaling, gee, ndvi, ndbi, method]
sources: 1
updated: 2026-05-21
---

# Source: Combining Landsat 8 and Sentinel-2 in GEE to Derive 10m LST

- **Type:** peer-reviewed article
- **Author(s):** Onačillová, K.; Gallay, M.; Paluba, D.; Péliová, A.; Tokarcík, O.; Laubertová, D.
- **Date:** 2022-08-20
- **Journal:** Remote Sensing, 14, 4076. https://doi.org/10.3390/rs14164076
- **Raw file:** [[raw/remotesensing-14-04076-v2.pdf]]

## Summary

Standard Landsat thermal data has a native resolution of 100 m (resampled to 30 m by USGS). This is too coarse to resolve individual streets, parks, or building blocks in an urban context. This paper presents a method to sharpen Landsat 8/9 LST to **10 m** by fusing it with Sentinel-2 multispectral imagery (which has no thermal band but provides 10 m optical data).

The method builds a multiple linear regression from NDVI, NDBI, and NDWI spectral indices — all calculable from Landsat 8 at 30 m — to predict LST30m. The same regression coefficients are then applied to the equivalent indices derived from Sentinel-2 at 10 m to yield LST10m. A residual correction step (redistributing the prediction error from 30 m back into the 10 m grid) enforces energy conservation and improves accuracy.

The entire pipeline is implemented as a free, public **Google Earth Engine application** that any researcher can point at any area of interest (≤1000 km²) worldwide. The user selects a Landsat and Sentinel-2 scene (ideally acquired on the same day), defines an ROI, and the tool outputs the downscaled 10 m LST map. Coefficients are automatically fitted to the local area — the Košice-specific values in the paper are illustrative, not fixed.

The case study (Košice, Slovakia, Dfb continental climate, ~240,000 inhabitants) shows that the 10 m product correctly resolves individual building blocks, roads, parks, and river areas — features invisible at 30 m. Validation against in-situ surface temperature sensors shows the 10 m product marginally outperforms the original 30 m L8 data (RMSE 4.22 °C vs. 4.43 °C; bias −1.55 °C vs. −2.05 °C).

## Key Claims

1. Landsat 8/9 LST can be downscaled from 30 m to **10 m** using Sentinel-2 spectral indices (NDVI, NDBI, NDWI) via multiple linear regression — no airborne data needed.
2. The three-index model reaches R²=0.642 (p<0.0001) for LST prediction. NDVI is the strongest single predictor (bivariate R²=0.63, negative sign); NDBI (R²=0.503, positive) and NDWI (R²=0.564, negative) add incremental signal.
3. Regression formula for Košice (illustrative — GEE recalculates locally): `LST30m = 38.476 − 12.929×NDVI + 2.416×NDBI − 5.310×NDWI`
4. Reconstruction quality when aggregating LST10m back to 30 m: R²=0.829, Pearson r=0.91 vs. observed L8 LST.
5. Validation against in-situ kinetic temperature: RMSE 4.22 °C, bias −1.55 °C for LST10m (vs. 4.43 °C / −2.05 °C for original LSTobs). The 10 m product is slightly more accurate than the native 30 m product.
6. A free GEE application implements the full pipeline and works for any location worldwide (ROI ≤1000 km²). Supports L8 and L9. Requires <5% cloud cover.
7. Ideal input: L8/9 and S2 scenes from the **same acquisition day**. A time lag up to ~20 min (typical overlap window) is acceptable; temperature drift during this window was <0.56 °C in the case study.

## Data and Figures

| Metric | L8 30 m (original) | Downscaled 10 m |
|--------|-------------------|-----------------|
| RMSE vs. in-situ | 4.43 °C | 4.22 °C |
| Bias vs. in-situ | −2.05 °C | −1.55 °C |
| R² (reconstruction) | — | 0.829 |
| Pearson r (reconstruction) | — | 0.91 |

NDVI bivariate R² with LST: **0.630** (negative)
NDBI bivariate R² with LST: **0.503** (positive)
NDWI bivariate R² with LST: **0.564** (negative)
Combined three-index model R²: **0.642**

## Step-by-Step Downscaling Procedure

This is the manual procedure. For Würzburg, the GEE tool (below) automates steps 1–9.

**Prerequisites:**
- Landsat 8 or 9 Collection 2 Level-2 surface reflectance product (OLI bands) + Level-1 or Level-2 thermal product (TIRS Band 10)
- Sentinel-2 MSI Level-2A product acquired on the same day as the Landsat overpass
- Both scenes must have <5% cloud cover over the area of interest
- Tools: ArcGIS / QGIS / Python with rasterio, or Google Earth Engine

**Step 1 — Compute spectral indices from Landsat 8 at 30 m:**
- NDVI = (B5 − B4) / (B5 + B4)
- NDBI = (B6 − B5) / (B6 + B5)
- NDWI = (B3 − B5) / (B3 + B5)

**Step 2 — Retrieve LST from Landsat 8 TIRS at 30 m:**
- The TIRS Band 10 has native 100 m resolution; USGS resamples to 30 m in Collection 2 Level-2 products.
- If using Level-2 ST product: LST is already delivered as surface temperature in Kelvin (scale factor ×0.00341802 + 149.0). Convert to °C.
- If computing manually: invert the radiative transfer equation using atmospheric correction parameters from the NASA atmcorr web tool (http://atmcorr.gsfc.nasa.gov) and estimate surface emissivity from NDVI using the threshold method.

**Step 3 — Fit the regression model (30 m resolution):**
- Regress LST30m against NDVI30m, NDBI30m, NDWI30m using ordinary least squares:
  `LST30m = a0 + a1×NDVI + a2×NDBI + a3×NDWI`
- Save coefficients a0–a3.

**Step 4 — Compute spectral indices from Sentinel-2 at 10 m:**
- NDVI = (B8 − B4) / (B8 + B4)
- NDBI = (B11 − B8) / (B11 + B8) — note: B11 is 20 m native, resample to 10 m
- NDWI = (B3 − B8) / (B3 + B8)

**Step 5 — Predict LST at 10 m:**
- Apply the same coefficients from Step 3 to the 10 m S2 indices:
  `LST10m_pred = a0 + a1×NDVI10m + a2×NDBI10m + a3×NDWI10m`

**Step 6 — Residual correction (energy conservation):**
- Compute residuals at 30 m: `ΔLST30m = LSTobs − LST30m_pred`
- Resample ΔLST30m to 10 m (bilinear or bicubic interpolation)
- Add residuals back: `LST10m = LST10m_pred + ΔLST10m`
- This step ensures that aggregating LST10m back to 30 m reproduces the original L8 values.

**Step 7 — Export and validate:**
- Visual check: parks, roads, and building blocks should be clearly resolved as cool/warm features at 10 m.
- Quantitative check: aggregate LST10m to 30 m grid and compare to LSTobs — target R²>0.8.

## GEE Shortcut (Recommended for Würzburg)

The GEE application automates all seven steps above:

- **App URL:** https://danielp.users.earthengine.app/view/lst-downscaling
- **Source code:** https://github.com/palubad/LST-downscaling-to-10m-GEE
- Requires a free Google Earth Engine account.

**How to use for Würzburg:**
1. Open the app.
2. Use the Geometry Tools to draw a polygon over Würzburg as your ROI (recommended: ≤1000 km²; Würzburg city area ~87 km² — well within limit).
3. Set start/end date to your target summer period (e.g. 2022-06-01 to 2022-09-30).
4. Select Landsat collection (L8 or L9). Click "Generate Image Collections" to see available scene IDs.
5. Pick a scene with <5% cloud cover. Note the exact scene ID.
6. Find the matching S2 scene for the same date in the S2 list. Enter both IDs.
7. Click to generate. Output layers: `LST 10 m (with residuals)` (use this), `LST 10 m (no residuals)`, original `Landsat 8/9 LST`, and RGB images.
8. Export `LST 10 m (with residuals)` to Google Drive as a GeoTIFF.

## Contradictions / Gaps

- Validation was performed on a different date than the imagery (same atmospheric conditions, different summer day) due to cloud cover during the planned measurement campaign — introduces some uncertainty.
- RMSE of ~4 °C means individual pixel absolute temperatures are unreliable; the method is best used for **spatial pattern analysis** (relative hot/cold spots) rather than absolute temperature claims.
- The Košice regression coefficients (a0–a3) are city-specific. The GEE tool recalculates them for the user's ROI, which is the correct approach for Würzburg.
- Only tested for summer clear-sky conditions. Not applicable to winter or cloudy periods.

## Wiki Pages Updated

- [[wiki/concepts/remote-sensing-methods]] — added step-by-step downscaling subsection; updated Würzburg pipeline
- [[wiki/concepts/land-surface-temperature]] — noted 10 m achievability; added accuracy caveats
- [[wiki/concepts/ndvi]] — added bivariate R²=0.63 with LST data point
- [[wiki/methodischer-plan-wuerzburg]] — Phase 1.1 expanded with concrete GEE workflow
- [[wiki/overview]] — source count updated; GEE tool noted in synthesis
