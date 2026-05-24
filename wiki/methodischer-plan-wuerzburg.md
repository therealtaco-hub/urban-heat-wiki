---
title: "Methodischer Plan: Urban Heat Mapping Würzburg"
type: overview
tags: [würzburg, methodik, plan, lst, simulation, zensus, vulnerabilität]
sources: 10
updated: 2026-05-20
---

# Methodischer Plan: Urban Heat Mapping Würzburg

Strukturierter Arbeitsplan für das Würzburg-Projekt. Basiert auf Synthese aller bisherigen Wiki-Quellen. Bei neuen Erkenntnissen aktualisieren.

---

## Phase 1 — Datenbeschaffung

**1.1 Land Surface Temperature (LST) — Ziel: 10 m Auflösung**

Empfehlung: **GEE-Downscaling-Tool** (Onačillová et al. 2022) direkt verwenden. Liefert LST auf 10 m, kostenlos, ohne eigene Algorithmus-Implementierung. Vollständige Schritt-für-Schritt-Anleitung: [[wiki/sources/onacillova-2022-lst-downscaling]]

**Konkrete Vorgehensweise:**

1. **GEE-Account anlegen** (kostenlos): https://earthengine.google.com
2. **GEE-App öffnen:** https://danielp.users.earthengine.app/view/lst-downscaling
3. **ROI definieren:** Geometry-Tool verwenden, Polygon über Würzburg zeichnen (~87 km², Limit 1000 km²).
4. **Zeitraum setzen:** Sommermonate, z.B. 2022-06-01 bis 2022-09-30.
5. **Landsat-Szene auswählen:** "Generate Image Collections" klicken → Szenen-IDs mit <5% Wolkenbedeckung werden aufgelistet. Eine Szene auswählen.
6. **Passende Sentinel-2-Szene finden:** gleicher Aufnahmetag wie die gewählte Landsat-Szene (Sentinel-2 hat ~5-Tage-Revisit; ein Überlappungstag mit Landsat reicht). Szenen-ID eintragen.
7. **Ausgabe generieren:** Layer `LST 10 m (with residuals)` verwenden (enthält Residualkorrektur zur Energieerhaltung).
8. **Export:** Als GeoTIFF auf Google Drive exportieren.
9. **Wiederholen** für 2–3 weitere klare Sommertage (verschiedene Jahre) → Mittelwert bilden für Robustheit.

**Fallback (ohne GEE-App, manuell in Python/QGIS):**
- Landsat Collection 2 Level-2 ST-Produkt herunterladen (LST wird direkt geliefert; Skalierungsfaktor ×0.00341802 + 149.0 K, dann −273.15 für °C).
- Sentinel-2 MSI Level-2A für denselben Tag laden.
- NDVI, NDBI, NDWI aus Landsat (30 m) und Sentinel-2 (10 m) berechnen.
- OLS-Regression fitten: `LST30m = a0 + a1×NDVI + a2×NDBI + a3×NDWI`
- Koeffizienten auf S2-10m-Indizes anwenden → LST10m_pred.
- Residuen (30 m) auf 10 m resampeln und addieren → LST10m final.

**Wichtige Einschränkungen:**
- Nur unter wolkenfreien Bedingungen (<5% Wolken) anwendbar — in Würzburger Sommern ggf. nur 3–6 nutzbare Tage pro Saison.
- RMSE ~4,2 °C gegen In-situ-Messung: Methode für räumliche Muster (Hotspot-Analyse) geeignet, nicht für Absoluttemperatur-Aussagen.
- Quelle: [[wiki/sources/onacillova-2022-lst-downscaling]]

**1.2 Baumbestandsdaten**
- *Beste Option*: Einzelkronendaten aus städtischem GIS Würzburg (Baumkataster) + hochauflösende Luftbilddaten → Einzelkronensegmentierung (analog zu den >166.000 Bäumen in München bei [[wiki/sources/garcia-de-leon-lst-trees-munich]])
- *Fallback*: NDVI aus Sentinel-2 als Proxy für Vegetationsdichte — aber: nur über NDVI > 0,4 ist ein Kühleffekt nachweisbar ([[wiki/sources/li-et-al-urban-form-lst-xgboost]])
- Zielgröße: **prozentuale Baumkronendeckung pro Polygon**

