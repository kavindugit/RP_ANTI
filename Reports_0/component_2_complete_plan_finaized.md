# Component 2 — Complete Research Plan
## 24-Hour EV Charging Demand Profile Generation and Forecasting for Sri Lanka (2026–2035)
**Researcher:** Herath H M K M — IT23249684
**Method:** Monte Carlo Simulation + N-BEATSx Deep Learning

---

## 1. Unified Research Question

> *How do the 24-hour EV charging demand profiles, stratified by functional place typology, evolve in shape and magnitude across Sri Lanka's 25 districts from 2025 to 2035 under different EV penetration scenarios?*

---

## 2. Research Objectives

| # | Objective |
|---|---|
| O1 | Compute spatial typology composition weights for each of Sri Lanka's 25 districts using OSM land-use density data (commercial area, residential area, tourism POIs, road length) to enable district-level demand scaling |
| O2 | Collect primary behavioural data from Sri Lankan EV owners via structured interviews to derive typology-specific charging parameters |
| O3 | Build a parameterized Monte Carlo simulation engine to generate annual 24-hour demand profiles for each district × typology × scenario combination (2026–2035) |
| O4 | Train Context-Aware N-BEATSx forecasting models on simulated annual profiles to predict demand evolution for 2032–2035 |
| O5 | Validate simulated profiles against available real-world surrogate data per typology |
| O6 | Conduct sensitivity analysis to identify which behavioural parameters most influence the demand profile output |

---

## 3. Place Typology Framework

| ID | Typology | Representative Locations | Core Behaviour |
|---|---|---|---|
| T1 | Urban Commercial Hub | Colombo Fort, Kandy City, Jaffna Town, Galle City | Workplace/midday charging, moderate SoC arrivals |
| T2 | Suburban Residential Zone | Gampaha, Moratuwa, Nugegoda, Kurunegala | Overnight home charging, TOU tariff shifting |
| T3 | Tourist Destination | Kandy, Nuwara Eliya, Galle, Sigiriya area, Trincomalee | Low SoC inter-district arrivals, fast charge preference |
| T4 | Highway Transit Corridor | Kadawatha, Nelundeniya, Kurunegala junction, Matara bypass | En-route top-up, DC fast charge only, bimodal peak |

---

## 4. Complete Variable Registry

### 4.1 — Input Variables (Per Simulated EV Session)

| Variable | Symbol | Type | Source | Description |
|---|---|---|---|---|
| Vehicle class | `v_class` | Categorical | DMT imports + Interview Q1 | Leaf-24, Leaf-30, BYD-Atto3, MG-ZS, Tuk-tuk, 2-wheeler |
| Nominal battery capacity | `B_nom` | Float (kWh) | From vehicle class | 24, 30, 50, 72, 6, 2 kWh respectively |
| Vehicle age (years) | `age` | Integer | DMT import year records | Used to compute SoH |
| State of Health | `SoH` | Float (0–1) | Degradation model | Fraction of original capacity remaining |
| Effective battery capacity | `B_eff` | Float (kWh) | Derived: `B_nom × SoH` | Actual usable capacity |
| Trip distance before charging | `d_trip` | Float (km) | Interview Q2 | Distance driven since last full charge |
| Energy consumption rate | `e_rate` | Float (kWh/km) | Literature + vehicle class | Avg: Leaf=0.17, BYD=0.19, Tuk-tuk=0.05 |
| Energy consumed on trip | `E_trip` | Float (kWh) | Derived: `d_trip × e_rate` | Battery depleted during trip |
| SoC at previous charge | `SoC_prev` | Float (0–1) | Assumed 0.85 (full charge prior) | Starting point of trip |
| SoC at plug-in arrival | `SoC_arr` | Float (0–1) | Interview Q7 / Derived | Clipped to [0.05, 0.95] |
| Target SoC | `SoC_tgt` | Float (0–1) | Typology-specific | T1=0.80, T2=0.95, T3=0.85, T4=0.80 |
| Energy needed | `E_need` | Float (kWh) | Derived: `max(0, (SoC_tgt − SoC_arr) × B_eff)` | Energy to transfer in this session |
| Charger type | `c_type` | Categorical | Interview Q4 | Slow-13A, Level2-7kW, DCFast-50kW |
| Charger power | `c_kW` | Float (kW) | From charger type | 1.5, 7.2, or 50 kW |
| Session duration | `t_sess` | Float (hours) | Derived: `E_need / c_kW` | Length of charging session |
| Plug-in arrival time | `t_arr` | Float (hour 0–24) | Interview Q5 | When EV is connected to charger |
| Has 3-Phase TOU Meter | `has_3phase` | Boolean | Interview Q8a | Whether home has CEB TOU smart meter installed |
| TOU shift flag | `f_TOU` | Boolean | Interview Q8b (Residential only) | Whether session shifts to off-peak (requires has_3phase=True) |
| Adjusted arrival time | `t_arr_adj` | Float (hour 0–24) | Derived from TOU shift | Final plug-in time after any shifting |
| District | `d` | Integer (1–25) | OSM / Component 1 | Which of 25 districts |
| Typology | `t` | Integer (1–4) | OSM classification | Which typology |
| Year | `y` | Integer (2026–2035) | Simulation loop | Which projection year |
| Scenario | `s` | Categorical | Component 1 | Low / Medium / High EV penetration |

