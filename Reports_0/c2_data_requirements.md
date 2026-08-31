# Component 2: Prototype Data Requirements & Integration Plan

**Component:** EV Charging Demand Modelling
**Member:** Herath H M K M

## 1. Purpose of this Data
To build a unified, interactive dashboard for our proposal presentation, we need to combine the outputs of all 4 research components. This document outlines exactly what sample/simulated data is needed from Component 2 to build the final prototype. 

The data you provide will show how charging behaviour impacts the grid. It will generate the 24-hour load curve charts on the dashboard, showing the panel exactly when peak charging happens (e.g., evening residential peaks vs. midday commercial peaks).

## 2. What to Provide
Please generate a realistic **synthetic/sample data** CSV file (since this is for the proposal, we don't need the final accurate model outputs yet, just realistic approximations).

**Suggested Filename:** `c2_demand_profiles.csv`

## 3. Required CSV Structure
Your CSV must contain the 24-hour kW load profile for different scenarios and place typologies.

| Column Name | Description | Example Value |
| :--- | :--- | :--- |
| `Typology` | The place typology | T1_Urban |
| `Scenario` | The adoption scenario | Medium |
| `Year` | The forecast year (2025 through 2035) | 2030 |
| `Hour_00` to `Hour_23` | 24 separate columns containing the predicted average kW demand for that specific hour | Hour_18: 45.2 |

## 4. Updates & Changes
If your component plan changes (e.g., adding specific vehicle classes like 2-wheelers vs 4-wheelers to the profiles), please update this document to reflect those changes before generating the sample data.
