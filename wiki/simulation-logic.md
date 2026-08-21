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
n_trees:               int    — Anzahl Neupflanzungen
area_m2:               float  — Bezugsfläche (z.B. Stadtbezirk oder ausgewähltes Polygon)
existing_coverage_pct: float  — Bestehende Kronendeckung der Fläche in % (0–100, Default 0)
```

### Berechnung

**Schritt 1 — Projizierte Kronendeckung (negativ-exponentielles Überlappungsmodell):**
```
crown_area_total = n_trees × CROWN_AREA_M2_DEFAULT      # 50 m² pro Baum (konservativer Default, kein Endausbau — Kronengröße in Überarbeitung, siehe Backlog Task 8)
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
> Quellen: [[wiki/sources/crookston-stage-1999-cover-equation]] (USDA RMRS-GTR-24, Primärquelle der Gleichung);
> Jennings et al. (1999, *Forestry* 72(1), canopy cover vs. closure); García de León et al. (2025).

**Pflanzpotenzial je Zelle (Versiegelungsgrad):**
```
seal_pct           = Σ(Überlappungsfläche × seal_rate) / Zellfläche   # je 100-m-Kachel, [0,1]
pflanzbare_flaeche = Zellfläche × (1 − seal_pct)
n_trees_max        = floor(pflanzbare_flaeche / MIN_GROUND_PER_TREE_M2)   # 100 m²/Baum (FLL-Richtlinie, Bäume 2. Ordnung)
```
Versiegelter Boden (Dächer, Straßen) trägt keinen Stamm → der Versiegelungsgrad begrenzt die
**Stammzahl**, **nicht** den Kühl-Nenner `area_m2` (Kronen überhängen versiegelten Boden; der
Koeffizient ist gegen Deckung über die gesamte Polygonfläche kalibriert). `seal_rate` je
ATKIS/OSM-Typ aus Literaturwerten (UBA/DIN/Bayreuth; Arnold & Gibbons 1996). Kacheln ohne
ATKIS-Siedlungs-/Verkehrsfläche gelten als unversiegelt (Grün-/Freifläche). Orthogonal zum
Überlappungsmodell: Poisson begrenzt die Deckung *pro Krone*, der Versiegelungsgrad die *Stammzahl*.

**Schritt 3 — Transpirationskühlleistung (v2, noch nicht implementiert):**
```
# Geplant: Transpirationskühlleistung in kWh
# transpiration_rate = TRANSPIRATION_LB3 / LB6
# cooling_kwh_year   = n_trees × CROWN_AREA_M2_DEFAULT × transpiration_rate × 365 × LATENT_HEAT_KWH_PER_KG
# Noch nicht im Endpoint — kein Output-Feld cooling_kwh_year in v1.
```

### Output (JSON)

```json
{
  "n_trees": 50,
  "area_m2": 120000,
  "existing_coverage_pct": 0.0,
  "new_crown_area_ratio": 0.021,
  "effective_new_pct": 2.06,
  "total_coverage_pct": 2.06,
  "delta_lst_celsius": -0.17,
  "co2_kg_year": 625.0,
  "coefficients_used": {
    "lst_per_pct_canopy": -0.083,
    "land_use": "mixed",
    "crown_area_m2": 50.0,
    "co2_kg_per_tree_year": 12.5
  },
  "caveats": [
    "Koeffizient aus München (Würzburg-Forscher) — nicht lokal kalibriert",
    "50 m² Kronenfläche ist konservativer Default für mittelalte Bäume",
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
| Jahresniederschlag Würzburg | ~574 mm/Jahr (0,5735 m) | DWD Klimanormalperiode 1991–2020, Station 05705 |
| Abflussbeiwerte nach Belagstyp | siehe Tabelle | [[wiki/sources/dwa-a138-lfu-regenwasser-bayern]] (Primärquelle, DWA-A138 / LfU Bayern) |
| ΔLST pro 1 % Entsiegelung | −0,03 °C | [[wiki/sources/tervooren-2015-gruenvolumen-potsdam]] |

> [!warning] Der LST-Koeffizient `LST_PER_PCT_UNSEALING` (−0,03 °C/%) existiert zwar in
> `simulation_params.py`, wird im Endpoint v1 aber **bewusst nicht angewendet**: Der
> Tervooren-Wert ist auf Stadtbezirksebene kalibriert und nicht für Einzelflächen gültig.
> Die Wasser-Simulation liefert daher **kein** `delta_lst_celsius`. Falls v2 eine
> Entsiegelungs-Temperaturwirkung ergänzt, muss diese auf Bezugsgebiets-Ebene erfolgen.

### Inputs

```
area_m2:       float  — Zu entsiegelnde Fläche (> 0)
from_surface:  str    — Ausgangsbelag (Default "asphalt")
to_surface:    str    — Zielbelag    (Default "schotterrasen")
```
Unbekannte Belagstypen (nicht in `RUNOFF_COEFFICIENTS`) → HTTP 422.

### Berechnung (Rational-Formel, nur Versickerung)

```
C_from   = RUNOFF_COEFFICIENTS[from_surface]   # z.B. 0.90 für Asphalt
C_to     = RUNOFF_COEFFICIENTS[to_surface]     # z.B. 0.30 für Schotterrasen
delta_C  = C_from - C_to                        # Abflussbeiwert-Differenz