---

### 4.2 — Intermediate Variables (Per Simulation Run)

| Variable | Symbol | Description |
|---|---|---|
| EV count for typology | `N_EVs(d,t,y,s)` | Total EVs = Component1_count × OSM_weight(d,t) |
| Per-session hourly kW contribution | `P_h(session)` | kW drawn during hour h for this session |
| Iteration demand curve | `DC_iter[0..23]` | 24-hour demand array for one Monte Carlo iteration |
| All iterations array | `DC_all[N*, 24]` | Stack of all iteration demand curves |

---

### 4.3 — Output Variables (Per District × Typology × Year × Scenario)

| Variable | Symbol | Description |
|---|---|---|
| Mean 24-hour demand curve | `DC_mean[24]` | Average demand per hour across all N* iterations (kW) |
| 5th percentile curve | `DC_p05[24]` | Best-case (quiet day) demand profile |
| 50th percentile curve | `DC_p50[24]` | Typical demand profile |
| 95th percentile curve | `DC_p95[24]` | Worst-case (peak demand day) profile |
| Peak demand hour | `H_peak` | Hour at which DC_mean is maximum |
| Peak demand magnitude | `P_peak` | Maximum kW in DC_mean |
| Total daily energy | `E_daily` | Sum of DC_mean × 1hr (kWh) |
| Per-EV normalized curve | `DC_norm[24]` | DC_mean ÷ N_EVs — used for LSTM training |

---

### 4.4 — N-BEATSx Model Variables

| Variable | Description |
|---|---|
| Target Series | 6 annual per-EV normalized 24-hour profiles (2026–2031) per typology |
| Static Exogenous Context | District ID (1-25), Typology ID (T1-T4), Fleet Size |
| Training target | Next year's per-EV normalized 24-hour profile |
| Test target | 2032–2035 profiles (held out, generated by Monte Carlo but never seen by AI) |
| Output: Trend | Structural polynomial curve representing year-over-year growth |
| Output: Seasonality | Fourier curve representing the daily 24-hour peak pattern |
| Scaled forecast | (Trend + Seasonality) × N_EVs(d,t,y,s) for each district |

---

## 5. Complete Data Requirements

### 5.1 — Data from Component 1

| Data Item | Format | Description |
|---|---|---|
| District EV count by year and scenario | Table: 25 rows × 10 years × 3 scenarios | Annual projected EV registrations per district for 2026–2035 under Low/Medium/High penetration |

> **Note:** If Component 1 outputs are not yet available, use placeholder growth rates (Low=5%, Medium=12%, High=20% annual from 2026 base count from DMT) until final values are received.

---

### 5.2 — Data from OSM (OpenStreetMap) — Free, No Registration Required

| Data Item | OSM Tag | Extraction Tool | Format | Purpose |
|---|---|---|---|---|
| Commercial land polygons | `landuse=commercial`, `landuse=retail` | OSMnx / GeoPandas | Polygon area km² per district | Commercial typology weight f₁(d) |
| Residential land polygons | `landuse=residential` | OSMnx / GeoPandas | Polygon area km² per district | Residential typology weight f₂(d) |
| Tourism POIs | `tourism=*`, `amenity=hotel`, `amenity=guest_house`, `tourism=attraction` | OSMnx POI query | Count per district | Tourist typology weight f₃(d) |
| Primary/trunk roads | `highway=primary`, `highway=trunk` | OSMnx road network | Total length km per district | Highway typology weight f₄(d) |

**Normalization formula (applied per feature across all 25 districts):**
```
f̂ᵢ(d) = [fᵢ(d) − min(fᵢ)] ÷ [max(fᵢ) − min(fᵢ)]
```