**1.3 Flächennutzung**
- ATKIS-Daten (wie in München-Studie) oder städtisches GIS Würzburg
- Kategorien: Wohngebiet, Mischgebiet, Gewerbe, Verkehr, Erholung — analog zu den 5 Klassen bei García de León et al.
- OpenStreetMap als ergänzende Quelle

**1.4 Demographiedaten (Vulnerabilität)**
- **Zensus 2022** — 100m-Rasterdaten für Deutschland (frei verfügbar über zensus2022.de)
- Relevante Variablen: Anteil >65 Jahre (Rentner), Anteil <6 Jahre (Kleinkinder) pro Rasterzelle
- Räumliche Überlagerung mit LST und Baumbestand → Identifikation von Hotspots mit hoher Wärmebelastung UND hoher Vulnerabilität

**1.5 Gebäude- und Morphologiedaten (für Simulation)**
- Gebäudegrundrisse + Höhen aus LoD2-Daten (Bayern: Bayerische Vermessungsverwaltung, kostenlos)
- Für LCZ-Klassifikation und WRF-Input → [[wiki/concepts/local-climate-zones]]

---

## Phase 2 — Korrelationsanalyse (LST × Baumbestand)

Methodik analog [[wiki/sources/garcia-de-leon-lst-trees-munich]]:

1. Flächennutzungspolygone als Analyseeinheiten
2. Pro Polygon extrahieren: mittlere LST + prozentuale Baumkronendeckung
3. **Lineare Regression** pro Nutzungsklasse: `LST ~ Baumkronendeckung (%)`
4. Benchmark-Koeffizienten aus München (Zielwerte für Würzburg-Validierung):

| Nutzungsklasse | Erwarteter Koeffizient |
|---|---|
| Gesamtstadt | ~−0,069°C pro 1% |
| Mischgebiet | ~−0,083°C pro 1% |
| Wohngebiet | ~−0,083°C pro 1% |
| Erholungsfläche | ~−0,038°C pro 1% |

5. Ergänzend: NDVI und NDBI als Prädiktoren → Vergleich, welcher Index LST besser erklärt (→ [[wiki/concepts/ndvi]])
6. Visualisierung: Violinplots (LST-Verteilung nach Nutzungsklasse), Regressionsgeraden, Karten

**Erwartetes Ergebnis:** Karte von Würzburg mit LST-Hotspots, überlagert mit Baumbestandsdichte — visuell und statistisch belegt, dass Baumflächen deutlich kühler sind.

---

## Phase 3 — Vulnerabilitätskartierung

1. Zensus-2022-Raster (100m) mit Altersstruktur für Würzburg laden
2. **Vulnerability Index** konstruieren: gewichteter Score aus Anteil >65 Jahre + Anteil <6 Jahre pro Rasterzelle
3. Überlagerung mit LST-Karte → **kombinierte Heatmap**: hohe Temperatur + hohe Vulnerabilität = höchste Priorität
4. Optional: weitere Sozialindikatoren (Haushaltsgröße, Migrationshintergrund) als zusätzliche Vulnerabilitätsdimension

**Erwartetes Ergebnis:** Priorisierungskarte — welche Stadtgebiete brauchen dringend Bäume/Entsiegelung, weil dort die gefährdetsten Gruppen leben.

---

## Phase 4 — Simulation

Zwei Simulationsebenen mit unterschiedlichem Aufwand und Präzision:

**4.1 Statistische Simulation (einfach, sofort umsetzbar)**
- Nutzt die Regressionskoeffizienten aus Phase 2
- Formel: `ΔLST = Koeffizient × ΔBaumkronendeckung (%)`
- Beispiel: Baumkronendeckung in Block X von 5% auf 25% (+20%) → ΔLST = 20 × 0,083 = **−1,66°C**
- Umsetzung: interaktives Tool (z.B. Python/Streamlit) — Nutzer wählt Fläche + Anzahl Bäume, Tool gibt Temperaturdifferenz aus
- Limitation: nur LST, keine Lufttemperatur; keine Rückkopplung mit Stadtmorphologie

**4.2 Physikalische Simulation (aufwändiger, wissenschaftlich belastbarer)**
- LCZ-Karte für Würzburg erstellen (aus LoD2 + ATKIS) → analog zu [[wiki/sources/muhammad-2021-urban-morphology-uhi]]
- LCZ als Input für **WRF-Modell** → Lufttemperatur-Simulation
- Counterfactual-Szenarien: LCZ-Klasse für Zielgebiet ändern (z.B. "versiegelte Fläche" → "locker bebaut mit Bäumen") → neue Simulation → Lufttemperaturdifferenz
- Alternativ für Blockmaßstab: **ENVI-met** (Mikroklima-Simulationstool) — noch keine Quelle im Wiki

