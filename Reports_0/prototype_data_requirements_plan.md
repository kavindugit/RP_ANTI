# Prototype Demo: Data Requirements & Integration Plan

**Purpose:** 
To build a unified, interactive dashboard for our proposal presentation, we need to combine the outputs of all 4 research components. This document outlines exactly what sample/simulated data each group member needs to generate and hand over so that the final prototype can be built.

---

## 📊 Component 1: EV Adoption Forecasting
**Member:** Ariyathilake P U L N

To visualize the growth of EVs and feed data into the charging demand models, we need the projected number of EVs for each of the 25 districts from 2025 to 2035.

**What to provide:** A CSV file containing the yearly projections under three different scenarios (Low, Medium, High).
**Suggested Filename:** `c1_ev_adoption_forecasts.csv`

**Required CSV Columns:**
1. `District` (e.g., Colombo, Gampaha, Kandy)
2. `Year` (2025 through 2035)
3. `Scenario` (Low / Medium / High)
4. `Total_EVs` (Integer count of predicted EVs)

**How it will be used in the demo:** 
This will power the interactive line charts in the dashboard, allowing the panel to see how EV adoption scales over time for any selected district.

---

## 📈 Component 2: EV Charging Demand Modelling
**Member:** Herath H M K M *(Your Component)*

To show how charging behaviour impacts the grid, you will need to provide the 24-hour demand curves.

**What to provide:** A CSV file containing the 24-hour kW load profile for different scenarios and typologies.
**Suggested Filename:** `c2_demand_profiles.csv`

**Required CSV Columns:**
1. `Typology` (Urban / Residential / Tourist / Highway)
2. `Scenario` (Low / Medium / High)
3. `Year` (2025 through 2035)
4. `Hour_00` to `Hour_23` (24 columns containing the predicted kW demand for that specific hour)

**How it will be used in the demo:** 
This will generate the 24-hour load curve charts, showing the panel exactly when peak charging happens (e.g., evening residential peaks vs. midday commercial peaks).

---

## ⚡ Component 3: Grid Hosting Capacity & Stress Assessment
**Member:** Wijesuriya W A A I

To visualize the stress on the national grid, we need the risk classification and capacity limits for the grid substations corresponding to each district.

**What to provide:** A CSV file mapping each district to its grid stress level.
**Suggested Filename:** `c3_grid_risk_assessment.csv`

**Required CSV Columns:**
1. `District` (All 25 districts)
2. `Substation_Name` (The primary grid substation for that area)
3. `Risk_Level` (Green / Amber / Orange / Red)
4. `Exhaustion_Year` (The year the substation hits capacity, e.g., 2029)
5. `Constraint_Type` (Thermal / Voltage / None)

**How it will be used in the demo:** 
This data will be used to color-code the interactive map of Sri Lanka. The panel will be able to instantly see which districts are at "Red" risk of grid failure and in what year it will happen.

---

## 🗺️ Component 4: GIS-Based Charging Station Placement
**Member:** Jasinarachchi J A D N N

To show the practical outcome of the framework, we need the exact geographic coordinates of the recommended charging stations, rolled out in phases.

**What to provide:** A CSV (or GeoJSON) file containing the exact locations of the proposed stations.
**Suggested Filename:** `c4_station_placements.csv`

**Required CSV Columns:**
1. `Station_ID` (e.g., CS001)
2. `Latitude` (e.g., 6.9271)
3. `Longitude` (e.g., 79.8612)
4. `District`
5. `Phase` (1 for 2027, 2 for 2030, 3 for 2035)
6. `Charger_Type` (e.g., 50kW DC, 150kW DC)

**How it will be used in the demo:** 
These coordinates will be plotted as interactive markers on the national map. The panel will have toggles to turn on "Phase 1", "Phase 2", and "Phase 3" to watch the charging network physically expand across Sri Lanka over time.

---

## Next Steps for the Group
1. **Review:** Please review the required CSV structures above.
2. **Generate Sample Data:** Since this is for the *proposal presentation*, we do not need the final accurate model outputs yet. Please generate **realistic synthetic/sample data** that perfectly matches these CSV formats.
3. **Integration:** Once everyone sends their CSV files, they will be loaded into the unified web dashboard to build a fully working, interactive prototype for the panel.