**Typology weight formula:**
```
w(d, T1) = f̂₁(d) / [f̂₁(d) + f̂₂(d) + f̂₃(d) + f̂₄(d)]
w(d, T2) = f̂₂(d) / [same denominator]
w(d, T3) = f̂₃(d) / [same denominator]
w(d, T4) = f̂₄(d) / [same denominator]
```

---

### 5.3 — Data from SLTDA (sltda.gov.lk/statistics)

| Data Item | Source Document | Format | Purpose |
|---|---|---|---|
| Registered accommodation establishments per district | SLTDA Annual Statistical Report (PDF) | Count per district | Tourist intensity numerator |
| Total bed capacity per district | Same | Integer per district | Tourist Vehicle Inflow Index |
| Average occupancy rate | Same | % per year | Scale tourist sessions by actual usage |

**Tourist Vehicle Inflow Index:**
```
TVII(d) = Bed_Capacity(d) × Occupancy_Rate(d) ÷ 2.5 (persons/vehicle)
```

---

### 5.4 — Data from Interviews (Primary Data — Your Original Collection)

**Target:** 33–52 respondents, stratified across four typology groups.

#### Complete Interview Questionnaire

> **Preamble:** *"This is a research study from NSBM Green University on EV charging patterns in Sri Lanka. This interview takes 10–15 minutes. Your responses will be anonymized and used only for academic research."*

| Q# | Question | Answer Type | Monte Carlo Variable Produced |
|---|---|---|---|
| Q1 | What is the model and year of your EV? | Dropdown: Nissan Leaf 24kWh / Leaf 30kWh / BYD Atto 3 / MG ZS EV / Electric Tuk-tuk / Electric 2-wheeler / Other | `v_class`, `B_nom` |
| Q2 | On a typical day, how many kilometres do you drive before you charge? | Number input (km) | `d_trip` — fitted to LogNormal(μ, σ) |
| Q3 | What is your main reason for driving? | Dropdown: Daily work commute / Business trips / Personal/household / Tourism/long trips / Delivery/commercial | Typology validation + assignment |
| Q4 | Where do you USUALLY charge your EV? | Dropdown: Home slow socket (13A) / Home wall-box (Level 2) / Workplace charger / Public slow charger / Public fast charger (DC) | `c_type` probability weights |
| Q5 | What time do you USUALLY plug in to charge? | Time picker (HH:MM) | `t_arr` — fitted to Normal or Gaussian Mixture |
| Q6 | What time do you USUALLY unplug? | Time picker (HH:MM) | `t_sess` cross-validation |
| Q7 | When you plug in, approximately what % battery do you have left? | Slider: 0–100% | `SoC_arr` — fitted to Beta(α, β) |
| Q8a | Does your home have a 3-phase electricity connection with a registered CEB Time-of-Use (TOU) meter? | Yes / No / Not sure | `p_3phase` = count(Yes) / total |
| Q8b | If YES to Q8a, do you actively wait until 10:30 PM to plug in your EV to save money? | Yes / No | `p_TOU` = count(Yes) / count(Q8a=Yes) |
| Q9 | On average, how many times per week do you charge your EV? | Number input (1–14) | Session frequency — fitted to Poisson(λ) |
| Q10 | Which district do you live in? | Dropdown: all 25 districts | Geographic stratification variable |

**Distribution fitting per parameter:**

| Parameter | Distribution | Fitting Formula |
|---|---|---|
| Trip distance (Q2) | LogNormal(μ, σ) | μ = mean(log(responses)); σ = std(log(responses)) |
| Arrival time (Q5) | Normal(μ, σ) or Gaussian Mixture | If unimodal: μ=mean, σ=std. If bimodal: fit 2-component GMM |
| SoC at arrival (Q7) | Beta(α, β) | α = μ²(1−μ)/σ² − μ; β = α(1−μ)/μ |
| 3-Phase TOU Meter (Q8a) | Bernoulli(p) | p = count("Yes") / n_residential_respondents |
| TOU probability (Q8b) | Bernoulli(p) | p = count("Yes") / count(Q8a="Yes") |
| Charging frequency (Q9) | Poisson(λ) | λ = mean(responses per typology) |
| Charger type (Q4) | Multinomial(p₁, p₂, p₃) | pᵢ = count(type_i) / n_respondents per typology |

**Recruitment targets (Justified by Central Limit Theorem, n ≥ 30 per stratum):**