infiltration_m3_year = max(0, area_m2 × ANNUAL_RAINFALL_WUERZBURG_M × delta_C)
retention_pct        = (1 − C_to) × 100
context_persons      = infiltration_m3_year / CONTEXT_PERSONS_M3_PER_YEAR   # 46,4 m³ (BDEW 2023, 127 L/Tag)
```
`max(0, …)` kappt den Fall, dass der Zielbelag stärker versiegelt ist als der Ausgangsbelag
(`delta_C ≤ 0`) — dann wird zusätzlich ein Caveat vorangestellt.

**Beispiel:** 1.000 m² Asphalt → Schotterrasen:
```
delta_C      = 0.90 − 0.30 = 0.60
infiltration = 1000 × 0.5735 × 0.60 = 344,1 m³/Jahr
```

### Output (JSON)

```json
{
  "area_m2": 1000,
  "from_surface": "asphalt",
  "to_surface": "schotterrasen",
  "infiltration_m3_year": 344.1,
  "retention_pct": 70.0,
  "context_persons": 7.4,
  "runoff_coefficients": { "from": 0.9, "to": 0.3, "delta": 0.6 },
  "rainfall_m_year": 0.5735,
  "caveats": [
    "Abflussbeiwerte nach Leitfaden Landkreis Bayreuth 2024 — Literaturwerte, nicht vor Ort gemessen.",
    "Niederschlag: DWD Station Würzburg (573,5 mm/Jahr, Referenzperiode 1991–2020).",
    "Kein Δ°C in v1 — Tervooren-Koeffizient gilt auf Stadtbezirksebene, nicht für Einzelflächen.",
    "Versiegelungsgrade sind Literaturwerte (v1); v2 (TODO): gemessene Per-Zellen-Versiegelung."
  ]
}
```

### Bekannte Einschränkungen

- **Kein `delta_lst_celsius` in v1** — der Tervooren-Koeffizient gilt auf Stadtbezirks-, nicht auf Einzelflächenebene (Begründung + v2-Ansatz unten).
- Rational-Formel nimmt homogene Bodendurchlässigkeit an; lokale Bodenart (LfU Bayern, kf-Werte aus DWA-A138) würde Präzision erhöhen.
- Asphalt-Abflussbeiwert: `simulation_params.py` verwendet Ψ = 0,90 im Einklang mit DWA-A138 (Primärquelle); der frühere Wert 0,95 aus dem Leitfaden Bayreuth wurde angeglichen.
- Große Entsiegelungsflächen lösen evtl. einen Verdunstungskühleffekt aus (Schwammstadt-Prinzip); dieser ist in v1 **nicht** quantifiziert (kein Δ°C — siehe unten).

### Warum die Entsiegelung in v1 kein Δ°C liefert — und wie v2 es ergänzen würde

Der Koeffizient `LST_PER_PCT_UNSEALING = −0,03 °C/%` (Tervooren 2015, Potsdam) ist in
`simulation_params.py` hinterlegt, wird im Endpoint aber **bewusst nicht angewendet**.

**Wie er gedacht war.** Tervooren misst, dass die mittlere Oberflächentemperatur um
etwa −0,03 °C je Prozentpunkt **Entsiegelung** sinkt — relativ zur Gesamtfläche eines
Bezugsgebiets. Die geplante Rechnung hätte einen dritten Parameter `reference_m2`
(z. B. die Fläche eines Stadtbezirks) gebraucht:

```
unsealing_pct     = entsiegelte_fläche / reference_m2 × 100
delta_lst_celsius = −0,03 × unsealing_pct
```

Der Effekt ist also **relativ**: 1.000 m² Asphalt aufzureißen senkt die mittlere
Temperatur eines ganzen Bezirks praktisch nicht, auf einem kleinen Hof dagegen spürbar.

**Warum v1 darauf verzichtet.** Der Koeffizient ist auf **Aggregatebene** kalibriert
(Grünvolumen vs. mittlere LST über große Flächen). Auf eine einzelne ausgewählte
Polygonfläche angewendet, liefert er physikalisch unsinnige Mikro-Werte (z. B. −0,006 °C),
die eine Genauigkeit vortäuschen, die die Datengrundlage nicht hergibt. Die
Wasser-Simulation gibt deshalb in v1 ausschließlich den flächenscharf berechenbaren
Wassernutzen aus (Versickerung via Rational-Formel) und **kein** Δ°C.

**v2-Ansatz.** Die Temperaturwirkung der Entsiegelung sollte **nicht pro Polygon**,
sondern auf **Bezugsgebiets-Ebene** berechnet und ausgewiesen werden — also als KPI der
Form „Δ°C für diesen Stadtbezirk bei X % Gesamtentsiegelung" statt als Wert pro
ausgewählter Einzelfläche. Erst dann ist die Kalibrierungs-Ebene des Koeffizienten
gewahrt.

---

## Vergleich der beiden Simulationen

| | Baumpflanzung | Entsiegelung |
|---|---|---|
| LST-Koeffizient | −0,083 °C/% (Mischgebiet, **angewendet**) | −0,030 °C/% (vorhanden, **in v1 nicht angewendet** — nur Stadtbezirksebene) |
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
4. **Entsiegelungs-Δ°C auf Bezugsgebiets-Ebene**: Den vorhandenen `LST_PER_PCT_UNSEALING` (−0,03 °C/%) als Stadtbezirks-KPI ausweisen statt pro Polygon (siehe „Warum die Entsiegelung in v1 kein Δ°C liefert" in Simulation B).
5. **Physikalische Simulation**: ENVI-met oder WRF für Blockmaßstab — wenn statistische Simulation zu grob.

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
