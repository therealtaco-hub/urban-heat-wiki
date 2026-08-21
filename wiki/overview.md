---
title: "Urban Heat Mapping — Overview"
type: overview
tags: [overview, synthesis]
sources: 25
updated: 2026-08-18
---

# Urban Heat Mapping — Overview

*Last updated: 2026-08-18 | Sources ingested: 25 (1 article + 11 papers/theses + 4 Entsiegelung/Hydrologie + 4 Heat-Vulnerability-Index + 5 Interactive-Tools/DSS)*

---

## Current Synthesis

Urban Heat Islands arise where sealed surfaces replace vegetation, converting solar energy to sensible heat rather than using it for evapotranspiration. In Central European cities including Germany, remote sensing studies consistently show that urban trees exhibit **8–12 K lower land surface temperature** than adjacent urban fabric in summer *(Schwaab et al. 2021, 293 European cities)*, and that each 1% increase in tree canopy cover corresponds to approximately **−0.069°C mean LST** *(García de León et al., Munich)*. When tree canopy is lost, the inverse holds: peak LST rises by 1–6°C and the summer warm period extends by up to 15 days *(Elmes et al. 2017)*.

The project target — **Würzburg** — sits firmly in this Central European zone where tree cooling is most effective. The methodological template for the project already exists in the literature: the García de León et al. study applies precisely the same approach (downscaled LST + individual tree crown data + land use classification) to Munich, conducted by researchers at the University of Würzburg itself. Adapting this to Würzburg is the core analytical task. The practical barrier to LST data acquisition is now closed: a free public Google Earth Engine application (Onačillová et al. 2022) delivers **10 m LST** for any area of interest by fusing Landsat 8/9 thermal data with Sentinel-2 optical bands — no custom code required. Step-by-step instructions are in [[wiki/methodischer-plan-wuerzburg]] and [[wiki/sources/onacillova-2022-lst-downscaling]].

A key data gap for the tree simulation is now closed: Würzburg is a **direct study city** in Moser-Reischl et al. (2021, Arboricult. & Urban For.), which provides species-specific crown projection area (CPA) allometries measured from 75–89 trees per species in Würzburg itself (Tilia, Platanus, Robinia, Aesculus). The `kronenfläche_m2` for each of the 44,647 Baumkataster trees can now be computed directly from the existing `kronenbrei` field (`CPA = π × (kronenbrei/2)²`) or, when that is missing, from the allometric regression (`CPA = exp(a) × DBH^b`). The worldwide allometric reference (Pretzsch et al. 2015, 22 species, 39,057 trees) confirms all four Würzburg species belong to Allometric Type 1 — the largest-crowned class — and that the current simulation default of 50 m² per tree is conservative for mature trees (Platanus Würzburg mean: 124 m²) but generous for saplings. The Beer-Lambert crown overlap model used in `/api/simulate/baeume` (Crookston & Stage 1999) is empirically validated by Gray et al. (2021): it performs well at the low-to-moderate canopy densities typical of urban Würzburg, with a known underestimation bias at >90% cover that is unlikely to be reached in practice.

A second intervention pathway — **surface unsealing (Entsiegelung)** — is now quantified: each 1% reduction in sealed area reduces LST by −0,03°C *(Tervooren 2015, Potsdam, R²=0,75–0,80)*. This is ~2.3× weaker per percentage point than tree planting (−0,069°C/%), but unsealing delivers co-benefits that trees alone cannot: precipitation infiltration, groundwater recharge, and biodiversity. The infiltration coefficients (Abflussbeiwerte) for all relevant surface types are sourced directly from the authoritative Bavarian engineering standard: **DWA-A138 / LfU Bayern** *(Ettinger, LfU Referat 67)* — the same values that back the `/api/simulate/wasser` endpoint. Practical cost data and broader surface ranges are documented in *(Leitfaden Bayreuth 2024)*. The Copernicus Imperviousness Layer provides free GIS data on Würzburg's current sealing state *(UBA 2021)*.

Three complicating factors are now in the literature base: (1) drought-tolerant tree species deliver ~11% less transpiration cooling than moisture-adapted species — a tradeoff for long-term planting strategy *(Stratopoulos-Le Chalony 2020)*; (2) the cooling threshold for NDVI is ~0.4 — areas below this show minimal response *(Li et al.)*; (3) LAI and transpiration are the two key measurable parameters linking green infrastructure to temperature reduction *(Stangl et al. 2019)*. For the simulation component, LCZ+WRF methodology provides a validated framework *(Muhammad 2021, TUM)*.