| Typology | Who | Where | Target Count |
|---|---|---|---|
| T1 Urban Commercial | EV office commuters in Colombo / Kandy | Facebook "EV Sri Lanka", LinkedIn | 40–50 |
| T2 Suburban Residential | EV home-chargers in Gampaha / Moratuwa | Facebook EV groups, BYD / Nissan / MG dealerships | 40–50 |
| T3 Tourist Destination | Long-trip drivers (Colombo→Kandy/Galle/Nuwara Eliya) | Facebook road trip posts, Instagram EV community | 40–50 |
| T4 Highway Corridor | Long-distance commuters, hotel fleet EV operators | EV Facebook group, hotel HR contacts | 40–50 |
| **Total** | | | **160–200** |

---

### 5.5 — Data from DMT (Department of Motor Traffic)

| Data Item | Format | Purpose |
|---|---|---|
| EV import records by vehicle category per district | Table: vehicle type × district | Fleet class composition per district → `fleet_weights[d]` |
| Vehicle registration year distribution | Histogram per class | Average fleet age per district → SoH calculation |

> If DMT data is inaccessible: use import duty levy categories from Central Bank Annual Report as proxy. Supplement with interview Q1 distribution.

---

### 5.6 — CEB Data (Validation Only)

| Data Item | Source | Purpose |
|---|---|---|
| Residential feeder hourly load curves | CEB Statistical Digest | Validate T2 simulated evening peak |
| Commercial feeder peak demand window | CEB Annual Report | Validate T1 simulated midday peak |

---

### 5.7 — Published Literature Constants (Fixed)

| Constant | Value | Citation |
|---|---|---|
| Nissan Leaf 24kWh degradation rate (hot climate) | **3.1% per year** | Real-world study: 1,382 readings from 283 Leafs (2011–2017); air-cooled, hot-climate sample |
| Nissan Leaf 30kWh initial degradation | **9.9% first 2 years** | Same study |
| BYD / MG ZS EV (liquid-cooled) | 2.0% per year | Published BTMS comparative study |
| Electric tuk-tuk | 5.0% per year | Estimated from similar LFP chemistry vehicles |
| Nissan Leaf energy consumption | 0.17 kWh/km | Published Leaf efficiency specification |
| BYD Atto 3 energy consumption | 0.19 kWh/km | BYD official specification |
| Electric tuk-tuk consumption | 0.05 kWh/km | 3-wheeler electrification study estimate |
| CEB domestic TOU off-peak window | 10:30pm – 5:30am | CEB published tariff schedule |

---

## 6. Fleet Composition and Degradation Model

| Vehicle Class | B_nom (kWh) | Degradation Model (SoH) | Urban District % | Rural District % |
|---|---|---|---|---|
| Nissan Leaf 24kWh (2012–2017) | 24 | SoH = 1 − 0.031 × age | 30% | 15% |
| Nissan Leaf 30kWh (2017–2019) | 30 | SoH = 1 − min(0.099×age, 0.099×2) − 0.031×max(age−2, 0) | 20% | 10% |
| BYD Atto 3 / MG ZS EV (2022+) | 50–72 | SoH = 1 − 0.020 × age | 15% | 5% |
| Electric Tuk-tuk | 6 | SoH = 1 − 0.050 × age | 25% | 55% |
| Electric 2-wheeler | 2 | SoH = 1 − 0.040 × age | 10% | 15% |

> SoH is clipped to minimum 0.50 (battery is retired below 50% original capacity).

---

## 7. Statistical Parameter Sets Per Typology (Initial Priors)

> All values below are **initial priors** used if interview data is not yet available. Replace with interview-derived values after data collection.

### T1 — Urban Commercial Hub
| Parameter | Distribution | Prior Value |
|---|---|---|
| Arrival time | Normal(μ, σ) | μ=10.0 hrs, σ=1.5 hrs |
| SoC at arrival | Beta(α=3, β=2) | Mean ≈ 60% |
| Trip distance | LogNormal(μ=2.3, σ=0.5) | Mean ≈ 12 km |
| Charger type | Multinomial | Slow=0.15, L2=0.65, DC=0.20 |
| Target SoC | Fixed | 0.80 |
| Session frequency | Poisson(λ=4) | 4 sessions/week |

