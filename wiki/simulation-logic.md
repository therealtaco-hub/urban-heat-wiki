---
title: "Simulationslogik: Bäume & Entsiegelung"
type: overview
tags: [simulation, bäume, entsiegelung, formel, implementierung, würzburg]
sources: 3
updated: 2026-06-10
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

**Schritt 1 — Projizierte Kronendeckung (negativ-exponentielles Überlappungsmodell):**
```
crown_area_total = n_trees × CROWN_AREA_M2_DEFAULT      # 50 m² pro Baum (Endausbau-Annahme)
new_ratio        = crown_area_total / area_m2           # Flächen-Verhältnis (kein Prozent)

# Bestand → äquivalentes Verhältnis (inverse Formel, log-sicher bei existing → 100):
existing_ratio   = −ln(1 − existing_coverage_pct / 100)

# Projizierte Gesamtdeckung nach Crookston & Stage (1999) — Bestand & Neu im selben Raum:
total_coverage_pct = (1 − exp(−(existing_ratio + new_ratio))) × 100
effective_new_pct  = total_coverage_pct − existing_coverage_pct      # realer Zuwachs, ≥ 0
```
Das Modell nimmt zufällige (Poisson-)Kronenüberlappung an und eliminiert die Doppelzählung
der naiven Summe `Σ Kronenfläche / Fläche`. Es konvergiert asymptotisch gegen 100 % — ein
harter Cap (früher `headroom`) entfällt. Annahme-Grenze: bei regelmäßigen Alleen leicht
unterschätzt, bei Park-Clustern leicht überschätzt (siehe Quellen).

**Schritt 2 — LST-Reduktion:**
```
# Koeffizient nach Flächennutzungsklasse (aus simulation_params.py)
coeff = LST_PER_PCT_CANOPY_MIXED        # –0.083 für Mischgebiet
# Δ°C nur auf den *projizierten* Zuwachs (= Kalibrierungsgröße García de León):
delta_lst_celsius = coeff × effective_new_pct
```

> [!note] Die projizierte Kronendeckung ist genau die Größe, gegen die der
> García-de-León-Koeffizient kalibriert ist (Vereinigungsfläche der Kronen, nicht Summe).
> Quellen: Crookston & Stage (1999, USDA RMRS-GTR-24, Primärquelle der Gleichung);
> Jennings et al. (1999, *Forestry* 72(1), canopy cover vs. closure); García de León et al. (2020).

**Pflanzpotenzial je Zelle (Versiegelungsgrad):**
```
seal_pct           = Σ(Überlappungsfläche × seal_rate) / Zellfläche   # je 100-m-Kachel, [0,1]
pflanzbare_flaeche = Zellfläche × (1 − seal_pct)
n_trees_max        = floor(pflanzbare_flaeche / MIN_GROUND_PER_TREE_M2)   # 25 m²/Baum
```
Versiegelter Boden (Dächer, Straßen) trägt keinen Stamm → der Versiegelungsgrad begrenzt die
**Stammzahl**, **nicht** den Kühl-Nenner `area_m2` (Kronen überhängen versiegelten Boden; der
Koeffizient ist gegen Deckung über die gesamte Polygonfläche kalibriert). `seal_rate` je
ATKIS/OSM-Typ aus Literaturwerten (UBA/DIN/Bayreuth; Arnold & Gibbons 1996). Kacheln ohne
ATKIS-Siedlungs-/Verkehrsfläche gelten als unversiegelt (Grün-/Freifläche). Orthogonal zum
Überlappungsmodell: Poisson begrenzt die Deckung *pro Krone*, der Versiegelungsgrad die *Stammzahl*.

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
  "crown_area_ratio": 0.021,
  "effective_new_pct": 2.06,
  "total_coverage_pct": 2.06,
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
- Kronenfläche 50 m² pro Baum: Das Baumkataster enthält `kronenbrei` (gemessener Kronendurchmesser). Bevorzugte Berechnung: `CPA = π × (kronenbrei/2)²`. Für Bäume ohne `kronenbrei`-Wert: allometrische Formel `CPA = exp(a) × DBH^b` aus [[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]] (Würzburg-Direktmessung, 2014–2017). Beide Wege sind datengestützt — der 50 m²-Default ist nun ein Fallback für fehlende Felder. Hinweis: 50 m² ist konservativ für ausgewachsene Bäume (Platanus Würzburg Mittel: 124 m²) und zu hoch für Jungbäume (DBH < 15 cm → CPA ≈ 15–25 m²). Quelle: [[wiki/sources/pretzsch-2015-urban-tree-crown-allometry]].
- Modell ist rein statistisch (kein physikalisches Mikroklimamodell); keine Rückkopplung mit Stadtmorphologie.
- Kühlwirkung bezieht sich auf Landoberflächentemperatur (LST), nicht Lufttemperatur.

