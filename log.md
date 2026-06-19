# Activity Log

## [2026-06-19] ingest | 3 Allometrie- & Kronendeckungs-Quellen
- Raw files: Moser-Reischl et al. (2021) Arboric. & Urban For. 47(4), Pretzsch et al. (2015) UFUG 14(3), Gray et al. (2021) Forest Ecol. Mgmt. 501
- Files created (3): wiki/sources/moser-reischl-2021-urban-tree-growth-germany.md, wiki/sources/pretzsch-2015-urban-tree-crown-allometry.md, wiki/sources/gray-2021-canopy-cover-prediction.md
- Files updated (8): wiki/concepts/tree-species-selection.md (allometric type table, Würzburg CPA data, park/street effect), wiki/simulation-logic.md (kronenfläche-Berechnung konkretisiert; 50m²-Default-Caveat; Gray-Validierung des Überlappungsmodells; 3 neue Quellen), wiki/entities/thomas-roetzer.md (sources 3→5; Pretzsch 2015 + Moser-Reischl 2021 ergänzt), wiki/entities/wuerzburg.md (Moser-Reischl als Direktstudie ergänzt), wiki/entities/tu-muenchen.md (sources 1→3; Pretzsch + Moser-Reischl ergänzt), wiki/overview.md (Kronenfläche-Lücke geschlossen; Source-Count-Tabelle erweitert), index.md, log.md
- Total sources now: 16 | Total pages: 36
- Key contribution (Moser-Reischl 2021): Würzburg ist direkte Studienstadt — Allometrie-Tabellen für Tilia/Platanus/Robinia/Aesculus aus Würzburg-Messungen (n=75–89 je Art). Schließt offenes TODO "Kronenfläche der Bäume berechnen": CPA = π × (kronenbrei/2)² als Primärformel; allometrischer Fallback CPA = exp(a) × DBH^b.
- Key contribution (Pretzsch 2015): Alle 4 Würzburg-Hauptarten = Allometrischer Typ 1 (größte Kronenfläche aller 22 Arten). Type-1-Mittel bei DBH=25cm: CPA 65,6 m² > unser Default 50 m².
- Key contribution (Gray 2021): Beer-Lambert/Crookston & Stage Überlappungsmodell empirisch validiert. RMSE ~12–14 % Cover. Modell unterschätzt bei >90 % Deckung — für urbane Würzburg-Szenarien (Deckung typisch <60 %) unkritisch.

Append-only record of all wiki activity. Most recent entry at top.

Parse tip: `grep "^## \[" log.md | head -10` gives the 10 most recent entries.

---

## [2026-06-10] update | Pflanzpotenzial je Zelle über Versiegelungsgrad (Teil 2)
- Schritt "Pflanzpotenzial je Zelle" ergänzt: seal_pct (flächengew. Versiegelungsgrad aus
  ATKIS/OSM) begrenzt n_trees_max = floor(pflanzbare Fläche / 25 m²), nicht den Kühl-Nenner.
  Orthogonal zum Überlappungsmodell. Quellen Arnold & Gibbons 1996 + SEAL_RATE_BY_TYPE-Literatur.
- Files updated (1): wiki/simulation-logic.md

## [2026-06-10] update | Kronendeckung auf Überlappungsmodell (Crookston & Stage 1999)
- Schritt 1 der Baum-Simulationslogik von naiver Kronensumme auf projizierte Kronendeckung
  umgestellt: `total = (1 − exp(−(existing_ratio + new_ratio))) × 100`, Δ°C nur auf
  `effective_new_pct`. Headroom-Cap entfällt. Quellen Crookston & Stage 1999 / Jennings 1999 ergänzt.
- Output-JSON: `delta_coverage_pct` → `crown_area_ratio` + `effective_new_pct` + `total_coverage_pct`.
- Files updated (1): wiki/simulation-logic.md

