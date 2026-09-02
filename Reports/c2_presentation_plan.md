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
- **Novel Contribution:** A reproducible end-to-end framework combining geospatial land-use modeling, primary survey-derived stochastic simulation, and interpretable deep learning to generate and forecast district-level EV charging demand profiles in the absence of historical charging data.

**Speaker Notes:** *"My component addresses the fundamental data problem in Sri Lanka — we have zero historical EV charging data. My single core novelty is an end-to-end reproducible framework that bridges three domains: geospatial land-use modeling using OSM, primary stochastic simulation using Monte Carlo, and interpretable deep learning using N-BEATSx. Together, these three produce the first district-level EV grid demand forecast for Sri Lanka without requiring any historical smart-meter data."*

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

**Approach A** — Agent-Based Modeling (ABM)
Simulates individual EV driver agents with detailed behavioral rules and survey-derived parameters. Captures micro-level user decisions but lacks functional land-use spatial decomposition and long-term demand forecasting capability.

**Approach B** — Stochastic Monte Carlo Simulation
Samples probabilistic distributions to generate demand profiles. Operates without historical data and some studies use generic surveys, but parameters are not stratified by functional land-use typology across all districts. No interpretable forecasting layer.

**Approach C** — GIS-Integrated Spatial Planning Models
Combines geographic land-use and infrastructure data to map charging demand spatially. Provides district-level spatial coverage but depends on secondary spatial datasets and cannot produce interpretable temporal demand forecasts.

**Gap:** No existing approach simultaneously achieves all four capabilities required for district-level EV grid planning in a data-scarce developing-nation context.

**Slide Text — Right Panel (Feature Matrix):**

| Capability | Approach A (ABM) | Approach B (MC Simulation) | Approach C (GIS-Spatial) | **Proposed System** |
|---|---|---|---|---|
| Functional Land-Use Typology Spatial Profiling | ✗ | ✗ | Partial (infrastructure siting only) | ✓ (25 districts × 4 typologies) |
| Primary Behavioral Survey Data | ✓ | Partial (not country-specific) | ✗ | ✓ (160–200 Sri Lankan EV owners) |
| Data-Scarce Operation | ✓ | ✓ | ✓ | ✓ |
| Interpretable Demand Forecasting | ✗ | ✗ | ✗ | ✓ (N-BEATSx Trend + Seasonality) |

**Speaker Notes:** *"I compare my research against three real methodological categories from current literature. Approach A — Agent-Based Modeling — does use behavioral surveys and operates without historical data, but it cannot decompose demand by functional land-use typology across 25 districts, and it has no forecasting capability. Approach B — Monte Carlo simulation — is also data-scarce capable, but existing studies use generic parameters not stratified by country-specific functional typologies. Approach C — GIS spatial planning — maps space well, but uses secondary data and cannot forecast demand evolution. Notice that only the Proposed System satisfies all four capabilities simultaneously. The critical gap is the combination of typology-based spatial profiling with interpretable deep learning forecasting — no existing approach achieves both."*

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

**Slide Text:**
- **Sampling Methodology:** Stratified Purposive Sampling (by Typology) + Snowball Sampling (for hard-to-reach EV owners — justified: no centralized EV registry exists in Sri Lanka)
- **Statistical Justification:** Cochran's Formula for finite population (N=8,655 registered EVs) → minimum n=95 required at 95% confidence. Target: **160–200 respondents** (margin of error ~7%)
- **Key Parameters Extracted:**

| Survey Q | Behavioral Variable | Proposed Distribution Model (Literature-Based) |
|---|---|---|
| Trip distance | `d_trip` | LogNormal — trip distances are right-skewed continuous |
| SoC at plug-in | `SoC_arr` | Beta — bounded variable [0, 1] |
| Arrival time | `t_arr` | Normal or Gaussian Mixture — unimodal or bimodal by typology |
| Charger type | `c_type` | Multinomial — discrete multi-category choice |
| 3-Phase meter | `p_3phase` | Bernoulli — binary yes/no infrastructure status |
| Session frequency | `λ` | Poisson — count of sessions per week |

> **Note:** Distribution families are theoretically selected based on variable properties and published EV demand literature. Actual parameters (μ, σ, α, β, λ) will be estimated from survey responses using Maximum Likelihood Estimation (MLE) post data collection.

- **Ethical Clearance:** Respondent ID only (no name/address). Full anonymization. No PII stored. Preamble read to all respondents.

**Speaker Notes:** *"Because no historical data exists, this survey is the foundation of the entire simulation. Using Cochran's formula, I need only 95 respondents for 95% confidence from Sri Lanka's 8,655 EV fleet — I target 160 to 200 for rigor. The table shows the distribution model I have theoretically proposed for each variable, based on the statistical properties of that variable and published EV charging literature. For example, trip distance is always right-skewed and bounded at zero, which makes LogNormal the theoretically correct family. SoC at arrival is bounded between 0 and 1, making Beta the correct family. These are prior choices — after the survey is completed, I will use Maximum Likelihood Estimation to fit the actual parameters from the collected responses. All data is fully anonymized with absolutely no PII collected."*

---

### Slide 8 — Monte Carlo Simulation & Bottom-Up Spatial Scaling
**Title:** Monte Carlo Engine & Bottom-Up Spatial Scaling (Spatial Micro-Simulation)