**The equity gap is now closed.** Four sources ground the project's Heat Vulnerability Index (HVI) design. The closest direct methodological precedent is **Aubrecht & Özceylan 2013** (Washington D.C. metro, census-block level): a Heat Stress Risk Index combining a kriged heat-hazard grid with a six-indicator, **equal-weighted, additive** vulnerability index — explicitly choosing fixed weighting over PCA "to avoid additional subjectivity," the same philosophy behind this project's literature-derived 0.6/0.4 LST/elderly weighting. **Niu et al. 2021**'s systematic review of 13 validated HVI studies confirms PCA is the dominant construction method in the literature but flags it as hard to interpret and unstable across input sets — direct justification for preferring a transparent fixed-weight index — while also cautioning that HVI–health-outcome validation is consistently weak (R² as low as 0.03) across the reviewed studies, a limitation this project's own (as-yet-unvalidated) HVI shares. **Chen et al. 2018** (Yangtze River Delta, 250m grid) demonstrates the same grid-based hazard×vulnerability composite approach at fine spatial resolution, using a multiplicative Crichton's-Risk-Triangle combination rather than an additive one — a citable methodological contrast. **Birkmann et al. 2021** (Ludwigsburg, ~93k inhabitants, Stuttgart region) is the closest case-study-city analog to Würzburg's own size class: ward-level vulnerability scenarios combining age and welfare-receipt (a German income proxy, used for the same reason this project cannot access income data at 100m grid), though as static, non-interactive scenario maps rather than a live tool. None of the four apply a small-numbers/Bayesian-shrinkage correction — this project's `shrink_senior_rate()` (N_PRIOR=50) is a genuine methodological contribution beyond the reviewed precedents, not a replication of an existing technique.

**The interactive-tools/DSS gap is now closed.** Five sources map the landscape of prior climate-adaptation decision-support tools, and — critically — none combine a social-vulnerability dimension with live heat and surface-water simulation. The closest prior tool is **Cavan et al. 2014**'s GRaBS Assessment Tool + STAR Tools (EU-funded, 10 European municipalities, 2008–2014): the Assessment Tool overlays 350+ static vulnerability/hazard layers with no live computation, and the STAR Tools — added specifically to enable "what-if" scenario modeling — ship as **two separate, independently-run tools** (a Surface Temperature Tool and a Surface Runoff Tool), the strongest concrete precedent for this project's "prior tools treat heat and surface-water as separate modules" claim. **Smith et al. 2009** is an earlier (and thinner) Manchester forerunner of the same tool lineage — cite briefly, not as independent evidence. Three physics/ML tools span the accessibility-vs-completeness spectrum: **UMEP-TARGET** (Chen et al. 2026) is the lightest-weight physics-based option (energy-balance model, <1 hour desktop runtime via a QGIS plugin) and is explicitly motivated by the same "the barrier is the interface, not the model" argument this project makes; **DUCT** (Aydt et al. 2026, Singapore) is the heaviest (WRF+PALM-4U coupling, up to 6,144 core-hours per run, proprietary multi-agency data); the **Lahti digital twin** (Bandaranayake et al. 2026) uses a fast ML surrogate (random forest, R²=0.96) but its own user evaluation found "Accuracy and Trust" the lowest-scoring dimension despite the strong technical accuracy — a citable argument for this project's fully-sourced, per-coefficient-citable approach over black-box prediction. All three lack any vulnerability dimension. See [[wiki/concepts/heat-vulnerability-index]] and [[wiki/concepts/interactive-climate-tools]] for full detail.

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
| Equal-weighted additive HVI avoids PCA subjectivity | Strong — explicit methodological argument, census-block validated | [[wiki/sources/aubrecht-oezceylan-2013-ncr-heat-risk]] |
| PCA-derived HVIs are unstable/uninterpretable across studies | Strong — systematic review of 13 validated HVI studies | [[wiki/sources/niu-2021-hvi-systematic-review]] |
| No prior tool integrates heat + vulnerability + live water/unsealing simulation | Strong — direct admission by authors of the closest prior tool (STAR Tools ships heat and runoff as two separate tools) | [[wiki/sources/cavan-2014-grabs-star-tools]] |
| Interface accessibility ≠ compute/data accessibility (heavyweight DT still needs HPC + proprietary data) | Medium — single heavily-instrumented case study (Singapore) | [[wiki/sources/aydt-2026-duct-singapore]] |
| ML-predicted climate outcomes score lower on user trust than technical accuracy | Medium — n=5 expert evaluation, single city | [[wiki/sources/bandaranayake-2026-lahti-digital-twin]] |

