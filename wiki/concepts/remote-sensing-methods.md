---
title: "Remote Sensing Methods for Urban Heat Mapping"
type: concept
tags: [remote-sensing, landsat, sentinel-2, modis, thermal-infrared, image-segmentation, lidar, gee, downscaling]
sources: 4
updated: 2026-05-21
---

# Remote Sensing Methods for Urban Heat Mapping

The suite of satellite and airborne sensing techniques used to map LST, vegetation, impervious surfaces, and tree canopy cover in urban areas. The methodological backbone of any quantitative urban heat mapping project.

## Key Data Sources

| Sensor | Resolution | Revisit | Primary Use |
|--------|-----------|---------|-------------|
| Landsat 8/9 OLI+TIRS | 30m (thermal 100m) | ~16 days | LST time series, NDVI, NDBI |
| Landsat 5 TM, 7 ETM+ | 30m | ~16 days | Historical LST (back to 1984) |
| MODIS | 1km | Daily | Continental-scale LST; coarse for city analysis |
| Sentinel-2 | 10m | ~5 days | High-res NDVI; no thermal band |
| ECOSTRESS (ISS) | 70m | Irregular | High-res LST, ET |
| WorldView-2 | 0.5m | Tasked | Very high-res tree canopy mapping |
| Airborne LiDAR | <1m | Survey | 3D tree structure, building heights |
| High-res aerial imagery | <0.5m | Survey | Individual tree crown segmentation |

## Key Techniques

**LST retrieval from Landsat thermal bands:**
- Mono-window algorithm (Qin et al.) — used in Hawassa study. *(Source: [[wiki/sources/reta-roba-hawassa-vegetation-lst]])*
- Split-window algorithm — multi-channel approach for atmospheric correction.
- Single-channel algorithm — simpler, for Landsat 8 Band 10.
- **Shortcut**: Landsat Collection 2 Level-2 ST product delivers LST already computed (scale: ×0.00341802 + 149.0 K → subtract 273.15 for °C). No manual retrieval needed.
- Downscaling: fusing lower-resolution thermal with higher-resolution optical to improve spatial detail. *(Source: [[wiki/sources/garcia-de-leon-lst-trees-munich]])*

**LST downscaling — 100 m/30 m → 10 m (Onačillová et al. 2022):**

The standard Landsat thermal band is 100 m native (USGS resamples to 30 m). Individual urban features (streets, parks, building blocks) require finer resolution. The Onačillová method fuses Landsat LST with Sentinel-2 10 m optical bands to produce a **10 m LST product** using a freely available GEE application — no custom code required for Würzburg.

*Full step-by-step procedure: [[wiki/sources/onacillova-2022-lst-downscaling]]*

**GEE app (recommended):** https://danielp.users.earthengine.app/view/lst-downscaling
- Requires free GEE account.
- Draw ROI over Würzburg (city is ~87 km², well within the 1000 km² limit).
- Select a cloud-free Landsat 8/9 scene + matching Sentinel-2 scene (same day, <5% cloud cover).
- App fits the regression locally, applies residual correction, and outputs `LST 10 m (with residuals)` → export as GeoTIFF to Drive.

**Manual procedure summary (7 steps):**
1. Compute NDVI, NDBI, NDWI from Landsat 8 OLI at 30 m.
2. Retrieve LST from Landsat 8 TIRS at 30 m (or use Level-2 ST product directly).
3. Fit OLS regression: `LST30m = a0 + a1×NDVI + a2×NDBI + a3×NDWI` (R²≈0.64).
4. Compute NDVI, NDBI, NDWI from Sentinel-2 at 10 m.
5. Apply coefficients from step 3 to S2 indices → `LST10m_pred`.
6. Compute residuals at 30 m, resample to 10 m, add back → `LST10m = LST10m_pred + ΔLST10m`.
7. Export and validate (aggregate back to 30 m, compare to original; target R²>0.8).

**Accuracy caveats:**
- RMSE ~4.2 °C against in-situ sensors — use for spatial pattern analysis, not absolute temperature claims.
- Requires same-day L8/9 and S2 imagery with <5% cloud cover; Central European summers have frequent cloud cover — may need to select specific clear-sky dates.
- Method is only valid for summer clear-sky conditions.

**Tree canopy mapping:**
- Individual tree crown segmentation from fused LiDAR + WorldView-2 at 0.5m (Elmes et al., Worcester). *(Source: [[wiki/sources/elmes-2017-tree-canopy-loss-lst]])*
- Image segmentation of high-res aerial imagery + surface models (García de León et al., Munich: >166,000 trees). *(Source: [[wiki/sources/garcia-de-leon-lst-trees-munich]])*
- NDVI thresholding from Landsat/Sentinel-2 — coarser but freely available.

**Vegetation indices:**
- **NDVI**: vegetation density, negative LST correlate → [[wiki/concepts/ndvi]]
- **NDBI**: built-up index, positive LST correlate (potentially stronger predictor than NDVI)
- **LAI (Leaf Area Index)**: leaf area per unit ground area — key driver of shade and ET *(Source: [[wiki/sources/stangl-2019-wirkungen-gruene-stadt]])*

**Time series analysis:**
- Seasonal Trend Analysis (STA) — separates magnitude and timing of temperature changes. *(Source: [[wiki/sources/elmes-2017-tree-canopy-loss-lst]])*
- Theil-Sen slopes for monotonic trend detection.
- Multi-temporal Landsat stacking for 30-year trajectories. *(Source: [[wiki/sources/reta-roba-hawassa-vegetation-lst]])*

## For the Würzburg Project

Recommended data pipeline:
1. **LST at 10 m**: Use the GEE downscaling app (Onačillová et al. 2022) — pick 1–3 clear-sky summer days per year, export LST10m GeoTIFFs. Average across years for robustness. See full guide: [[wiki/sources/onacillova-2022-lst-downscaling]].
2. **Tree cover**: if high-res aerial imagery available from city of Würzburg → individual crown segmentation. Otherwise NDVI from Sentinel-2.
3. **Land use**: ATKIS (used in Munich study) + OpenStreetMap + city GIS data.
4. **Demographic data**: Zensus 2022 (100m grid cells) for vulnerable population mapping.

## Related Concepts

- [[wiki/concepts/land-surface-temperature]] — the primary output
- [[wiki/concepts/ndvi]] — derived vegetation index
- [[wiki/concepts/local-climate-zones]] — classification framework

## Sources

- [[wiki/sources/garcia-de-leon-lst-trees-munich]]
- [[wiki/sources/elmes-2017-tree-canopy-loss-lst]]
- [[wiki/sources/reta-roba-hawassa-vegetation-lst]]
- [[wiki/sources/onacillova-2022-lst-downscaling]]