**Entsiegelungseffekt:**
- Physikalisch: Entsiegelung → höhere Bodenfeuchte → mehr ET → Kühlung + Albedoerhöhung
- Formel: **ΔTempLST = −0,03°C × ΔVersiegelung [%]** *(Tervooren 2015, Potsdam, R²=0,75–0,80)* → [[wiki/concepts/entsiegelung]]
- Belagstypenwahl bestimmt Versickerungsgrad (Abflussbeiwert) → [[wiki/sources/leitfaden-flaechenentsiegelung-2024]]
- Entsiegelungskoeffizient ~2,3× schwächer als Baumkoeffizient — aber Mehrfachnutzen (Infiltration, Grundwasser, Biodiversität)

---

## Phase 5 — Visualisierung & Kommunikation

- **Interaktive Karte** (Leaflet/Folium oder QGIS2Web): LST-Heatmap + Baumbestand + Vulnerabilitätslayer schaltbar
- **Simulationstool**: Nutzer klickt Fläche an, wählt Maßnahme ("20 Bäume" / "500m² entsiegeln"), bekommt Temperaturabschätzung
- **Priorisierungskarte** (Phase 3) als PDF für Stadtplanung

---

## Datenquellen-Übersicht

| Datensatz | Quelle | Kosten | Status |
|---|---|---|---|
| Landsat 8/9 | USGS EarthExplorer / GEE | kostenlos | zu laden |
| Sentinel-2 | Copernicus Open Access Hub | kostenlos | zu laden |
| Baumkataster Würzburg | Stadt Würzburg (GIS-Amt) | anfragen | offen |
| ATKIS Flächennutzung | BayernAtlas / LVG Bayern | kostenlos | zu laden |
| Zensus 2022 | zensus2022.de (Destatis) | kostenlos | zu laden |
| LoD2 Gebäude Bayern | Bayerische Vermessungsverwaltung | kostenlos | zu laden |

---

## Offene Methodenfragen (Lücken im Wiki)

| Lücke | Priorität | Nächster Schritt |
|---|---|---|
| Mikroskaliensimulation (ENVI-met) | hoch | Quelle zu ENVI-met-Methodik besorgen |
| Entsiegelungskoeffizient (°C-Reduktion) | ~~hoch~~ | **Geschlossen**: −0,03°C pro 1% Entsiegelung — [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |
| LST-Downscaling auf 10 m | ~~hoch~~ | **Geschlossen**: GEE-App direkt einsetzbar — [[wiki/sources/onacillova-2022-lst-downscaling]] |
| Lufttemperatur vs. LST (Übersetzung) | mittel | Quelle zu LST-Tair-Beziehung besorgen |
| Würzburg-spezifische Kalibrierung | mittel | nach Phase-2-Ergebnissen beurteilen |
| Gesundheitliche Temperaturschwellen | mittel | Hitzemortalitätsliteratur besorgen |

---

## Quellen-Grundlage dieses Plans

- [[wiki/sources/garcia-de-leon-lst-trees-munich]] — methodisches Template (Würzburg/DLR/TUM)
- [[wiki/sources/schwaab-2021-trees-european-cities]] — europäischer Benchmark (8–12 K)
- [[wiki/sources/muhammad-2021-urban-morphology-uhi]] — LCZ+WRF Simulationspipeline
- [[wiki/sources/li-et-al-urban-form-lst-xgboost]] — Schwellenwerte, LCZ, Morphologie
- [[wiki/sources/elmes-2017-tree-canopy-loss-lst]] — kausaler Baumverlust-LST-Effekt
- [[wiki/sources/klimabaeume-fuer-die-stadt]] — Artenauswahl und Transpirationskoeffizienten
- [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] — Entsiegelungskoeffizient −0,03°C/% (Phase 4)
- [[wiki/sources/leitfaden-flaechenentsiegelung-2024]] — Abflussbeiwerte und Belagskosten (Phase 4)
- [[wiki/sources/uba-texte141-2021-entsiegelung]] — Rechtslage, Copernicus Imperviousness Layer (Phase 1)
- [[wiki/sources/onacillova-2022-lst-downscaling]] — LST-Downscaling auf 10 m via GEE (Phase 1.1)
