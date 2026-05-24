---
title: "Urban Heat Mapping — Overview"
type: overview
tags: [overview, synthesis]
sources: 11
updated: 2026-05-20
---

# Urban Heat Mapping — Overview

*Last updated: 2026-05-21 | Sources ingested: 12 (1 article + 8 papers/theses + 3 Entsiegelung)*

---

## Current Synthesis

Urban Heat Islands arise where sealed surfaces replace vegetation, converting solar energy to sensible heat rather than using it for evapotranspiration. In Central European cities including Germany, remote sensing studies consistently show that urban trees exhibit **8–12 K lower land surface temperature** than adjacent urban fabric in summer *(Schwaab et al. 2021, 293 European cities)*, and that each 1% increase in tree canopy cover corresponds to approximately **−0.069°C mean LST** *(García de León et al., Munich)*. When tree canopy is lost, the inverse holds: peak LST rises by 1–6°C and the summer warm period extends by up to 15 days *(Elmes et al. 2017)*.

The project target — **Würzburg** — sits firmly in this Central European zone where tree cooling is most effective. The methodological template for the project already exists in the literature: the García de León et al. study applies precisely the same approach (downscaled LST + individual tree crown data + land use classification) to Munich, conducted by researchers at the University of Würzburg itself. Adapting this to Würzburg is the core analytical task. The practical barrier to LST data acquisition is now closed: a free public Google Earth Engine application (Onačillová et al. 2022) delivers **10 m LST** for any area of interest by fusing Landsat 8/9 thermal data with Sentinel-2 optical bands — no custom code required. Step-by-step instructions are in [[wiki/methodischer-plan-wuerzburg]] and [[wiki/sources/onacillova-2022-lst-downscaling]].

A second intervention pathway — **surface unsealing (Entsiegelung)** — is now quantified: each 1% reduction in sealed area reduces LST by −0,03°C *(Tervooren 2015, Potsdam, R²=0,75–0,80)*. This is ~2.3× weaker per percentage point than tree planting (−0,069°C/%), but unsealing delivers co-benefits that trees alone cannot: precipitation infiltration, groundwater recharge, and biodiversity. Practical surface options and their infiltration coefficients (Abflussbeiwert) are documented for the Bavaria context *(Leitfaden Bayreuth 2024)*. The Copernicus Imperviousness Layer provides free GIS data on Würzburg's current sealing state *(UBA 2021)*.

Three complicating factors are now in the literature base: (1) drought-tolerant tree species deliver ~11% less transpiration cooling than moisture-adapted species — a tradeoff for long-term planting strategy *(Stratopoulos-Le Chalony 2020)*; (2) the cooling threshold for NDVI is ~0.4 — areas below this show minimal response *(Li et al.)*; (3) LAI and transpiration are the two key measurable parameters linking green infrastructure to temperature reduction *(Stangl et al. 2019)*. For the simulation component, LCZ+WRF methodology provides a validated framework *(Muhammad 2021, TUM)*.

The equity angle (vulnerable populations) is not yet covered by any ingested source — this is an active gap.

---

## Key Open Questions

- What is the current LST distribution in Würzburg (by neighbourhood, by land use class)?
- Which parts of Würzburg have the highest LST and the lowest tree cover — the worst heat burden?
- Where do elderly (Rentner) and young children (Kleinkinder) live in Würzburg, and how does that overlap with heat burden? (Zensus data needed)
- What is the quantitative relationship between tree planting / surface unsealing and temperature reduction at specific Würzburg locations?
- What does the Bavarian Modernisierungsgesetz (2025) actually change for Würzburg's planning authority?
- What is the relative contribution of shade vs. evapotranspiration to total tree cooling in a Central European context?

---

## Strongest Evidence So Far

| Claim | Strength | Source |
|-------|---------|--------|
| Central European trees: 8–12 K cooler than urban fabric (summer) | Strong — 293 cities, Nature Comms | [[wiki/sources/schwaab-2021-trees-european-cities]] |
| Each 1% tree canopy → −0.069°C LST (Munich) | Strong — large polygon sample, R²=0.41–0.61 | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| Tree canopy loss → +1–6°C peak LST | Strong — natural experiment (Worcester MA) | [[wiki/sources/elmes-2017-tree-canopy-loss-lst]] |
| Munich net tree loss ~2,000/year | Medium — advocacy source (Bund Naturschutz) | [[wiki/sources/gegen-hitze-kuehlleistung-baum]] |
| 1% surface unsealing → −0.03°C LST (Potsdam) | Medium — single city, one day, R²=0.75–0.80 | [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |
| Drought-tolerant trees cool 11% less (transpiration) | Medium — single city nursery study | [[wiki/sources/klimabaeume-fuer-die-stadt]] |

---

## Active Debates

- **Drought vs. cooling tradeoff**: climate-resilient tree selection may reduce cooling effectiveness by ~11%. Needs longer-term survival data to resolve.
- **LST vs. air temperature**: all remote sensing studies measure LST, but health impacts relate to air temperature. The translation is imperfect.
- **NDVI vs. tree canopy cover** as the right metric: NDVI conflates grass and trees; individual tree crowns are more precise but require high-resolution data.
- **Bavarian deregulation**: whether Modernisierungsgesetz 2025 meaningfully erodes surface sealing protections is contested between researchers and government.

---

## Next Sources to Find

Priority:
1. **Würzburg-specific heat / climate data** — any existing heat mapping study for Würzburg
2. **Zensus 2022 methodology** — how to work with 100m grid demographic data for Germany
3. **Health impact literature** — heat-related mortality in German cities, elderly vulnerability
4. **ENVI-met or similar microclimate model** — for block-level "plant X trees at Y" simulation (WRF is mesoscale; need microscale tool)
5. **Rötzer's primary paper** on tree cooling quantification (40,000 kWh figure) — currently only cited in journalism

---

## Source Count by Topic

| Topic | Sources |
|-------|---------|
| LST–tree correlation / remote sensing | 4 |
| Green infrastructure / tree cooling | 5 |
| Impervious surface / Versiegelung | 2 |
| Entsiegelung / surface unsealing | 3 |
| Urban morphology / LCZ | 2 |
| Simulation (WRF, LCZ) | 1 |
| Policy (Bavaria) | 1 |
| Species selection / drought tradeoff | 1 |
| Health impacts | 0 |
| Equity / vulnerable populations | 0 |
| Würzburg-specific | 0 (indirect: Würzburg researchers studied Munich) |
