---
title: "Wiki Index"
updated: 2026-05-21
total_sources: 12
total_pages: 32
---

# Urban Heat Mapping — Wiki Index

Master catalog of all wiki pages. Read this before answering any query.

---

## Overview

- [[wiki/overview]] — Evolving synthesis, project goals, open questions, source counts (11 sources)

---

## Sources

- [[wiki/sources/gegen-hitze-kuehlleistung-baum]] — BR24 article (2024): TU München quantifies tree cooling at 40,000 kWh/year; Munich net tree loss ~2,000/year; Bavarian deregulation risk
- [[wiki/sources/garcia-de-leon-lst-trees-munich]] — García de León et al. (Würzburg/DLR/TUM): LST vs. tree canopy in Munich by land use class; −0.069°C per 1% tree cover **[KEY SOURCE]**
- [[wiki/sources/schwaab-2021-trees-european-cities]] — Schwaab et al. 2021 (ETH Zürich, Nature Comms): urban trees 8–12 K cooler than urban fabric in Central Europe across 293 cities **[KEY SOURCE]**
- [[wiki/sources/klimabaeume-fuer-die-stadt]] — Stratopoulos-Le Chalony (TUM, 2020 dissertation): drought-tolerant trees cool 11% less; drought vs. cooling tradeoff
- [[wiki/sources/elmes-2017-tree-canopy-loss-lst]] — Elmes et al. 2017 (Clark Univ.): UTC loss → +1–6°C LST, +15 day warm season (Worcester MA, Landsat time series)
- [[wiki/sources/reta-roba-hawassa-vegetation-lst]] — Reta-Roba & Worku-Tabor: LST vs. NDVI/NDBI in Hawassa Ethiopia; NDBI stronger LST predictor than NDVI
- [[wiki/sources/li-et-al-urban-form-lst-xgboost]] — Li et al. (Chinese cities, XGBoost-SHAP): NDVI must exceed 0.4 for cooling; LCZ and urban form thresholds
- [[wiki/sources/stangl-2019-wirkungen-gruene-stadt]] — Stangl et al. 2019 (Univ. Bodenkultur Wien): review of urban greening effects; LAI and transpiration as key parameters
- [[wiki/sources/muhammad-2021-urban-morphology-uhi]] — Muhammad 2021 (TUM master thesis): LCZ+WRF pipeline for UHI simulation; GIS-based 3D morphology
- [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] — Tervooren (2015, AGIT): ΔTempLST = −0,03°C × ΔVersiegelung%; R²=0,75–0,80; Potsdam/Cfb **[KEY: Entsiegelungskoeffizient]**
- [[wiki/sources/leitfaden-flaechenentsiegelung-2024]] — Leitfaden Flächenentsiegelung (Landkreis Bayreuth, 2024): Abflussbeiwert-Tabelle nach Belagstyp; 45% Germany sealed; Kosten
- [[wiki/sources/uba-texte141-2021-entsiegelung]] — Pannicke-Prochnow et al. (UBA Texte 141/2021): Entsiegelungspotenziale; Rechtslage; Copernicus Imperviousness Layer; doppelte Innenentwicklung
- [[wiki/sources/onacillova-2022-lst-downscaling]] — Onačillová et al. (2022, Remote Sensing): Landsat 8 LST → 10 m via Sentinel-2 + multiple linear regression; free GEE app; step-by-step guide for Würzburg **[KEY: LST-DATENERFASSUNG]**

---

## Concepts

- [[wiki/concepts/urban-heat-island]] — Core phenomenon: cities warmer than surroundings; 8–12 K differential in Central Europe (4 sources)
- [[wiki/concepts/land-surface-temperature]] — LST: primary measurement variable; retrieval methods; −0.069°C/% tree cover in Munich (5 sources)
- [[wiki/concepts/green-infrastructure]] — Trees, parks, green roofs: cooling evidence; 40,000 kWh/tree; −0.069°C/% regression; 8–12 K European benchmark (6 sources)
- [[wiki/concepts/impervious-surface]] — Versiegelung: sealed surfaces as UHI driver; Munich/Nuremberg ranking; Bavarian policy risk (2 sources)
- [[wiki/concepts/evapotranspiration]] — Plant transpiration cooling mechanism; key parameter alongside LAI (3 sources)
- [[wiki/concepts/ndvi]] — Vegetation index; negative LST correlate; cooling threshold at NDVI > 0.4 (2 sources)
- [[wiki/concepts/remote-sensing-methods]] — Landsat LST, Sentinel-2 downscaling to 10 m (GEE), tree crown segmentation, NDVI/NDBI; full data pipeline for Würzburg (4 sources)
- [[wiki/concepts/local-climate-zones]] — LCZ classification; WRF input; simulation framework (2 sources)
- [[wiki/concepts/urban-morphology]] — Building density, sky view factor, LCZ; morphology effects on LST (2 sources)
- [[wiki/concepts/tree-species-selection]] — Drought tolerance vs. cooling tradeoff; LB3 vs. LB6 species (1 source)
- [[wiki/concepts/entsiegelung]] — Surface unsealing; ΔTemp = −0,03°C/%; Abflussbeiwert-Tabelle; Mehrfachnutzen; Vollentsiegelung vs. Teilentsiegelung (3 sources)

---

## Entities

### Cities
- [[wiki/entities/wuerzburg]] — **Target city**; University of Würzburg researchers; heat problem; project goals
- [[wiki/entities/muenchen]] — Case study; high impervious cover; ~2,000 trees/year net loss; García de León study location
- [[wiki/entities/nuernberg]] — Co-cited with Munich as Germany's most sealed cities

### Researchers
- [[wiki/entities/thomas-roetzer]] — TU München; tree cooling quantification; co-author on Würzburg/Munich paper (3 sources)

### Institutions
- [[wiki/entities/university-of-wuerzburg]] — Institute of Geography; produced Munich LST+tree study; natural partner for Würzburg replication
- [[wiki/entities/dlr]] — German Aerospace Center; remote sensing data products; Taubenböck/Leichtle
- [[wiki/entities/tu-muenchen]] — TU München; Rötzer's lab; Stratopoulos dissertation; Muhammad thesis
- [[wiki/entities/eth-zurich]] — ETH Zürich; Schwaab et al. 2021 European cities study

---

## Other

- [[wiki/kuehleffekte-vergleich]] — Alle quantitativen Kühleffekte aus dem Wiki im Vergleich; Übertragbarkeit auf Würzburg (9 Quellen)
- [[wiki/methodischer-plan-wuerzburg]] — Strukturierter Arbeitsplan für das Würzburg-Projekt: 5 Phasen, Datenquellen, offene Methodenfragen (9 Quellen)
- [[wiki/simulation-logic.md]] — Berechnungslogik für /api/simulate/baeume + /api/simulate/wasser; Input/Output-Verträge; Annahmen (4 Quellen)
