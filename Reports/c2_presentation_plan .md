# Component 2: Presentation Master Plan — MSc Academic Defense (Revised)

**Total Slides: 11** | **Allocated Time: 4 Minutes** | **Pace: ~22 seconds per slide**

**MSc Presenter Rule:** Your slides carry the academic weight (equations, methodology names, standard references). Your voice carries the story. Never read bullet points — explain the *why* behind each point.

---

## SLIDE STRUCTURE OVERVIEW

| Slide | Section | Title |
|---|---|---|
| 1 | Opening | Title, Researcher, Core Novelties |
| 2 | Background | The Developing Grid Crisis |
| 3 | Research Gaps | Gap in Current Literature |
| 4 | Research Question + Objectives | Unified Research Question & 6 Objectives |
| 5 | System Overview | Component 2: End-to-End System Architecture |
| 6 | Methodology — GIS | Spatial Typology Framework & OSM Mapping |
| 7 | Methodology — Survey | Primary Data Collection & Ethical Clearance |
| 8 | Methodology — Simulation | Monte Carlo Simulation & Bottom-Up Spatial Scaling |
| 9 | Methodology — AI | Context-Aware N-BEATSx Forecasting |
| 10 | Validation & Output | Validation Protocol & Final System Output |
| 11 | Backup | Sensitivity Analysis & Limitations |

---

## SLIDE DESIGN STANDARD (Applies to Slides 2–11)