### T2 — Suburban Residential Zone
| Parameter | Distribution | Prior Value |
|---|---|---|
| Arrival time (pre-TOU) | Normal(μ, σ) | μ=20.5 hrs (8:30pm), σ=1.5 |
| Arrival time (TOU-shifted) | Uniform | [22.5, 29.5] (10:30pm–5:30am) |
| 3-Phase Meter probability | Bernoulli(p) | **p derived from Q8a responses** |
| TOU shift probability | Bernoulli(p) | **p derived from Q8b responses (conditional on 3-phase)** |
| SoC at arrival | Beta(α=2, β=3) | Mean ≈ 40% |
| Trip distance | LogNormal(μ=2.8, σ=0.6) | Mean ≈ 18 km |
| Charger type | Multinomial | Slow=0.70, L2=0.25, DC=0.05 |
| Target SoC | Fixed | 0.95 |
| Session frequency | Poisson(λ=5) | 5 sessions/week |

### T3 — Tourist Destination
| Parameter | Distribution | Prior Value |
|---|---|---|
| Arrival time | Uniform | [9.0, 17.0] (9am–5pm) |
| SoC at arrival | Beta(α=1.5, β=5) | Mean ≈ 23% |
| Trip distance | LogNormal(μ=4.0, σ=0.7) | Mean ≈ 80 km |
| Charger type | Multinomial | Slow=0.05, L2=0.25, DC=0.70 |
| Target SoC | Fixed | 0.85 |
| Session frequency | Poisson(λ=2) | 2 sessions/week |
| Session count scaler | SLTDA TVII index | Applied per district |

### T4 — Highway Transit Corridor
| Parameter | Distribution | Prior Value |
|---|---|---|
| Arrival time | GaussianMixture | μ₁=8.0 (σ=0.8) + μ₂=17.0 (σ=0.8), equal weight |
| SoC at arrival | Beta(α=1, β=7) | Mean ≈ 12% |
| Trip distance | LogNormal(μ=4.5, σ=0.8) | Mean ≈ 120 km |
| Charger type | Multinomial | Slow=0.0, L2=0.05, DC=0.95 |
| Target SoC | Fixed | 0.80 |
| Session frequency | Poisson(λ=1.5) | 1.5 sessions/week |

---

## 8. Monte Carlo Simulation Design

### Convergence Testing Protocol
```
For N in [100, 250, 500, 1000, 2500, 5000, 10000, 25000]:
    Run simulation N times for reference case (Kandy, T3, Medium, 2026)
    Compute CV = std(peak_hour_demand) / mean(peak_hour_demand)
Plot CV vs N → find N* where |CV(N) - CV(2N)| < 0.01
Use N* for all 3,300 production runs
```

### Total Simulation Scale
```
10 years (2026–2035) × 25 districts × 4 typologies × 3 scenarios = 3,000 runs
Each run: N* iterations × vectorized NumPy operations
Estimated runtime on your machine: ~56 minutes (benchmarked)
```

### Core Simulation Loop (Vectorized Python)
```python
for d in DISTRICTS:
  for t in TYPOLOGIES:
    for year in YEARS:
      for scenario in SCENARIOS:

        N_evs = component1[d, year, scenario] * osm_weight[d, t]
        params = typology_params[t]

        all_curves = np.zeros((N_STAR, 24))

        for i in range(N_STAR):
          v_class  = np.random.choice(classes, N_evs, p=fleet_weights[d])
          B_nom    = battery_capacity[v_class]
          SoH      = 1 - degradation_rate[v_class] * vehicle_age[v_class]
          B_eff    = B_nom * np.clip(SoH, 0.5, 1.0)

          d_trip   = np.random.lognormal(params.mu_dist, params.sigma_dist, N_evs)
          SoC_arr  = np.clip(np.random.beta(params.alpha, params.beta, N_evs), 0.05, 0.95)
          E_need   = np.clip((params.SoC_tgt - SoC_arr) * B_eff, 0, B_eff)
          c_kW     = np.random.choice([1.5, 7.2, 50], N_evs, p=params.charger_probs)
          t_arr    = draw_arrival(params, N_evs)      # typology-specific draw

          if t == 'Residential':
            # Only EVs at homes with a 3-phase TOU meter have the option to shift
            has_3phase = np.random.binomial(1, params.p_3phase, N_evs).astype(bool)
            # Of those with a meter, some choose to shift
            tou_shift = np.random.binomial(1, params.p_tou, N_evs).astype(bool)
            # Final shift is logical AND
            actual_shift = has_3phase & tou_shift
            t_arr[actual_shift] = np.random.uniform(22.5, 29.5, actual_shift.sum())

          bins = np.clip(t_arr.astype(int) % 24, 0, 23)
          all_curves[i] = np.bincount(bins, weights=c_kW, minlength=24)

        save_result(d, t, year, scenario, all_curves)
```

