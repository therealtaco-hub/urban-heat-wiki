---
title: "Wiki Index"
updated: 2026-08-18
total_sources: 25
total_pages: 49
---

# Urban Heat Mapping — Wiki Index

Master catalog of all wiki pages. Read this before answering any query.

---

## Overview

- [[wiki/overview]] — Evolving synthesis, project goals, open questions, source counts (25 sources)

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
- [[wiki/sources/dwa-a138-lfu-regenwasser-bayern]] — LfU Bayern / Florian Ettinger: DWA-A138 Regenwasserbewirtschaftung Bayern; vollständige Abflussbeiwert-Tabelle (Primärquelle); kf-Werte; Versickerungsanlagentypen **[KEY: ABFLUSSBEIWERTE]**
- [[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]] — Moser-Reischl et al. 2021 (Arboricult. & Urban For. 47(4)): CPA/DBH allometry for 4 species in 6 South German cities **incl. Würzburg directly** (n=75–89/species); park > street crown size **[KEY: KRONENFLÄCHE WÜRZBURG]**
- [[wiki/sources/pretzsch-2015-urban-tree-crown-allometry]] — Pretzsch et al. 2015 (UFUG 14(3)):  Crown allometry for 22 species worldwide (39,057 trees); Tilia/Platanus/Aesculus/Robinia = Allometric Type 1 (largest crowns); cr25 values **[KEY: ALLOMETRIE-KLASSIFIKATION]**
- [[wiki/sources/gray-2021-canopy-cover-prediction]] — Gray et al. 2021 (Forest Ecol. Mgmt.): Empirical validation of Beer-Lambert/Crookston & Stage crown overlap model; OCF_e=0.015; RMSE ~12–14% cover
- [[wiki/sources/birkmann-2021-ludwigsburg-vulnerability-scenarios]] — Birkmann et al. 2021 (Climatic Change, ZURES project): ward-level future vulnerability scenarios (age + welfare-receipt) for Ludwigsburg, closest German mid-sized-city analog **[KEY: HVI CASE-STUDY-CITY]**
- [[wiki/sources/niu-2021-hvi-systematic-review]] — Niu et al. 2021 (Curr. Clim. Change Rep.): systematic review of 13 validated HVI studies; PCA dominant but unstable; weak health-outcome validation **[KEY: HVI METHODOLOGY]**
- [[wiki/sources/chen-2018-yrd-heat-health-risk]] — Chen et al. 2018 (Int. J. Health Geogr.): 250m-grid composite heat-health-risk index, Yangtze River Delta; PCA vulnerability, multiplicative Crichton's Risk Triangle
- [[wiki/sources/aubrecht-oezceylan-2013-ncr-heat-risk]] — Aubrecht & Özceylan 2013 (Environment International): census-block HSRI, Washington D.C. metro; equal-weighted additive HVI **[KEY: CLOSEST HVI METHODOLOGICAL PRECEDENT]**
- [[wiki/sources/bandaranayake-2026-lahti-digital-twin]] — Bandaranayake et al. 2026 (DESRIST): ML-based digital twin, Lahti Finland; LST-only, no vulnerability; user-trust gap despite R²=0.96
- [[wiki/sources/aydt-2026-duct-singapore]] — Aydt et al. 2026 (City & Environment Interactions): DUCT — WRF+PALM-4U coupled digital twin, Singapore; up to 6,144 core-hours/run, no vulnerability dimension
- [[wiki/sources/chen-2026-umep-target]] — Chen et al. 2026 (Environ. Modelling & Software): UMEP-TARGET QGIS plugin, Zurich; lightweight energy-balance model, <1hr desktop runtime, no vulnerability
- [[wiki/sources/smith-2009-manchester-gis-dss]] — Smith et al. 2009 (ICUC7): early GIS DSS forerunner, Greater Manchester; pre-calculated, no live simulation
- [[wiki/sources/cavan-2014-grabs-star-tools]] — Cavan et al. 2014 (Handbook of Climate Change Adaptation): GRaBS Assessment Tool + STAR Tools, 10 EU cities **[KEY: CLOSEST PRIOR TOOL — heat & runoff as separate modules]**

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
- [[wiki/concepts/tree-species-selection]] — Drought tolerance vs. cooling tradeoff; LB3/LB6 transpiration; allometric type classification; Würzburg species CPA table (3 sources)
- [[wiki/concepts/entsiegelung]] — Surface unsealing; ΔTemp = −0,03°C/%; Abflussbeiwert-Tabelle; Mehrfachnutzen; Vollentsiegelung vs. Teilentsiegelung (3 sources)
- [[wiki/concepts/heat-vulnerability-index]] — HVI construction methodology: PCA vs. fixed weighting, additive vs. multiplicative, spatial units, validation limits (4 sources)
- [[wiki/concepts/interactive-climate-tools]] — Landscape of prior climate-adaptation DSS/digital-twin tools; accessibility-vs-completeness trade-off; no prior tool integrates vulnerability (5 sources)

---

## Entities

### Cities
- [[wiki/entities/wuerzburg]] — **Target city**; University of Würzburg researchers; heat problem; project goals
- [[wiki/entities/muenchen]] — Case study; high impervious cover; ~2,000 trees/year net loss; García de León study location
- [[wiki/entities/nuernberg]] — Co-cited with Munich as Germany's most sealed cities
- [[wiki/entities/ludwigsburg]] — Closest German mid-sized-city HVI comparator (~93k inhabitants, Stuttgart region); Birkmann et al. 2021 / ZURES project
- [[wiki/entities/manchester]] — Origin city of the closest prior interactive tool (GRaBS Assessment Tool + STAR Tools); Smith 2009 + Cavan 2014

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