> **Component Header Rule:** Every slide from Slide 2 onwards must display the following component identifier as a small label in the **top-left corner** of every slide:
>
> `Component 2: 24-Hour EV Charging Demand Profiling & Forecasting`
>
> Use a small font (10–12pt), muted colour (e.g., grey or your theme's secondary colour), so it does not compete with the slide title but is always visible to the panel.

---

## DETAILED SLIDE PLANS

---

### Slide 1 — Title & Core Novelties
**Title:** Component 2: 24-Hour EV Charging Demand Profile Generation & Forecasting for Sri Lanka (2026–2035)

**Visual:** Dark academic theme. Researcher name (top left). University logo (top right). One highlighted novelty box centered at the bottom.

**Slide Text — Core Research Novelty:**
- **Novel Contribution:** A framework that forecasts temporal 24-hour EV demand by land-use typology—not just charger siting—using survey-parameterized Monte Carlo simulation and interpretable N-BEATSx, without historical data.


**Speaker Notes:** *"My component addresses the fundamental data problem in Sri Lanka — we have zero historical EV charging data. My core novelty is that I forecast temporal, 24-hour demand curves stratified by functional land-use typology — not just where to place chargers, which is what existing GIS-based EV studies do. I bridge three domains: geospatial land-use modeling using OSM, primary survey-parameterized Monte Carlo simulation, and interpretable deep learning using N-BEATSx. Together, these produce a district-level EV grid demand forecast for Sri Lanka without requiring any historical smart-meter data."*

---

### Slide 2 — Introduction & Background
**Title:** The Developing Grid Crisis: Why Sri Lanka Cannot Use Existing Models

**Visual:** Left — photograph of a CEB substation or power line (or a stylized map of Sri Lanka). Right — three bullet problem statements.

**Slide Text:**
- **The Global Problem:** Unmanaged EV charging causes distribution transformer overloading (IEA, 2023)
- **Sri Lankan Constraint 1 — No Data:** Western Deep Learning models require years of historical smart-meter data which Sri Lanka does not have
- **Sri Lankan Constraint 2 — Infrastructure Gap:** CEB Time-of-Use (TOU) tariff shifting requires a 3-Phase domestic electricity connection. Only a fraction of Sri Lankan homes have this — existing models completely ignore this constraint
- **Sri Lankan Constraint 3 — Fleet Composition:** Sri Lanka's EV fleet is dominated by passively air-cooled Nissan Leafs (hot-climate accelerated battery degradation). Western models assume liquid-cooled batteries

**Speaker Notes:** *"The Sri Lankan grid context is unique in three ways. First, we have no historical data. Second, our TOU metering infrastructure is far behind Western grids. Third, our most common EV — the Nissan Leaf — degrades far faster in tropical heat. Any model that ignores these three constraints will produce dangerous over-estimates of grid load."*

---

### Slide 3 — Research Gaps
**Title:** Theoretical Gaps in Current Literature

**Visual:** Two-panel layout (matching the academic standard format):
- **Left panel:** Short description of each existing approach (3 lines each, small font, with label bold)
- **Right panel:** Feature matrix — approaches as columns, capability criteria as rows, ✓/✗ in cells

**Slide Text — Left Panel (Approach Descriptions):**

**Research A**
Prakobkaew & Sirisumrannukul (2022) — Energies 15(11)
Thailand — grid-based GIS estimation of EV counts and public chargers for country-level planning.

**Research B**
Yang et al. (2025) — Scientific Reports 15:4022
China — Monte Carlo spatio-temporal charging load prediction across four functional urban areas.

**Research C**
Sanami et al. (2025) — arXiv:2502.16365
California — LSTM-attention 24-hour charging demand forecast with post-hoc SHAP explainability.

**Gap:** no existing study forecasts typology-stratified, temporal demand from primary survey data without historical smart-meter records.

**Slide Text — Right Panel (Feature Matrix):**

| Capability | Prakobkaew 2022 | Yang 2025 | Sanami 2025 | **Proposed System** |
|---|---|---|---|---|
| 24-hour temporal profiling | ✗ | ✓ | ✓ | ✓ |
| Typology / functional-area split | — (partial) | ✓ | ✗ | ✓ |
| No historical smart-meter data needed | ✓ | ✗ | ✗ | ✓ |
| Primary survey-parameterized | ✗ | — (partial) | ✗ | ✓ |
| Architecturally interpretable AI | ✗ | ✗ | — (partial) | ✓ |

**Speaker Notes:** *"I compare my research against three highly relevant, very recent papers. Research A is the closest developing-nation precedent from Thailand, which uses GIS but only estimates static EV counts, lacking temporal profiling. Research B, published just this year, uses Monte Carlo for spatio-temporal loads across urban areas, but they still rely on massive Chinese smart-meter historical data, which we don't have. Research C, also a 2025 paper from California, does 24-hour forecasting using LSTM, but their interpretability is only 'partial' because they use post-hoc SHAP on a black-box model, whereas N-BEATSx is natively interpretable. Crucially, as the matrix shows, no existing study—not even the latest 2025 papers—can forecast typology-stratified temporal demand from primary surveys without historical smart-meter records. That is the exact gap my proposed system fills."*

---

### Slide 4 — Research Question & Objectives
**Title:** Research Objective & Sub-Objectives

**Visual:** Three-tier visual hierarchy. Top band = Research Question (highlighted). Middle band = Main Objective (bold box). Bottom band = 6 sub-objectives in a numbered two-column grid.

**Research Question (large highlighted box at top):**
> *"How do 24-hour EV charging demand profiles, stratified by functional place typology, evolve in shape and magnitude across Sri Lanka's 25 districts from 2026 to 2035 under different EV penetration scenarios?"*

**Main Objective:**
> Develop a **reproducible, data-scarce EV charging demand forecasting framework** that generates accurate 24-hour district-level load profiles and long-term grid demand forecasts for Sri Lanka without relying on historical smart-meter data.

**Sub-Objectives:**
- **SO1 — Spatial Mapping:** Compute district-level typology weights using OSM land-use density data.
- **SO2 — Primary Data:** Collect behavioral charging parameters from 160–200 Sri Lankan EV owners via survey.
- **SO3 — Stochastic Simulation:** Build a Monte Carlo engine to generate 3,000 synthetic 24-hour demand profiles (2026–2035).
- **SO4 — Interpretable Forecasting:** Train N-BEATSx to forecast district-level demand evolution for 2032–2035.
- **SO5 — Multi-Tier Validation:** Validate profiles against CEB feeder data and SLTDA tourist statistics.
- **SO6 — Sensitivity Analysis:** Identify behavioral parameters most influential on peak grid demand.

**Speaker Notes:** *"My main objective is to build a reproducible forecasting framework that works without historical data — a core challenge in developing nations like Sri Lanka. To achieve this, I have six measurable sub-objectives. SO1 through SO3 build the data pipeline: GIS mapping, primary survey, and Monte Carlo simulation. SO4 adds the forecasting intelligence via N-BEATSx. SO5 and SO6 provide rigorous scientific validation and parameter sensitivity testing. Every sub-objective has a measurable, verifiable output."*

---

### Slide 5 — System Architecture (CRITICAL — Show Early)
**Title:** Component 2: End-to-End System Architecture

**Visual:** A clean left-to-right flowchart with 3 color-coded phases:
- **Phase 1 (Blue — Inputs):** Two stacked boxes: `Primary Survey (160-200 EV Owners)` + `OSM GIS & DMT Fleet Data`
- **Phase 2 (Green — Synthesis):** `Vectorized Monte Carlo Engine` → `3,000 Synthetic District Curves (2026–2035)`
- **Phase 3 (Purple — Forecasting):** `Gaussian Data Augmentation` → `Context-Aware N-BEATSx` → `2032–2035 Trend + Seasonality Forecasts`
- **Output (Orange):** `Proposed Decision-Support Tool (Grid Pulse EV) → CEB Planning Directorate`

All phases connected by bold arrows. Label each arrow with what is being transferred.

**Slide Text:** Keep minimal — let the diagram speak.
- Training split: **2026–2031** (synthetic "past") → **2032–2035** (AI forecast)
- 25 Districts × 4 Typologies × 3 Scenarios × 10 Years = **3,000 simulation runs**

**Speaker Notes:** *"Before diving into the methodology, let me show you the complete system. On the left, two data sources feed the engine: our primary survey and open-source GIS data. The Monte Carlo engine in the center generates a synthetic 10-year dataset. The right side is the AI — N-BEATSx is trained on 2026 to 2031, then forecasts 2032 to 2035. The final output is a web dashboard usable directly by CEB engineers."*

---

### Slide 6 — Spatial Typology Framework & OSM Mapping
**Title:** Spatial Typology Framework: Behavioral Spectrum + GIS Automation

**Visual:** A 2×2 matrix. X-axis: Short Dwell ↔ Long Dwell. Y-axis: Low Power ↔ High Power. Four quadrants each labeled with a typology.

**Slide Text:**
| Typology | Dwell Time | Core Behaviour | Arrival Distribution | OSM Tag |
|---|---|---|---|---|
| T1 — Urban Commercial | Medium (office hours) | Workplace / midday charging | Normal (office hours pattern) | `landuse=commercial` |
| T2 — Suburban Residential | Long (overnight) | Home charging + TOU tariff shift | Normal (late evening peak) | `landuse=residential` |
| T3 — Tourist Destination | Variable (9am–5pm) | Inter-district, low SoC arrival | Uniform (daytime window) | `tourism=*`, POI count |
| T4 — Highway Transit | Ultra-short (en-route) | En-route top-up, bimodal flow | Gaussian Mixture (morning + evening peaks) | `highway=trunk/primary` |

- **Academic Justification:** Typologies cover 100% of the behavioral spectrum by dwell-time pattern, derived from land-use planning theory. Charger type and power are **survey-derived** (Q4), not assumed.
- **OSM Weighting:** Land-use density per typology is normalized per district using GeoPandas to produce typology composition weights.

**Speaker Notes:** *"I designed these 4 typologies based on land-use planning theory — each one captures a distinct dwell-time pattern: medium for offices, long overnight for residential, variable for tourism, and ultra-short en-route for highways. I specifically did not pre-define charger types for these typologies — the actual charger mix used in each typology is empirically derived from the survey. The second key design principle is that every typology maps to a specific OpenStreetMap land-use tag, allowing GeoPandas to automatically compute its spatial weight in every district."*

---

### Slide 7 — Primary Data Collection & Ethical Clearance
**Title:** Primary Data Collection: Survey Design, Sample Size & Ethics

**Visual:** Left — large QR Code to Google Form. Right — parameter-to-distribution mapping table.

**Slide Text (Left Column):**
- **Objective:** Collect primary behavioral charging data to parameterize the Monte Carlo simulation engine.
- **Sampling Strategy:** 
  - Stratified Purposive Sampling (by Typology) 
  - Snowball Sampling (for hard-to-reach EV owners)
- **Ethical Clearance:** Fully anonymized survey. No Personally Identifiable Information (PII) collected.

**Visual (Bottom Left):** Small QR Code to Google Form

**Slide Text (Right Column):**
**Key Behavioral Parameters Extracted:**
1. **Trip distance** (`d_trip`)
2. **State of Charge (SoC) at plug-in** (`SoC_arr`)
3. **Arrival time** (`t_arr`)
4. **Charger type/power** (`c_type`, `c_kW`)
5. **Session frequency** (`λ`)
6. **Time-of-Use (TOU) shift probability** (`p_3phase`)

**Speaker Notes:** *"Because Sri Lanka has no historical smart-meter data, this primary survey is the foundation of the entire simulation. The objective is to collect real behavioral parameters from Sri Lankan EV owners. Because there is no centralized EV registry, I am using Stratified Purposive and Snowball sampling to reach respondents across the four typologies. The survey extracts six key parameters, including trip distance, arrival time, and SoC at plug-in. Crucially, all data is fully anonymized with absolutely no PII collected."*

---

### Slide 8 — Methodology: Overcoming Data Scarcity
**Title:** Methodology: Simulation & Forecasting Pipeline

**Visual:** Two-step flowchart: `[1. Monte Carlo Simulator: Generate Data]` → `[2. N-BEATSx Deep Learning: Forecast Trends]`

**Slide Text:**
- **Phase 1: Generating the Missing Data (Monte Carlo)**
  - **The Purpose:** Sri Lanka has no real-world smart-meter data. We use Monte Carlo simulation to stochastically generate thousands of realistic 24-hour daily charging profiles.
  - **The Result:** Captures human behavioral uncertainty (creating Best, Median, and Worst-case scenarios) without needing physical sensor data.
- **Phase 2: Forecasting Long-Term Growth (N-BEATSx)**
  - **The Purpose:** Train an AI model on the simulated baseline data (2026–2031) to predict how grid demand will evolve up to 2035.
  - **The Result:** Uses an architecturally *interpretable* model that gives CEB engineers two explainable curves: **Trend** (annual growth) and **Seasonality** (daily peak shifts).

**Speaker Notes:** *"This slide shows how I overcome Sri Lanka's data scarcity in two distinct phases. Phase 1 is the Monte Carlo Simulator. The purpose of this tool is to mathematically generate a synthetic baseline dataset. It simulates thousands of charging sessions based on our primary survey to build realistic 24-hour demand curves. Phase 2 is the Forecasting engine. Once we have simulated the baseline data for 2026 to 2031, we train a deep learning model called N-BEATSx to forecast the long-term evolution from 2032 to 2035. I chose N-BEATSx specifically because it is an interpretable model—it doesn't just give the CEB a black-box number, it gives them a clear Trend curve showing year-on-year growth, and a Seasonality curve showing how the evening peak shifts. That is the core purpose of this pipeline: generating realistic baseline data, then predicting explainable future trends."*

---

### Slide 9 — Two-Tier Validation Strategy & Final Output
**Title:** Two-Tier Validation Protocol & Final Research Output

**Visual:** A split screen. Left: Validation flow (Tier 1 + Tier 2). Right: Large, clear screenshot of the *Grid Pulse EV* dashboard.

**Slide Text:**
- **Tier 1: AI Mathematical Validation (N-BEATSx)**
  - **Method:** Hold-Out Testing. The AI is trained on 2026–2031, but evaluated on hidden 2032–2035 data.
  - **Metrics:** RMSE (curve accuracy) and MAPE (peak magnitude accuracy).
- **Tier 2: Simulation Logic Validation (Monte Carlo)**
  - *How do we validate EV profiles without historical EV data?*
  - **Physics-Bound Checks:** Simulated energy strictly checked against survey-derived Vehicle Kilometers Traveled (VKT) physical limits.
  - **Expert Face Validity:** Final simulated district profiles are reviewed and endorsed by CEB planning engineers.
- **The Final Output: Grid Pulse EV Dashboard**
  - A web-based decision support tool for CEB engineers to instantly visualize EV grid impact, peak hours, and load growth up to 2035.
  - **Live Demo:** [https://grid-pulse-ev.vercel.app/](https://grid-pulse-ev.vercel.app/)

**Speaker Notes:** *"Validating this system was the biggest challenge due to data scarcity. I use a two-tier strategy. Tier 1 is purely mathematical: the N-BEATSx AI is tested against a hidden 2032-2035 hold-out set to prove its predictive accuracy using RMSE and MAPE. Tier 2 validates the Monte Carlo simulation itself. Because we don't have historical data, we use strict physics-bound checks: total simulated energy is constrained by real driving distances from our survey, ensuring no generated profile is physically impossible. Furthermore, the generated profiles are subject to expert face validity reviews by CEB planning engineers. Finally, all of this complex math is packaged into a web app called the Grid Pulse EV Dashboard. A live demo is available at the link on screen, giving utility planners a simple, click-and-play decision support tool."*

---

### Slide 10 — Backup: Sensitivity Analysis & Limitations
**Title:** Sensitivity Analysis & Honest Limitations

**Visual:** Two-column card layout — left = sensitivity, right = limitations.

**Slide Text:**
- **Sensitivity Analysis (O6):** Testing parameter ranges to identify most influential inputs:

| Parameter | Tested Range | Impact Measured |
|---|---|---|
| TOU shift probability | ±30% | Residential overnight peak kW |
| Nissan Leaf degradation rate | 2.0–4.5%/yr | SoC arrival distribution |
| Tourist party size | 2.0–4.0 persons/vehicle | T3 district EV count |
| Monte Carlo N iterations | 0.5N* to 1.5N* | Coefficient of variation of peak |

- **Limitations & Mitigations:**
  - Survey may over-represent early adopters → Two-phase design (mainstream correction for 2028–2035)
  - OSM coverage sparse in rural districts → Supplement with Geofabrik extract + Sentinel-2 land cover
  - N-BEATSx may not outperform ARIMA → Planned comparison, result reported honestly regardless of outcome
  - Component 1 projections carry uncertainty → Propagated through Low/Medium/High scenarios

**Speaker Notes:** *"Finally, I want to be transparent about limitations — which is a marker of rigorous academic work. My sensitivity analysis formally tests how sensitive the model's outputs are to each uncertain parameter. And my limitations section honestly states that if N-BEATSx does not beat the ARIMA baseline, the result will be reported truthfully. The science is the priority, not the outcome."*

---

## PRESENTATION DELIVERY GUIDE

| Section | Slides | Target Time |
|---|---|---|
| Opening + Background | 1–2 | ~45 sec |
| Gaps + Objectives | 3–4 | ~40 sec |
| System Architecture | 5 | ~20 sec |
| Methodology (GIS + Survey + MC + AI) | 6–9 | ~90 sec |
| Validation + Output | 10 | ~20 sec |
| **Total** | **10 slides** | **~3:55 min** |
| Backup (Sensitivity) | 11 | Q&A only |

> **Key Principle (MSc Level):** Every claim on every slide must be backed by either a named statistical distribution, a named academic standard, a named external data source, or a named algorithm. Vague statements like "we use machine learning" are not acceptable at this level.

---

## APPENDIX — PANEL Q&A CITATION REFERENCE (Not a counted slide)

Keep this list on hand for oral defense. Verify exact bibliographic details (author order, page numbers) before printing any of these on a References slide — titles, venues, and years below are confirmed; full author lists for items 4–5 should be double-checked against the source page.

**N-BEATS(x) / interpretability**
1. Oreshkin, B. N., Carpov, D., Chapados, N., & Bengio, Y. (2020). *N-BEATS: Neural basis expansion analysis for interpretable time series forecasting.* ICLR 2020.
2. Olivares, K. G., Challu, C., Marcjasz, G., Weron, R., & Dubrawski, A. (2021). *Neural basis expansion analysis with exogenous variables: Forecasting electricity prices with NBEATSx.*
3. Kasprzyk, M., Pełka, P., Oreshkin, B. N., & Dudek, G. (2024/2025). *Enhanced N-BEATS for mid-term electricity demand forecasting.* (arXiv:2412.02722) — secondary support for the interpretability-trend framing.

**Monte Carlo synthetic data for EV load**
4. Ni, X., & Lo, K. L. (2020). *A methodology to model daily charging load in the EV charging stations based on Monte Carlo simulation.* ICSGCE 2020.
5. Xie, T., Zhang, Y., Zhang, G., Zhang, K., Li, H., & He, X. (2024). *Research on electric vehicle load forecasting considering regional special event characteristics.* Frontiers in Energy Research, 12:1341246.

**GIS / land-use spatial demand (key comparator)**
6. Prakobkaew, P., & Sirisumrannukul, S. (2022). *Practical Grid-Based Spatial Estimation of Number of Electric Vehicles and Public Chargers for Country-Level Planning with Utilization of GIS Data.* Energies, 15(11), 3859. — the Thailand study; cite by name when asked "why is this different from existing GIS EV work?"

**CEB / TOU policy context**
7. Daily FT / PUCSL (2017, May 5). *Single phase domestic customers to get time of use tariff.* — confirms CEB extended TOU tariffs to single-phase domestic customers specifically due to rising EV fleet and evening-peak concern. Use as policy-context grounding for the TOU/3-phase novelty, not as an academic literature citation — no peer-reviewed study was found that empirically measures this shift for Sri Lanka, which is precisely the gap this component fills.

**If asked "why not LSTM":** Do not claim grid engineers or CEB "refuse" to use black-box models — no source supports that specific claim. Instead: "2024–2025 literature increasingly raises interpretability concerns about deep-learning load forecasters; N-BEATSx addresses this architecturally rather than requiring a post-hoc explainability layer."
