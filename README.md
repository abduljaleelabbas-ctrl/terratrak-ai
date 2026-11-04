# TerraTrak AI

**A prototype soil workability simulator that shows when it is safe to take machinery onto a field.**

TerraTrak AI is a capstone concept from the Meta AI Academy (October 2026). It helps farm managers and tractor operators decide on field entry using a simple workability index: W = current soil moisture / plastic-limit moisture.

**Live demo:** https://abduljaleelabbas-ctrl.github.io/terratrak-ai/

---

## The Problem

- Driving heavy machinery on soil that is wetter than its plastic limit collapses soil pores, creates hardpans and can cause lasting yield losses.
- Operators face a dilemma: enter too early and damage the soil and equipment, or wait too long and miss the planting or harvesting window.
- Commercial in-field moisture sensors are costly and hard to maintain, so they are out of reach for many cooperatives and tractor-hire operators.

## What It Does Today

- An interactive simulator where you enter soil moisture and plastic-limit moisture and choose heavy or light equipment.
- Soil moisture is entered manually in this prototype. Satellite data is a planned next step.
- A landing page with a link to a waitlist form for people interested in early access.

## How It Works

TerraTrak AI uses a **Workability Index (W)**:

```
W = θ_current / θ_PL
```

- `θ_current`: current surface soil moisture (m³/m³). In the prototype this is typed in; a planned data source is satellite data such as NASA SMAP.
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
| `index.html` | Responsive landing page with an interactive workability simulator and a waitlist link |

The page runs entirely in the browser, so there is nothing to install. To try it locally, download `index.html` and open it in any modern browser.

## Project Components

1. **Workability logic:** the W index and equipment-adjusted decision rules, implemented in the browser simulator.
2. **AI system prompt (design):** built on the RCTCF framework (Role, Context, Task, Constraints, Format) to turn metrics into short, plain-language WhatsApp advisories.
3. **WhatsApp chatbot flow (design):** menu-based dialogue (select field, select equipment, receive advisory). This is a design, not a live service.
4. **Landing page and simulator:** this repository's `index.html`.
5. **Pitch deck:** 5 slides submitted with the capstone (not stored in this repository).

## How It Was Built

The workability logic, thresholds and user experience were designed by me. The HTML, CSS and JavaScript were written with AI-assisted coding, then tested, corrected and deployed by me.

## Limitations

TerraTrak AI should **not** be relied on alone in these situations:

- **Active heavy rainfall:** satellite passes cannot capture fast, intra-day moisture changes.
- **Drainage and tile failures:** coarse satellite data cannot see small-scale mud traps or drainage breaks.
- **Steep slopes (above about 8–10%):** traction depends on shear strength and wheel slip, not moisture alone.
- **Expansive clays (Vertisols) and organic soils:** plastic limit estimates need local ground-truth calibration.

## Roadmap

- **Phase 1 (current prototype):** web simulator, plus the WhatsApp dialogue and AI prompt designs.
- **Phase 2 (planned):** automated daily satellite moisture data (for example via the Google Earth Engine API) and a small farm pilot.
- **Phase 3 (planned):** 3-day predictive soil drying curves using evapotranspiration weather forecasts.

## Business Model (Concept)

- **Cooperative subscriptions:** annual fee based on registered hectares.
- **Pay-per-query credits:** low-cost SMS/WhatsApp credits for independent tractor-hire operators.

## Author

**Abduljaleel Abbas**
Agricultural and Bioresources Engineering, Federal University of Technology, Minna.
Interests: AI and data science for smart and precision agriculture