## [2026-06-08] ingest | DWA-A138 Regenwasserbewirtschaftung Bayern (LfU / Florian Ettinger)
- Raw file: dwa_a138_lfu.pdf
- Files created (1): wiki/sources/dwa-a138-lfu-regenwasser-bayern.md
- Files updated (5): wiki/concepts/entsiegelung.md (Abflussbeiwert-Tabelle auf DWA-A138 umgestellt, Gründach-Zeilen ergänzt, Primärquelle deklariert), wiki/simulation-logic.md (Quellverweis auf DWA-A138 aktualisiert, Asphalt-Diskrepanz dokumentiert), wiki/overview.md (Quellzähler + Syntheseabsatz), index.md, log.md
- Total sources now: 13 | Total pages: 33
- Key contribution: DWA-A138 / LfU Bayern ist die autoritative Primärquelle für alle Abflussbeiwerte in simulation_params.py — bislang nur sekundär über Leitfaden Bayreuth 2024 referenziert
- Neue Werte: Pflaster dichte Fugen 0,75; Verbundsteine/Sickersteine 0,25; Gründach-Staffelung (0,3/0,5/0,7 je Aufbaudicke)
- Diskrepanz dokumentiert: Asphalt DWA-A138 = 0,9 vs. simulation_params.py = 0,95 (beide innerhalb Bandbreite; Anpassung optional)

## [2026-05-21] ingest | Onačillová et al. 2022 — LST Downscaling Landsat+Sentinel-2 in GEE
- Raw file: remotesensing-14-04076-v2.pdf
- Files created (1): wiki/sources/onacillova-2022-lst-downscaling.md
- Files updated (6): wiki/concepts/remote-sensing-methods.md (step-by-step downscaling section + GEE app), wiki/concepts/land-surface-temperature.md (10 m achievability, accuracy caveat), wiki/concepts/ndvi.md (bivariate R² table), wiki/methodischer-plan-wuerzburg.md (Phase 1.1 konkretisiert + Lücke geschlossen), wiki/overview.md, index.md
- Total sources now: 12 | Total pages: 32
- Key contribution: free GEE app delivers 10 m LST for Würzburg out of the box; step-by-step guide filed in source page and methodischer plan
- Limitation filed: RMSE ~4.2 °C — use for spatial patterns, not absolute temperatures

## [2026-05-20] update | Brücke zu Code-Projekt resilientes_wuerzburg
- Neu: wiki/simulation-logic.md — Berechnungslogik für beide Simulationsendpoints (Input/Output, Formeln, Caveats)
- Neu: backend/simulation_params.py im Code-Projekt (alle Koeffizienten mit Wiki-Quellverweisen)
- Update: CLAUDE.md des Code-Projekts um Wiki-Referenzabschnitt ergänzt
- Update: index.md um simulation-logic.md erweitert; Quellzahlen korrigiert

## [2026-05-20] lint | P3 fixes
- green-infrastructure.md: doppelte Datentabellen zu einer zusammengeführt
- methodischer-plan-wuerzburg.md: Quellen-Grundlage um 3 Entsiegelung-Quellen ergänzt
- overview.md: Tervooren-Koeffizient in Strongest-Evidence-Tabelle eingetragen
- tervooren-2015.md: Wiki-Pages-Updated um land-surface-temperature und overview ergänzt

## [2026-05-20] lint | P1+P2 fixes
- urban-heat-island.md: doppelte Relevant-Entities-Sektion entfernt; sources 4→6; entsiegelung verlinkt
- evapotranspiration.md: sources 1→3; stangl + klimabaeume als Quellen ergänzt
- impervious-surface.md: sources 1→4
- thomas-roetzer.md: sources 1→3
- kuehleffekte-vergleich.md: sources 6→9
- methodischer-plan-wuerzburg.md: sources 6→9
- green-infrastructure.md: entsiegelung als Related Concept verlinkt
- land-surface-temperature.md: Tervooren-Formel + entsiegelung als Related Concept ergänzt
- muenchen.md: sources 1→2; garcia-de-leon Quelle ergänzt
- wuerzburg.md: entsiegelung verlinkt; uba-texte141 als Quelle ergänzt

## [2026-05-20] ingest | 3 Entsiegelung-Quellen + Konzeptseite
- Raw files: tervooren-2015 (AGIT Konferenzbeitrag), leitfaden-flaechenentsiegelung-2024 (Landkreis Bayreuth), uba-texte141-2021 (Umweltbundesamt)
- Files created (4): wiki/sources/tervooren-2015-gruenvolumen-potsdam, wiki/sources/leitfaden-flaechenentsiegelung-2024, wiki/sources/uba-texte141-2021-entsiegelung, wiki/concepts/entsiegelung
- Files updated (6): index.md, log.md, wiki/overview.md, wiki/kuehleffekte-vergleich.md (neu: Abschnitt L), wiki/methodischer-plan-wuerzburg.md (Lücke Entsiegelungskoeffizient geschlossen), wiki/concepts/impervious-surface.md
- Total sources now: 11 | Total pages: 31
- Lücke geschlossen: Entsiegelungskoeffizient −0,03°C pro 1% Versiegelungsreduktion (Tervooren 2015, Potsdam, R²=0,75–0,80)
- Schlüsselbefund: Entsiegelung kühlt ~2,3× schwächer pro Prozentpunkt als Baumpflanzung — aber Mehrfachnutzen (Infiltration, Grundwasser, Biodiversität)

