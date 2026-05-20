---
title: "Land Surface Temperature (LST)"
type: concept
tags: [lst, remote-sensing, landsat, thermal-infrared, core-concept]
sources: 5
updated: 2026-05-20
---

# Land Surface Temperature (LST)

The radiometric temperature of the land surface as measured by thermal infrared (TIR) sensors on satellites. The primary quantitative variable in remote sensing-based UHI research, and the dependent variable the Würzburg project aims to correlate with tree density.

## Key Facts

- LST ≠ air temperature. LST is a surface measurement; health-relevant temperature is air temperature at human height (~1.2m). The two are correlated but differ, especially over shaded surfaces.
- Standard satellite sources: **Landsat** (30m/100m resolution, ~16 day revisit), **MODIS** (1km, daily), **Sentinel-3** (1km, daily), **ECOSTRESS** (70m, irregular). For city-level analysis, Landsat is typically the best trade-off.
- **Retrieval algorithms**: mono-window algorithm (Qin et al.), split-window algorithm, single-channel algorithm — different bands and emissivity assumptions.
- In Munich: downscaled LST product used by García de León et al., giving sub-Landsat resolution via downscaling techniques. *(Source: [[wiki/sources/garcia-de-leon-lst-trees-munich]])*
- **Key relationship**: each 1% increase in tree canopy cover → −0.069°C mean LST (Munich, summer 2020). *(Source: [[wiki/sources/garcia-de-leon-lst-trees-munich]])*
- **Unsealing relationship**: each 1% reduction in sealed area → −0.03°C LST (Potsdam, R²=0.75–0.80). *(Source: [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]])*
- Central European cities: urban trees 8–12 K cooler than urban fabric in summer. *(Source: [[wiki/sources/schwaab-2021-trees-european-cities]])*

## Mechanisms / How It Works

LST is driven by the surface energy balance:
- Net radiation = sensible heat + latent heat + ground heat flux
- Surfaces with high latent heat flux (vegetation via ET) have lower LST
- Impervious surfaces convert most net radiation to sensible heat → high LST
- NDVI is a proxy for vegetation density and correlates negatively with LST
- NDBI correlates positively with LST (built-up surfaces)

## Evidence and Data

| Finding | Value | Source |
|---------|-------|--------|
| LST per 1% tree canopy (Munich, whole area) | −0.069°C | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| LST by land use (Munich): Mixed | ~39°C median | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| LST by land use (Munich): Recreational | ~34.5°C median | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| Trees vs. urban fabric (Central Europe, summer) | 8–12 K lower | [[wiki/sources/schwaab-2021-trees-european-cities]] |
| Trees vs. urban fabric (Southern Europe, summer) | 0–4 K lower | [[wiki/sources/schwaab-2021-trees-european-cities]] |
| UTC loss → peak LST increase | 1–6°C | [[wiki/sources/elmes-2017-tree-canopy-loss-lst]] |
| NDVI threshold for cooling effect | >0.4 | [[wiki/sources/li-et-al-urban-form-lst-xgboost]] |

## Debates and Uncertainties

- Downscaling methods improve spatial resolution but introduce uncertainty.
- Single-date analysis vs. time series: summer averages give a different picture than individual heat days.
- LST during extreme heat events may differ from summer averages in important ways.

## Related Concepts

- [[wiki/concepts/remote-sensing-methods]] — how LST is retrieved
- [[wiki/concepts/ndvi]] — key negative correlate
- [[wiki/concepts/impervious-surface]] — key positive correlate
- [[wiki/concepts/entsiegelung]] — unsealing as quantified LST reduction strategy
- [[wiki/concepts/evapotranspiration]] — the latent heat flux that reduces LST
- [[wiki/concepts/urban-heat-island]] — LST is the primary measurement of surface UHI

## Relevant Entities

- [[wiki/entities/wuerzburg]] — target city for LST analysis
- [[wiki/entities/muenchen]] — case study city
- [[wiki/entities/university-of-wuerzburg]] — produced Munich LST+tree study
- [[wiki/entities/dlr]] — partner institution for LST data products

## Sources

- [[wiki/sources/garcia-de-leon-lst-trees-munich]]
- [[wiki/sources/schwaab-2021-trees-european-cities]]
- [[wiki/sources/elmes-2017-tree-canopy-loss-lst]]
- [[wiki/sources/reta-roba-hawassa-vegetation-lst]]
- [[wiki/sources/li-et-al-urban-form-lst-xgboost]]
