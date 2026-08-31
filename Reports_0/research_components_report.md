# Research Project Plan: Electric Vehicle (EV) Infrastructure Framework for Sri Lanka

This report outlines the basic ideas, sub-objectives, tasks, and novel contributions of the four core components of the research project focused on building a comprehensive framework for Electric Vehicle infrastructure planning in Sri Lanka.

---

## Component 1: District-Level EV Adoption Forecasting
**Member Name:** Ariyathilake P U L N  
**Registration No:** IT23413788

### Sub-Objective
To build a district-level EV adoption forecasting model for Sri Lanka that predicts the number of registered electric vehicles in each of the 25 districts from 2025 to 2035, by combining historical vehicle registration data with socioeconomic driving factors, using an ensemble of time-series and machine learning models.

### Tasks
- **Data Collection & Cleaning:** Collect and clean Department of Motor Traffic (DMT) vehicle registration data by district, including pre-2020 and post-February 2025 periods, and handle the structural data gap caused by the vehicle import ban.
- **Socioeconomic Data Gathering:** Gather district-level socioeconomic variables (population density, household income, urbanization rate, and fuel price history) from the Census and Statistics Department, CPC, and World Bank.
- **Exploratory Data Analysis (EDA):** Perform EDA to identify registration trends, spatial EV distribution, and correlations with socioeconomic factors.
- **Model Development:** Develop and train ARIMA, Prophet, LSTM, and XGBoost models individually, then combine them into an ensemble, evaluated using RMSE, MAE, and MAPE with walk-forward cross-validation.
- **Spatial Disaggregation:** Apply dasymetric mapping using OpenStreetMap data to disaggregate district-level projections to city/town level for use by Components 2 and 4.
- **Data Export:** Export 2025–2035 district and city-level EV projections as inputs to the broader framework.

### Novelty
Existing studies apply EV adoption forecasting in contexts with continuous, uninterrupted registration data (e.g., US, India, Malaysia). None address a setting where historical data contains a multi-year structural break caused by a government-imposed import ban, as experienced in Sri Lanka from 2020–2025. Adapting an ensemble model to reconstruct adoption trends across this disrupted data gap, incorporating Sri Lanka-specific socioeconomic drivers (post-crisis recovery trajectory, import duty policy shifts, district-level income disparity), represents a methodological contribution not found in reviewed literature. Furthermore, this component introduces dasymetric spatial disaggregation to translate district-level EV projections into city and town-level demand estimates for infrastructure planning, enabling practical charging station placement in a context where sub-district official data does not exist.

---

## Component 2: EV Charging Demand Modelling
**Member Name:** Herath H M K M  
**Registration No:** IT23249684

### Sub-Objective
To model hourly and seasonal EV charging demand patterns at the district level across Sri Lanka's 25 districts by adapting international charging session datasets to the Sri Lankan context using behavioural simulation and deep learning forecasting, producing demand curves that feed into grid stress assessment (Component 3) and station placement optimization (Component 4).

### Tasks
- **Data Adaptation:** Acquire and contextualise ACN-Data and UK government open charging datasets by mapping session attributes to Sri Lankan driving and charging behaviour using census data, fuel price history, and an EV owner survey.
- **Behavioural Simulation:** Define probability distributions for key user behaviour variables (commute distance, charging frequency, preferred charging time, battery capacity, state-of-charge at plug-in) calibrated to Sri Lankan conditions and run a Monte Carlo simulation to generate synthetic charging session profiles per district.
- **Demand Aggregation:** Aggregate simulated profiles with Component 1's EV population projections to produce hourly and daily charging demand curves per district across low, medium, and high penetration scenarios and dry/wet season splits.
- **Forecasting Models:** Train BiLSTM and Transformer-based models on the synthetic demand time series to forecast future charging load patterns; benchmark against ARIMA and persistence baselines using RMSE, MAE, and MAPE.
- **Validation & Sensitivity Analysis:** Validate simulated demand against ACN-Data holdout sets and available CEB load data; conduct sensitivity analysis on behavioural assumptions (e.g., overnight vs. workplace charging preference).
- **Data Packaging:** Package district-level hourly demand forecasts as structured inputs for Components 3 and 4, and contribute the demand layer to the national planning dashboard.

### Novelty
- **Sri Lanka-Specific Behavioural Calibration:** No published study has systematically adapted ACN-Data or equivalent datasets to a South Asian market accounting for tropical seasonality, shorter average commutes, Chinese EV battery profiles, and income-constrained charging behaviour.
- **District-Stratified Monte Carlo Simulation under Data Scarcity:** This component provides a reproducible synthetic demand generation framework using openly available demographic and behavioural priors, addressing the data gap common across developing economies.
- **Hybrid Simulation–Deep Learning Pipeline:** While hybrid approaches exist, they are usually applied to single cities or uniform grids. This work extends the pipeline across 25 Sri Lankan districts with distinct socioeconomic and load profiles, producing the first district-resolved, seasonally stratified EV charging demand forecast for Sri Lanka.

---