### Bottom-Up Spatial Scaling (District-Level Curve Generation)
This framework utilizes the globally recognized academic standard known as **Bottom-Up Spatial Scaling** (or Spatial Micro-Simulation) to generate the final district-level demand curves. The Monte Carlo engine mathematically combines the Primary Survey Data (Human Behavior) with the GIS/DMT Data (Spatial Density) without needing a country-wide survey:
1. **The Shape:** The 160-200 targeted survey responses generate 4 normalized probability curves (one per Typology).
2. **The Scale:** For a specific district (e.g., Colombo), the code extracts the total Fleet Size from the DMT data and the Typology composition weights from the OSM GIS data (e.g., 60% Urban Commercial, 30% Suburban).
3. **The Generation:** The engine multiplies the normalized Typology curves by the specific District's fleet size and OSM weights, then sums them together. This scales micro-behavioral survey data up to generate 25 unique macro-spatial district curves in Megawatts.

### 8.2 — Theoretical Rationale for Monte Carlo
*   **Why use it?** Sri Lanka lacks historical smart-meter data for EV charging. The Monte Carlo engine acts as a "synthetic data generator" to overcome this data scarcity. It translates small-scale probabilistic human behavior (from the survey) into massive, 10-year historical load profiles.
*   **What it produces:** It outputs exactly 3,000 synthetic load curves across all districts, typologies, and scenarios. This acts as the required "ground truth" dataset needed to train the deep learning model.

---

## 9. N-BEATSx Forecasting Design

### Training Data Structure
```
Dataset Base (Synthetic Past): 2026–2031 (6 years × 25 districts = 150 per-EV normalized profiles per typology)
Data Augmentation (Mandatory to prevent overfitting): 
  + Gaussian noise injection & Time Jittering (×10 augmentation) 
  = 1,500+ training sequences per typology
Test (Held Out Future): 2032–2035 (4 years × 25 districts = 100 sequences)
```

### Context-Aware Global Architecture
| Hyperparameter | Value |
|---|---|
| Model | N-BEATSx (Neural Basis Expansion Analysis with Exogenous Variables) |
| Input (Target) | 24 (historical 24-hour profile) |
| Static Exogenous Inputs | District ID (categorical), Typology (categorical), Fleet Size (numerical) |
| Blocks | 1 Trend Block (Polynomial), 1 Seasonality Block (Fourier) |
| Loss | MSE / MAE |
| Optimizer | Adam, lr=0.001 with early stopping |
| Outputs | Predicted Trend (growth), Predicted Seasonality (daily shape) |

### Validation Protocol
```
N-BEATSx trained on augmented 2026–2031 synthetic profiles
Predicts 2032–2035 without having seen those years
Compare N-BEATSx prediction vs Monte Carlo 2032–2035 ground truth
Metrics: RMSE per hour, MAPE on peak demand, Pearson r on curve shape
Report separately per typology (T1, T2, T3, T4)
```

### Baseline Comparison (Mandatory)
```
Baseline 1: Linear interpolation between 2026 and 2035 MC profiles
Baseline 2: ARIMA(1,1,0) on peak demand time series
Compare interpretability (Trend/Seasonality decomposition vs black-box baseline)
```

### 9.1 — Theoretical Rationale for N-BEATSx
*   **Why use it?** Standard models like LSTM are "black boxes" that cannot explain their forecasts. N-BEATSx is structurally interpretable and context-aware (utilizing exogenous inputs like District ID and Fleet Size).
*   **What it produces:** It mathematically extracts the underlying `Trend Curve` (long-term grid demand growth) and `Seasonality Curve` (the shifting daily peak shape). 
*   **The Ultimate Goal:** Once validated against the Monte Carlo ground truth, the trained N-BEATSx model becomes a standalone forecasting engine. End-users (CEB) can use it to instantly predict post-2035 demand simply by inputting a future Fleet Size, completely bypassing the need to re-run massive Monte Carlo simulations.

### 9.2 — Validation Contingency Plan (If AI Fails)
If the N-BEATSx model fails to accurately forecast the 2032-2035 hold-out set, the following 3-step contingency plan is enacted:
1.  **Overfitting Diagnosis:** Increase Data Augmentation (Gaussian noise and time-jittering) to force the model to generalize.
2.  **Exponential Shift:** If EV adoption spikes non-linearly (S-Curve), feed an explicit non-linear 'Growth Factor' as an exogenous input so the AI learns exponential scaling.
3.  **Ultimate Fallback:** Abandon Neural Networks and utilize the robust Monte Carlo simulation to generate the full 10-year timeline, applying a standard statistical ARIMA or Prophet model to extract the trend lines.

