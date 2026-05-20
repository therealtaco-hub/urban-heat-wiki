---
title: "Simulationslogik: Bäume & Entsiegelung"
type: overview
tags: [simulation, bäume, entsiegelung, formel, implementierung, würzburg]
sources: 3
updated: 2026-05-20
---

# Simulationslogik: Bäume & Entsiegelung

Dieses Dokument ist die autoritative Quelle für die Berechnungslogik der beiden Simulationsendpoints in *Resilientes Würzburg*. Es übersetzt Wiki-Evidenz in konkrete Input/Output-Verträge für den Code.

**Code-Referenz:** `backend/simulation_params.py` enthält alle Koeffizienten mit Quellverweisen.
**Implementierungsort:** `backend/routers/simulate.py`

---

## Simulation A — Baumneupflanzung (GET /api/simulate/baeume)

### Wissenschaftliche Grundlage

| Koeffizient | Wert | Quelle |
|---|---|---|
| ΔLST pro 1 % Kronendeckung (Mischgebiet) | −0,083 °C | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| ΔLST pro 1 % Kronendeckung (Gesamtstadt) | −0,069 °C | [[wiki/sources/garcia-de-leon-lst-trees-munich]] |
| Transpiration LB3 (feuchteadaptiert) | 0,19 kg H₂O m⁻² Tag⁻¹ | [[wiki/sources/klimabaeume-fuer-die-stadt]] |
| Transpiration LB6 (trockenheitstolerant) | 0,17 kg H₂O m⁻² Tag⁻¹ | [[wiki/sources/klimabaeume-fuer-die-stadt]] |

### Inputs

```
n_trees:      int    — Anzahl Neupflanzungen
area_m2:      float  — Bezugsfläche (z.B. Stadtbezirk oder ausgewähltes Polygon)
land_use:     str    — "mixed" | "recreational" | "overall" (Standard: "mixed")
species_type: str    — "lb3" | "lb6" (Standard: "lb6")
```

### Berechnung

**Schritt 1 — Kronendeckungszuwachs:**
```
crown_area_total = n_trees × CROWN_AREA_M2_DEFAULT      # 50 m² pro Baum
delta_coverage_pct = crown_area_total / area_m2 × 100   # in %
```

**Schritt 2 — LST-Reduktion:**
```
# Koeffizient nach Flächennutzungsklasse (aus simulation_params.py)
coeff = LST_PER_PCT_CANOPY_MIXED        # –0.083 für Mischgebiet
delta_lst_celsius = coeff × delta_coverage_pct
```

**Schritt 3 — Transpirationskühlleistung:**
```
transpiration_rate = TRANSPIRATION_LB3  # oder LB6 je nach species_type
# Tageswert: Gesamtkronenfläche × Transpirationsrate
daily_kg = crown_area_total × transpiration_rate
# Jahreskühlleistung in kWh
cooling_kwh_year = daily_kg × 365 × LATENT_HEAT_KWH_PER_KG
```

### Output (JSON)

```json
{
  "n_trees": 50,
  "area_m2": 120000,
  "delta_coverage_pct": 2.08,
  "delta_lst_celsius": -0.17,
  "cooling_kwh_year": 110400,
  "species_type": "lb6",
  "land_use": "mixed",
  "coefficients_used": {
    "lst_per_pct": -0.083,
    "transpiration_kg_m2_day": 0.17,
    "crown_area_m2": 50.0
  },
  "caveats": [
    "Koeffizient aus München (Würzburg-Forscher) — nicht lokal kalibriert",
    "Kronenfläche 50 m² ist Literatur-Mittelwert, keine Würzburg-Messung",
    "LST ≠ Lufttemperatur"
  ]
}
```

### Bekannte Einschränkungen

- Koeffizient −0,083 °C/% aus München (Sommer 2020, R² ≈ 0,61) — noch nicht mit Würzburger Daten validiert.
- Kronenfläche 50 m² pro Baum: Würzburger Baumkataster enthält keine Kronendurchmesser-Messung → Literaturwert. Verbesserung: LiDAR oder Luftbildsegmentierung.
- Modell ist rein statistisch (kein physikalisches Mikroklimamodell); keine Rückkopplung mit Stadtmorphologie.
- Kühlwirkung bezieht sich auf Landoberflächentemperatur (LST), nicht Lufttemperatur.

---

## Simulation B — Flächenentsiegelung (GET /api/simulate/wasser)

### Wissenschaftliche Grundlage