## Component 3: Grid Hosting Capacity & Stress Assessment
**Member Name:** Wijesuriya W A A I  
**Registration No:** IT23274648

### Sub-Objective
To assess EV hosting capacity and quantify grid headroom across Sri Lanka’s electricity network at the 132/33 kV grid-substation level using real CEB capacity data, and at the 11 kV feeder level using power-flow simulation; and to train a machine learning classifier that tiers each substation zone into grid-stress risk bands, identifying the EV penetration threshold and the binding constraint type (thermal / voltage) at which network reinforcement becomes necessary.

### Tasks
- **Baseline Headroom Establishment:** Extract day-peak and night-peak demand forecasts and firm (N-1) transformer capacities for the ~49 named 132/33 kV grid substations from CEB’s Long-Term Transmission Development Plan and LTGEP 2025–2044; establish a per-substation headroom baseline using CEB records and Statistical Digest.
- **Load Integration & Headroom Exhaustion:** Layer Component 2’s projected hourly EV charging demand onto each substation’s existing peak load under Component 1’s adoption scenarios (2025–2035), and compute the year each substation’s headroom is exhausted.
- **Feeder-Level Simulation:** Build a representative 11 kV distribution feeder model in OpenDSS (using a real CEB/LECO feeder or a parameterised IEEE 33-bus / CIGRE LV benchmark) and compute feeder-level hosting capacity via Monte Carlo sampling over EV arrival time and charging location.
- **ML Classification:** Train ML classification models using the substation headroom margins and feeder hosting-capacity results to classify each grid-substation zone into green/amber/orange/red risk bands and predict the EV penetration threshold and binding constraint type.
- **Risk Mapping:** Produce a colour-coded national grid-headroom risk map by named grid-substation zone and export the classification and thresholds as a structured layer for Component 4’s siting constraints and the unified planning dashboard.

### Novelty
Existing EV grid-impact work for Sri Lanka either assesses impact at the national system-operation level or focuses on distribution-level hosting-capacity for solar PV, not EVs. Internationally, established hosting-capacity methods have never been calibrated to Sri Lankan grid-substation capacities or load curves. This component delivers the first EV hosting-capacity and grid-headroom assessment for Sri Lanka, uniquely combining: (i) real CEB grid-substation demand forecasts and firm (N-1) transformer capacities, (ii) physics-based feeder-level hosting-capacity simulation, and (iii) an ML risk classifier that maps each substation zone to a penetration threshold and constraint type. This produces a substation-resolved national grid-stress map that does not currently exist, directly supplying the grid-risk constraint consumed by Component 4.

---

## Component 4: GIS-Based Charging Station Placement Optimization
**Member Name:** Jasinarachchi J A D N N  
**Registration No:** IT23215160

### Sub-Objective
To build a GIS-based optimization framework that recommends a prioritized, phased network of public EV charging station locations across Sri Lanka, by integrating city-level EV demand projections, grid stress risk classifications, road infrastructure, and flood vulnerability data into a multi-criteria scoring and constrained optimization pipeline.

### Tasks
- **GIS Database Construction:** Construct a national GIS database by extracting OpenStreetMap road network topology, building footprints, and land-use polygons for all 25 districts; overlay Disaster Management Centre flood hazard zone shapefiles to classify candidate locations into flood-risk tiers.
- **Candidate Location Generation:** Generate candidate charging station locations at road intersections, fuel stations, and high-traffic nodes identified through betweenness centrality analysis on the road network graph, filtering out locations within flood high-risk zones and protected areas.
- **Constrained Optimization Model:** Formulate the placement problem as a budget-constrained set covering optimisation (maximising total weighted coverage subject to per-phase station limits, minimum inter-station distance, and flood-risk exclusion). Solve using a greedy heuristic with marginal gain computation, validated against the LP relaxation lower bound.
- **Phased Rollout Execution:** Execute the optimisation in three phased runs: 50 stations for 2027, 100 cumulative for 2030, and 200 cumulative for 2035, locking in prior placements and re-scoring remaining candidates iteratively.
- **Rollout Plan Export:** Export the phased rollout plan as a GeoJSON layer with per-station attributes (phase, capacity recommendation based on Component 2 demand, suitability score, grid risk zone, flood zone tier) for the national planning dashboard.

### Novelty
Existing EV charging station placement studies typically adopt narrow approaches (e.g., power-system-centric optimisation requiring full load flow computation, or operations-research placement lacking spatial/electrical constraints). None combine real grid stress risk classification, flood vulnerability exclusion, demand-driven phased rollout, and graph-theoretic traffic analysis on actual road topology. 
By operationalising grid stress through Component 3's ML-classified risk map as a discrete constraint, this approach becomes viable in data-scarce utility environments without requiring full load flow computations. Furthermore, it expands the candidate space through network centrality analysis rather than limiting it to existing amenities, a significant advantage in areas with sparse fuel infrastructure. The integration of flood zone exclusion as a first-order filter in a developing-country EVCS placement model has not been reported previously, representing a practical and crucial contribution for climate-vulnerable island nations like Sri Lanka.