---

## 10. Validation Strategy

| Typology | Surrogate Data Source | Validation Method |
|---|---|---|
| T1 Commercial | CEB Annual Report commercial feeder peak timing | Simulated peak window (10am–2pm) matches CEB commercial peak |
| T2 Residential | CEB Statistical Digest residential load curves | Evening peak amplitude and timing compared to CEB residential load factor |
| T3 Tourist | SLTDA monthly tourist arrival data | Tourist typology demand peaks align with SLTDA high-season months |
| T4 Highway | Published Sri Lanka highway traffic pattern reports | Bimodal morning/evening peak structure confirmed |

---

## 11. Sensitivity Analysis Plan

| Parameter | Baseline | Tested Range | Outcome Metric |
|---|---|---|---|
| TOU shift probability p | Interview-derived | ±30% | Residential evening peak kW |
| Nissan Leaf degradation rate | 3.1%/year | 2.0–4.5%/year | SoC at arrival distribution |
| Tourist party size | 2.5 persons | 2.0–4.0 | T3 N_EVs per district |
| Target SoC (T3) | 0.85 | 0.75–0.95 | Session energy and duration |
| Monte Carlo N iterations | N* | 0.5×N* and 1.5×N* | CV of peak demand |
| Mainstream behavioural shift | Phase A early-adopter | Phase B corrected | 2030–2035 profile change |

---

## 12. Output File Structure

| File | Columns |
|---|---|
| `monte_carlo_profiles.csv` | District, Typology, Year, Scenario, N_EVs, Peak_Hour, Peak_kW, Daily_kWh, Mean_H00–H23, P05_H00–H23, P50_H00–H23, P95_H00–H23, Norm_H00–H23 |
| `nbeatsx_forecasts.csv` | District, Typology, Year (2032–2035), Predicted_H00–H23, Trend_H00_H23, Seasonality_H00_H23, Actual_H00–H23, RMSE, MAPE |
| `typology_weights.csv` | District, f1_raw, f2_raw, f3_raw, f4_raw, w_T1, w_T2, w_T3, w_T4 |
| `interview_data.csv` | Respondent_ID, Typology_Group, Q1–Q10 (anonymized) |
| `interview_parameters.csv` | Typology, Parameter, Distribution, Mean, SD, N_sample |
| `fleet_composition.csv` | District, Leaf24_pct, Leaf30_pct, BYD_pct, Tuktuk_pct, TwoWheeler_pct |
| `convergence_test.csv` | N_iterations, CV_T1, CV_T2, CV_T3, CV_T4, N_star |
| `sensitivity_results.csv` | Parameter, Variation, Typology, Baseline_kW, Varied_kW, Delta_pct |
| `validation_results.csv` | Typology, Source, Metric, Simulated, Reference, Delta_pct |

---

## 13. System Deployment & End-User Handover (Grid Pulse EV)

To ensure the research is highly accessible to the Ceylon Electricity Board (CEB) Planning Directorate, the validated N-BEATSx deep learning model will be deployed as an interactive web application dubbed **"Grid Pulse EV"** (`https://grid-pulse-ev.vercel.app/demand`).

### User Interface & Features
The web dashboard provides a "System Load Topography" module allowing non-technical end-users to generate instant demand forecasts.

*   **Sector Definition Panel:** Users can toggle between the 4 mapped spatial typologies (e.g., *Urban Commercial Hub (T1)*).
*   **Timeline Spec Slider:** An interactive timeline allowing users to slide the forecast year up to 2035 (and beyond).
*   **Dynamic 24-Hour Load Curve:** The UI renders the forecasted stochastic load profile (in kW) for the selected parameters, including shaded probability envelopes (5th-95th percentiles) to visualize uncertainty.
*   **Critical Output Metrics:** The dashboard instantly calculates and displays the three most critical metrics required for grid planning:
    1.  **Peak Hour** (e.g., 11:00)
    2.  **Peak Magnitude** (e.g., 138.2 kW)
    3.  **Daily Energy** (e.g., 1,724 kWh)

### Handover Protocol
By providing a visual web interface, the CEB engineers do not need to understand Python, Monte Carlo simulations, or N-BEATSx neural network architectures. They simply select a sector and a year, and the deployed model outputs the actionable grid metrics instantly.

---

## 14. Technology Stack