| Koeffizient | Wert | Quelle |
|---|---|---|
| ΔLST pro 1 % Entsiegelung | −0,03 °C | [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |
| Jahresniederschlag Würzburg | ~600 mm/Jahr | DWD, via CLAUDE.md |
| Abflussbeiwerte nach Belagstyp | siehe Tabelle | [[wiki/sources/leitfaden-flaechenentsiegelung-2024]] |

### Inputs

```
area_m2:       float  — Entsiegelungsfläche
from_surface:  str    — Ausgangsbelag (z.B. "asphalt")
to_surface:    str    — Zielbelag (z.B. "schotterrasen", "rasengitter", "rasendecke")
reference_m2:  float  — Gesamtfläche des Bezugsgebiets (für LST-%-Berechnung)
```

### Berechnung

**Schritt 1 — LST-Reduktion:**
```
# Prozentsatz der entsiegelten Fläche relativ zum Bezugsgebiet
unsealing_pct = area_m2 / reference_m2 × 100
delta_lst_celsius = LST_PER_PCT_UNSEALING × unsealing_pct    # –0.03 °C pro %
```

**Schritt 2 — Versickerungszunahme (Rational-Formel):**
```
C_current = RUNOFF_COEFFICIENTS[from_surface]   # z.B. 0.95 für Asphalt
C_target  = RUNOFF_COEFFICIENTS[to_surface]     # z.B. 0.30 für Schotterrasen
delta_C   = C_current - C_target                # Abflussbeiwert-Differenz

# Jährliche Versickerungszunahme
infiltration_m3_year = area_m2 × ANNUAL_RAINFALL_WUERZBURG_M × delta_C
```

**Beispiel:** 1.000 m² Asphalt → Schotterrasen:
```
delta_C = 0.95 – 0.30 = 0.65
infiltration = 1000 × 0.60 × 0.65 = 390 m³/Jahr
delta_lst = (1000 / reference_m2 × 100) × (–0.03)
```

### Output (JSON)

```json
{
  "area_m2": 1000,
  "from_surface": "asphalt",
  "to_surface": "schotterrasen",
  "reference_m2": 500000,
  "unsealing_pct": 0.2,
  "delta_lst_celsius": -0.006,
  "infiltration_m3_year": 390.0,
  "runoff_coefficients": { "from": 0.95, "to": 0.30, "delta": 0.65 },
  "caveats": [
    "LST-Koeffizient aus Potsdam (Cfb) — Würzburg (Dfb) nicht direkt validiert",
    "Rational-Formel setzt homogenen Niederschlag und Bodendurchlässigkeit voraus",
    "Bodenversickerungskapazität lokal verschieden — LfU Bayern-Daten für präzise C-Werte"
  ]
}
```

### Bekannte Einschränkungen

- LST-Koeffizient aus Potsdam (Cfb), Würzburg ist Dfb — Klimazonentransfer plausibel, nicht validiert.
- Rational-Formel nimmt homogene Bodendurchlässigkeit an; lokale Bodenart (LfU Bayern) würde Präzision erhöhen.
- Große Entsiegelungsflächen lösen evtl. Verdunstungskühleffekt aus (Schwammstadt-Prinzip) — dieser Effekt ist in der LST-Formel implizit enthalten (Tervooren misst Nettoeffekt), aber nicht separat quantifiziert.

---

## Vergleich der beiden Simulationen

| | Baumpflanzung | Entsiegelung |
|---|---|---|
| LST-Koeffizient | −0,083 °C/% (Mischgebiet) | −0,030 °C/% |
| Stärke pro Prozentpunkt | **~2,8× stärker** | Referenz |
| Zusatznutzen | Transpirationskühlleistung (kWh) | Versickerung (m³/Jahr), Grundwasser |
| Modellbasis | Würzburg-Forscher, R² 0.41–0.61 | Potsdam, R² 0.75–0.80 |
| Lokale Validierung | ausstehend | ausstehend |

→ Bäume kühlen temperaturmäßig stärker, Entsiegelung liefert messbaren Wassernutzen zusätzlich.

---

## Offene Verbesserungen (nach erster Implementierung)

1. **Würzburg-Kalibrierung**: Sobald Phase-2-Regression (LST × Baumkronendeckung) für Würzburg abgeschlossen ist, eigene Koeffizienten aus lokalen Daten ableiten und `simulation_params.py` aktualisieren.
2. **Lokale Bodenversickerung**: LfU Bayern Bodendaten (WFS) für präzise Abflussbeiwerte je Bodentypeinheit statt Literatur-Mittelwerte.
3. **Kombinierte Simulation**: Baumpflanzung auf entsiegelter Fläche (Koeffizient aus Tervooren bestätigt: Entsiegelung + Bepflanzung kombiniert > Entsiegelung allein).
4. **Physikalische Simulation**: ENVI-met oder WRF für Blockmaßstab — wenn statistische Simulation zu grob.

---

## Quellen

- [[wiki/sources/garcia-de-leon-lst-trees-munich]] — Baum-Koeffizient −0,083 °C/%
- [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] — Entsiegelungskoeffizient −0,03 °C/%
- [[wiki/sources/leitfaden-flaechenentsiegelung-2024]] — Abflussbeiwerte, Bayreuth Bayern
- [[wiki/sources/klimabaeume-fuer-die-stadt]] — Transpirationsraten LB3/LB6
- [[wiki/methodischer-plan-wuerzburg]] — Projektplan Phase 4 (Simulation)
