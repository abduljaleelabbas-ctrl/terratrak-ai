# TerraTrak AI

**Smart field entry and soil workability advisories, delivered through WhatsApp.**

TerraTrak AI is a hardware-free decision support concept that helps farm managers and tractor operators decide when it is safe to take machinery onto a field. It combines satellite soil moisture data with soil mechanics logic to prevent subsoil compaction, rutting and costly equipment damage, without expensive on-farm sensors.

**Live demo:** https://abduljaleelabbas-ctrl.github.io/terratrak-ai/

*Capstone project, Meta AI Academy (October 2026).*

---

## The Problem

- Driving heavy machinery on soil that is wetter than its plastic limit collapses soil pores, creates hardpans and can cause lasting yield losses.
- Operators face a dilemma: enter too early and damage the soil and equipment, or wait too long and miss the planting or harvesting window.
- Commercial in-field moisture sensors are costly and hard to maintain, so they are out of reach for many cooperatives and tractor-hire operators.

## How It Works

TerraTrak AI uses a **Workability Index (W)**:

```
W = θ_current / θ_PL
```

- `θ_current`: current surface soil moisture (m³/m³), e.g. from satellite data such as NASA SMAP
- `θ_PL`: soil moisture at the plastic limit (m³/m³)

Thresholds depend on equipment weight:

| Workability Index (W) | Heavy machinery (tractors, disc plows, harvesters) | Light machinery (boom sprayers, ATVs) |
|---|---|---|
| W < 0.85 | 🟢 Safe to enter | 🟢 Safe to enter |
| 0.85 ≤ W ≤ 1.00 | 🟡 Marginal entry (delay heavy tillage 24–48 h) | 🟢 Safe to enter |
| 1.00 < W ≤ 1.15 | 🔴 Do not enter | 🟡 Marginal entry (light traffic only) |
| W > 1.15 | 🔴 Do not enter | 🔴 Do not enter |

**Example:** θ_current = 0.28 and θ_PL = 0.25 give W = 1.12. This is 🔴 DO NOT ENTER for heavy equipment and 🟡 MARGINAL for light equipment.

## What's in This Repository

| File | Description |
|---|---|
| `index.html` | Responsive landing page with an interactive workability simulator and a pilot sign-up form |

The page runs entirely in the browser, so there is nothing to install. To try it locally, download `index.html` and open it in any modern browser.

## Project Components

1. **Soil workability engine:** the W index and equipment-adjusted decision logic.
2. **AI system prompt:** built on the RCTCF framework (Role, Context, Task, Constraints, Format) to turn metrics into short, plain-language WhatsApp advisories.
3. **WhatsApp chatbot flow:** menu-based dialogue (select field, select equipment, receive advisory).
4. **Landing page and simulator:** this repository's `index.html`.
5. **Pitch deck:** capstone submission slides.

## Limitations

TerraTrak AI should **not** be relied on alone in these situations:

- **Active heavy rainfall:** satellite passes cannot capture fast, intra-day moisture changes.
- **Drainage and tile failures:** coarse satellite data cannot see small-scale mud traps or drainage breaks.
- **Steep slopes (above about 8–10%):** traction depends on shear strength and wheel slip, not moisture alone.
- **Expansive clays (Vertisols) and organic soils:** plastic limit estimates need local ground-truth calibration.

## Roadmap

- **Phase 1 (current MVP):** workability engine, WhatsApp dialogue script and web simulator.
- **Phase 2 (next 60 days):** Google Earth Engine API integration for automated daily satellite data, and a pilot on 20 farms.
- **Phase 3 (scaling):** 3-day predictive soil drying curves using evapotranspiration weather forecasts.

## Business Model (Concept)

- **Cooperative subscriptions:** annual fee based on registered hectares.
- **Pay-per-query credits:** low-cost SMS/WhatsApp credits for independent tractor-hire operators.

## Author

**Abduljaleel Abbas**
Agricultural and Bioresources Engineering, Federal University of Technology, Minna.
Interests: AI and data science for smart and precision agriculture
