---
title: "Source: Inference of Urban 3D Morphology from Satellite Imagery and GIS Datasets — Application to Urban Climate Characterization"
type: source
tags: [uhi, wrf, local-climate-zones, lcz, 3d-morphology, simulation, gis, tum, fraunhofer]
sources: 1
updated: 2026-05-20
---

# Source: Muhammad (2021) — Urban 3D Morphology and UHI Simulation (TUM Master Thesis)

- **Type:** Master's thesis (Geodesy and Geoinformation, TU München)
- **Author:** Fadel Muhammad
- **Institution:** TU München, Chair of Geoinformatics (Prof. Thomas H. Kolbe); in cooperation with Fraunhofer Institute for Building Physics (IBP)
- **Supervisors:** Dr. Tatjana Kutzner (TUM), Dr.-Ing. Julian Vogel (Fraunhofer IBP), Dr. Afshin Afshari (Fraunhofer IBP)
- **Year:** 2021
- **Raw file:** [[raw/w8i4jtqmorih7djipbl5tm8c6.MasterThesis_FadelMuhammad.pdf]]

## Summary

This thesis develops a pipeline for deriving urban 3D morphology data from satellite imagery and GIS datasets, and applies it to UHI simulation using the WRF (Weather Research and Forecasting) mesoscale model. The key bottleneck addressed is that WRF's default LULC datasets are too coarse for urban-scale simulation — Local Climate Zones (LCZ) provide finer spatial resolution for characterising urban morphology as WRF input.

The thesis demonstrates that LCZ maps derived from GIS data (using a CityGML-based approach) can serve as more accurate LULC input than WRF's default MODIS-based datasets, improving surface urban heat island intensity (SUHII) simulation. Methods include WUDAPT (World Urban Database and Access Portal Tools) for LCZ training areas, confusion matrix evaluation, and correlation analysis.

This is **directly relevant to the Würzburg simulation goal**: the LCZ + WRF approach provides a methodological template for building the "what if we plant X trees at location Y" simulation.

## Key Claims

1. WRF model requires LULC input; default datasets (MODIS) are too coarse for city-scale UHI simulation.
2. **Local Climate Zones (LCZ)** provide finer spatial resolution and better capture urban morphology for WRF input.
3. **GIS-based LCZ classification** using CityGML produces more accurate results than satellite-based WUDAPT in areas with good GIS data availability.
4. The pipeline: GIS data → 3D morphology → LCZ map → WRF input → SUHII simulation.
5. Both surface UHI intensity (SUHII, from remote sensing) and canopy-level UHI intensity (UHII, from weather stations) are computed.
6. Fraunhofer IBP collaboration brings building physics expertise to urban climate modelling.

## Data and Figures

> [!note] Synthesis — not yet sourced
> Quantitative simulation results (SUHII magnitudes, improvement over default LULC) not yet extracted from this summary. Deep read of results section (Chapter 4) recommended.

## Contradictions / Gaps

- Mesoscale model (WRF) may not resolve individual tree or block-level cooling — microclimate simulation tools (ENVI-met) may be needed for the Würzburg project's localised "plant X trees at location Y" queries.
- Study city not specified in the available abstract/intro — likely a German city but needs confirmation.

## Wiki Pages Updated

- [[wiki/sources/muhammad-2021-urban-morphology-uhi]] ← this page
- [[wiki/concepts/local-climate-zones]]
- [[wiki/concepts/urban-morphology]]
- [[wiki/concepts/urban-heat-island]]
- [[wiki/entities/tu-muenchen]]