**Visual:** Three-step flow diagram: `[Survey Shape]` × `[OSM Weights + DMT Fleet]` = `[25 District Curves (MW)]`

**Slide Text:**
- **Core Methodology: Bottom-Up Spatial Scaling (Spatial Micro-Simulation)**
  - **Step 1 — The Shape:** Survey data → 4 normalized typology probability curves (one per typology, representing behavioral patterns)
  - **Step 2 — The Scale:** District fleet size (from Component 1) is weighted by OSM land-use density per typology per district
  - **Step 3 — Generation:** Typology Shape × District Fleet × OSM Weight → **25 unique district demand profiles in MW**
- **Why Monte Carlo?** To stochastically simulate thousands of individual EV sessions per district using six behavioural and physical inputs (survey-derived + literature-derived) — outputs the P05, P50, P95 uncertainty envelopes per district
- **Computational Scale:** Convergence Test ($N^*$) → **3,000 simulation runs** (10yr × 25 districts × 4 typologies × 3 scenarios)

**Speaker Notes:** *"The headline innovation of this slide is Bottom-Up Spatial Scaling. The survey gives us the behavioral shape of each typology's demand curve. We then scale that shape by the actual fleet size in each district, weighted by the OSM GIS density. This mathematically generates 25 unique district curves without surveying all 25 districts. The Monte Carlo engine runs this process stochastically thousands of times across six behavioural and physical inputs to output three uncertainty bands — low, median, and high — for every district."*

---

### Slide 9 — Context-Aware N-BEATSx Forecasting
**Title:** Interpretable Deep Learning: Context-Aware N-BEATSx Architecture

**Visual:** Flowchart — `[Synthetic District Profiles]` → `[Gaussian Augmentation]` → `[N-BEATSx: Trend Block + Seasonality Block]` → `[Trend Curve + Seasonality Curve]`

**Slide Text:**
- **Why N-BEATSx?** Its architecture is structurally interpretable — it mathematically decomposes the forecast output into two separate, explainable components, making it directly suitable for grid engineering planning decisions.
- **Training Split:**
  - **Train:** 2026–2031 (6 years × 25 districts = 150 synthetic profiles) — augmented via Gaussian noise and time-jittering to expand training sequences
  - **Test (Hold-Out):** 2032–2035 — held out completely, never seen by the model during training
- **Context Inputs (Exogenous Variables):** District ID (categorical), Typology (categorical), Fleet Size (numerical)
- **Outputs:** `Trend Curve` — Year-on-Year grid demand growth | `Seasonality Curve` — shifting daily peak shape
- **Baseline Comparison:** N-BEATSx performance compared against a statistical baseline model — result reported honestly regardless of outcome

**Speaker Notes:** *"N-BEATSx is selected because its architecture is structurally interpretable — it mathematically separates the forecast into a Trend block and a Seasonality block, giving CEB engineers an explainable output they can use directly for grid planning. I train the model on 2026-to-2031 synthetic profiles, with data augmentation applied to expand training sequences and prevent overfitting. The model is tested on the completely hidden 2032-to-2035 hold-out set. The exogenous inputs — district, typology, and fleet size — allow the model to be context-aware across all 25 districts. Performance is compared against a statistical baseline and reported honestly."*

---

### Slide 10 — Validation & Final Output
**Title:** Two-Tier Validation Protocol & Final Research Output

**Visual:** Left column — Tier 1 (AI Validation). Right column — Tier 2 (Simulation Validity). Below both — a screenshot of the Grid Pulse EV dashboard.

**Slide Text:**
- **Tier 1 — AI Model Validation (Mathematical):**
  - Hold-Out Test: N-BEATSx predictions vs. Monte Carlo 2032–2035 ground truth
  - Metrics: RMSE per hour, MAPE on peak demand, Pearson r on curve shape
  - Baseline: Compared against a statistical baseline model — result reported honestly regardless of outcome
- **Tier 2 — Simulation Validity (Physical/Face Validity):**
  - T1 Commercial peak window (10am–2pm) compared against CEB Annual Report commercial feeder data
  - T2 Residential evening peak compared against CEB Statistical Digest residential load factor
  - T3 Tourist seasonal peaks compared against SLTDA monthly arrival statistics
  - T4 Highway bimodal peak compared against published Sri Lanka traffic flow studies
- **Proposed Decision-Support Tool — Grid Pulse EV Dashboard** → CEB Planning Directorate:
  - CEB engineers select: District + Typology + Year → Instant 24-hour demand curve
  - Outputs: Peak Hour, Peak Magnitude (kW), Daily Energy (kWh), P05/P50/P95 probability envelopes
  - Accessible without any programming knowledge

**Speaker Notes:** *"Validation happens on two levels. At the AI level, N-BEATSx is mathematically validated using hold-out testing against ground-truth Monte Carlo curves using RMSE and MAPE. At the simulation level, each typology's demand shape is physically validated against real surrogate data from CEB and SLTDA. The final product is the Grid Pulse EV web dashboard — a fully deployed tool that allows CEB planning engineers to generate instant district-level demand forecasts for any year up to and beyond 2035."*

---

### Slide 11 — Backup: Sensitivity Analysis & Limitations
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
