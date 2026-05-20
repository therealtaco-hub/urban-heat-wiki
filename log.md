# Activity Log

Append-only record of all wiki activity. Most recent entry at top.

Parse tip: `grep "^## \[" log.md | head -10` gives the 10 most recent entries.

---

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