| Tool | Purpose |
|---|---|
| Python 3.10+ | Core language |
| NumPy & Numba | Vectorized Monte Carlo simulation |
| SciPy | Distribution fitting (Beta, LogNormal) |
| Pandas | Data management and CSV I/O |
| OSMnx & GeoPandas | OSM land-use polygon extraction and spatial mapping |
| NeuralForecast (Nixtla) | N-BEATSx model training |
| Statsmodels | ARIMA baseline |
| Matplotlib / Plotly | 24-hour profile visualizations |
| Scikit-learn | MinMax normalization, train/test utilities |
| React / Next.js / Vercel | End-user web dashboard deployment |

## 15. Execution Timeline — 14 Weeks

| Week | Phase | Tasks |
|---|---|---|
| 1 | OSM Extraction | Extract commercial, residential, tourism POI, road length for 25 districts. Compute min-max weights. Validate 5 districts manually. |
| 2 | SLTDA Collection | Download Annual Report PDF. Extract bed capacity, occupancy per district. Compute TVII. |
| 3–4 | Interview Design + Pilot | Finalize questionnaire. Build Google Form (English + Sinhala). Pilot with 3–5 respondents. Revise. |
| 5–6 | Interview Data Collection | Recruit via Facebook EV group, dealerships, LinkedIn. Collect 33–52 responses. |
| 7 | Parameter Estimation | Fit all responses to distributions using scipy.stats. Finalize parameter tables per typology. |
| 8 | Fleet Model | Extract DMT import data. Compute fleet composition per district. Cross-check with Q1 interview responses. |
| 9 | Convergence Test | Build simulation prototype. Run convergence test. Identify and record N*. |
| 10–11 | Monte Carlo Full Run | Run all 3,000 combinations. Save to monte_carlo_profiles.csv. Estimated: ~56 minutes. |
| 12 | N-BEATSx Preparation | Extract per-EV normalized profiles. Prepare target/static exogenous sequences. Apply 1,750+ Gaussian augmentation. |
| 13 | N-BEATSx Training | Train N-BEATSx and ARIMA baseline. Evaluate on held-out 2032–2035 test set. Record RMSE/MAPE per typology. |
| 14 | Sensitivity Analysis | Run all parameter variations. Identify most influential parameters. |
| 15 | Validation + Packaging | Compare against CEB and SLTDA surrogate data. Generate visualizations. Package all output files. |

---

## 16. Research Novelties

| Novelty | Contribution Statement |
|---|---|
| Place-Typology Stratified Demand Profiling | First study to generate EV charging demand profiles by functional land-use typology across 25 districts |
| Interview-Parameterized Monte Carlo for Sri Lanka | First primary behavioural data collection from Sri Lankan EV owners used to parameterize a Monte Carlo demand simulation |
| CEB TOU Tariff Shift Quantification | First empirical measurement of TOU-driven charging shifts, explicitly differentiating between standard single-phase and 3-phase smart meter adoption constraints |
| Tropical Battery Degradation Integration | First demand simulation incorporating published Nissan Leaf 3.1%/year air-cooled degradation rate for a tropical fleet |
| Data-Scarce Methodology Framework | Reproducible pipeline using OSM + SLTDA + interviews for EV demand profiling without smart meter or traffic data |
| Interpretable Context-Aware Deep Learning | First study training N-BEATSx on synthetic Monte Carlo profiles to forecast highly interpretable (trend/seasonality) demand evolution |
| Uncertainty Quantification via Percentile Envelopes | 5th/50th/95th percentile demand bands provide probabilistic worst-case planning envelope |

---

## 17. Limitations and Mitigations

| Limitation | Mitigation |
|---|---|
| Interview sample skewed toward early adopters | Two-phase design: Phase A (online) + Phase B (dealer expert). Mainstream correction for 2028–2035 profiles |
| TOU probability from small sample | Sensitivity analysis ±30%; sample size explicitly stated in thesis |
| OSM coverage sparse in rural districts | Supplement with Geofabrik PBF extract + Sentinel-2 land cover raster |
| SLTDA tourist data is aggregate, not vehicle-level | Party size sensitivity test 2.0–4.0; proxy method stated |
| No charging log validation for T3 and T4 | Surrogate validation via SLTDA seasonality + highway traffic pattern alignment |
| N-BEATSx may not outperform statistical baselines | Planned comparison reported honestly — baseline used if N-BEATSx fails |
| Component 1 projections carry uncertainty | Low/Medium/High scenarios propagate this uncertainty to all outputs |