---

## Active Debates

- **Drought vs. cooling tradeoff**: climate-resilient tree selection may reduce cooling effectiveness by ~11%. Needs longer-term survival data to resolve.
- **LST vs. air temperature**: all remote sensing studies measure LST, but health impacts relate to air temperature. The translation is imperfect.
- **NDVI vs. tree canopy cover** as the right metric: NDVI conflates grass and trees; individual tree crowns are more precise but require high-resolution data.
- **Bavarian deregulation**: whether Modernisierungsgesetz 2025 meaningfully erodes surface sealing protections is contested between researchers and government.
- **PCA vs. fixed/literature-derived weighting for HVIs**: PCA is more "data-driven" but produces uninterpretable, study-area-specific components (Niu et al. 2021); fixed weighting is transparent and reproducible but requires defending specific weight values against the literature. This project's 0.6/0.4 LST/elderly split follows the fixed-weighting camp (same as Aubrecht & Özceylan 2013) — needs explicit justification in Methods, not just an implementation choice.
- **Additive vs. multiplicative hazard–vulnerability combination**: multiplicative (Crichton's Risk Triangle, used by Chen et al. 2018 and Aubrecht & Özceylan 2013) implies zero risk if either hazard or vulnerability is zero; additive weighted-sum (this project) does not have that property. A substantive methodological choice worth stating explicitly, not glossing over.
- **Model simplification vs. better interfaces on heavyweight models** as the path to tool accessibility: DUCT (Singapore) keeps full physical complexity and builds a polished UI on top, but still requires HPC and proprietary data; TARGET/UMEP and this project instead simplify the underlying model to achieve genuine desktop/browser-level accessibility. The reviewed evidence favors model-simplification for true accessibility, but at an explicit cost in physical completeness (no advection, no anthropogenic heat, simplified geometry) that should be stated as a limitation, not hidden.

---

## Next Sources to Find

Priority:
1. **Würzburg-specific heat / climate data** — any existing heat mapping study for Würzburg
2. **Health-outcome validation for HVIs** — Reid et al. 2009, Wolf & McGregor 2013, Conlon et al. 2020 identified as candidates (URLs on file) but not yet ingested; would strengthen the HVI validation limitation currently only covered secondhand via Niu et al. 2021's review
3. **Second ZURES/Ludwigsburg paper** — Laranjeira et al. (household survey, companion to Birkmann et al. 2021) identified but not yet ingested; would add primary-source epidemiological grounding for the age/poverty vulnerability weighting currently only cited secondhand via Birkmann et al.'s summary
4. **Rötzer's primary paper** on tree cooling quantification (40,000 kWh figure) — currently only cited in journalism

*(Note: per explicit project decision 2026-08-18, no further sources are being added for the current paper draft — items above are flagged for a possible future revision, not active work.)*

---

## Source Count by Topic

| Topic | Sources |
|-------|---------|
| LST–tree correlation / remote sensing | 4 |
| Green infrastructure / tree cooling | 5 |
| Impervious surface / Versiegelung | 2 |
| Entsiegelung / surface unsealing | 4 |
| Urban morphology / LCZ | 2 |
| Simulation (WRF, LCZ) | 1 |
| Policy (Bavaria) | 1 |
| Species selection / drought tradeoff | 1 |
| Tree allometry / crown size | 2 |
| Canopy cover modeling | 1 |
| Health impacts | 0 |
| Equity / vulnerable populations (Heat Vulnerability Index) | **4** — see [[wiki/concepts/heat-vulnerability-index]] |
| Interactive tools / decision-support systems | **5** — see [[wiki/concepts/interactive-climate-tools]] |
| Würzburg-specific | **1 direct** (Moser-Reischl 2021) + 1 indirect (Würzburg researchers studied Munich) |