## [2026-05-20] update | Stangl 2019 vollständig extrahiert
- Quantitative Daten für Parks, Gründächer, Vertikalbegrünung, thermischen Komfort nachgezogen
- Dateien aktualisiert: stangl-2019-wirkungen-gruene-stadt.md, kuehleffekte-vergleich.md
- Lücke "Stangl noch nicht extrahiert" geschlossen

## [2026-05-20] query | Methodischer Plan Würzburg
- Frage: strukturierter Arbeitsplan für das Würzburg-Projekt
- Output als Wiki-Seite abgelegt: [[wiki/methodischer-plan-wuerzburg]]
- Index aktualisiert

## [2026-05-20] query | Vergleichstabelle Kühleffekte
- Frage: Vergleich aller quantitativen Kühleffekte aus dem Wiki
- Output als Wiki-Seite abgelegt: [[wiki/kuehleffekte-vergleich]]
- Index aktualisiert

## [2026-05-20] ingest | Batch ingest — 7 academic papers
- Sources: Schwaab 2021 (Nature Comms), García de León et al. (Würzburg/DLR/TUM), Stratopoulos-Le Chalony 2020 (TUM dissertation), Elmes et al. 2017, Reta-Roba & Worku-Tabor, Li et al. (XGBoost-SHAP), Stangl et al. 2019, Muhammad 2021 (TUM thesis)
- Files created (source pages): garcia-de-leon-lst-trees-munich, schwaab-2021-trees-european-cities, klimabaeume-fuer-die-stadt, elmes-2017-tree-canopy-loss-lst, reta-roba-hawassa-vegetation-lst, li-et-al-urban-form-lst-xgboost, stangl-2019-wirkungen-gruene-stadt, muhammad-2021-urban-morphology-uhi
- Files created (concept pages): land-surface-temperature, ndvi, local-climate-zones, remote-sensing-methods, urban-morphology, tree-species-selection
- Files created (entity pages): wuerzburg, university-of-wuerzburg, dlr, eth-zurich
- Files updated: urban-heat-island, green-infrastructure, thomas-roetzer, overview, index, log
- Total pages now: 27 | Total sources: 8
- Key finding filed: Central European trees 8–12 K cooler than urban fabric (Schwaab); −0.069°C/% tree cover in Munich (García de León)
- Project context saved: Würzburg heat mapping project — LST correlation, vulnerable population targeting, simulation

## [2026-05-20] ingest | Gegen Hitze – Wissenschaftler berechnen Kühlleistung eines Baumes
- Source: BR24 article by Susanne Delonge, 2024-09-28
- Files created (9): `wiki/sources/gegen-hitze-kuehlleistung-baum.md`, `wiki/concepts/urban-heat-island.md`, `wiki/concepts/green-infrastructure.md`, `wiki/concepts/impervious-surface.md`, `wiki/concepts/evapotranspiration.md`, `wiki/entities/muenchen.md`, `wiki/entities/nuernberg.md`, `wiki/entities/thomas-roetzer.md`, `wiki/entities/tu-muenchen.md`
- Files updated (3): `wiki/overview.md`, `index.md`, `log.md`
- Key claim filed: 20m tree = up to 40,000 kWh/year cooling ≈ €16,000 AC equivalent (Rötzer, TU München)

## [2026-05-20] setup | Wiki initialized
- Created directory structure: `raw/`, `raw/assets/`, `wiki/`, `wiki/entities/`, `wiki/concepts/`, `wiki/sources/`
- Created `CLAUDE.md` schema
- Created `index.md` (empty catalog)
- Created `log.md` (this file)
- Created `wiki/overview.md` (stub)
- Domain: Urban Heat Mapping
- Vault: Obsidian, `C:\Code\Obsidian\Urban Heat Mapping`