---

## Simulation B — Flächenentsiegelung (GET /api/simulate/wasser)

### Wissenschaftliche Grundlage

| Koeffizient | Wert | Quelle |
|---|---|---|
| ΔLST pro 1 % Entsiegelung | −0,03 °C | [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |
| Jahresniederschlag Würzburg | ~574 mm/Jahr | DWD Klimanormalperiode 1991–2020, Station 05705 |
| Abflussbeiwerte nach Belagstyp | siehe Tabelle | [[wiki/sources/dwa-a138-lfu-regenwasser-bayern]] (Primärquelle, DWA-A138 / LfU Bayern) |

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
- Rational-Formel nimmt homogene Bodendurchlässigkeit an; lokale Bodenart (LfU Bayern, kf-Werte aus DWA-A138) würde Präzision erhöhen.
- Asphalt-Abflussbeiwert: DWA-A138 gibt 0,9; `simulation_params.py` verwendet 0,95 — innerhalb Bandbreite, DWA-A138 ist Primärquelle.
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

1. **Würzburg-Kalibrierung**: Sobald Phase-2-Regression (LST × Baumkronendeckung) für Würzburg abgeschlossen ist, eigene Koeffizienten aus lokalen Daten ableiten und `simulation_params.py` aktualisieren. Allometrische Grundlage für Kronendeckungs-Input jetzt vorhanden ([[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]]).
2. **Lokale Bodenversickerung**: LfU Bayern Bodendaten (WFS) für präzise Abflussbeiwerte je Bodentypeinheit statt Literatur-Mittelwerte.
3. **Kombinierte Simulation**: Baumpflanzung auf entsiegelter Fläche (Koeffizient aus Tervooren bestätigt: Entsiegelung + Bepflanzung kombiniert > Entsiegelung allein).
4. **Physikalische Simulation**: ENVI-met oder WRF für Blockmaßstab — wenn statistische Simulation zu grob.

---

## Quellen

- [[wiki/sources/garcia-de-leon-lst-trees-munich]] — Baum-Koeffizient −0,083 °C/%
- [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] — Entsiegelungskoeffizient −0,03 °C/%
- [[wiki/sources/dwa-a138-lfu-regenwasser-bayern]] — Abflussbeiwerte (DWA-A138 / LfU Bayern, Primärquelle)
- [[wiki/sources/leitfaden-flaechenentsiegelung-2024]] — Kosten, ergänzende Bandbreiten
- [[wiki/sources/klimabaeume-fuer-die-stadt]] — Transpirationsraten LB3/LB6
- [[wiki/sources/moser-reischl-2021-urban-tree-growth-germany]] — Würzburg-spezifische CPA-Allometrie; Kronenfläche aus DBH und kronenbrei
- [[wiki/sources/pretzsch-2015-urban-tree-crown-allometry]] — Worldwide allometric type classification; CPA-Fallback für 22 Baumarten
- [[wiki/sources/gray-2021-canopy-cover-prediction]] — Beer-Lambert Überlappungsmodell empirisch validiert; RMSE-Caveat dokumentiert
- [[wiki/methodischer-plan-wuerzburg]] — Projektplan Phase 4 (Simulation)
