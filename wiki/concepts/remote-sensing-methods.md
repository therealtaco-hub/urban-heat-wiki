---
title: "Remote Sensing Methods for Urban Heat Mapping"
type: concept
tags: [remote-sensing, landsat, modis, thermal-infrared, image-segmentation, lidar]
sources: 3
updated: 2026-05-20
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
- Downscaling: fusing lower-resolution thermal with higher-resolution optical to improve spatial detail. *(Source: [[wiki/sources/garcia-de-leon-lst-trees-munich]])*

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
1. **LST**: Landsat 8/9 thermal bands, summer months, multi-year average. Optionally downscale with Sentinel-2 10m optical.
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
