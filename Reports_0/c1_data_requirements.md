# Component 1: Prototype Data Requirements & Integration Plan

**Component:** EV Adoption Forecasting
**Member:** Ariyathilake P U L N

## 1. Purpose of this Data
To build a unified, interactive dashboard for our proposal presentation, we need to combine the outputs of all 4 research components. This document outlines exactly what sample/simulated data is needed from Component 1 to build the final prototype. 

The data you provide will be used to visualize the growth of EVs and act as the base multiplier for the charging demand models. It will power the interactive line charts in the dashboard, allowing the panel to see how EV adoption scales over time for any selected district.

## 2. What to Provide
Please generate a realistic **synthetic/sample data** CSV file (since this is for the proposal, we don't need the final accurate model outputs yet, just realistic approximations).

**Suggested Filename:** `c1_ev_adoption_forecasts.csv`

## 3. Required CSV Structure
Your CSV must contain the yearly projections for all 25 districts under three different scenarios (Low, Medium, High).

| Column Name | Description | Example Value |
| :--- | :--- | :--- |
| `District` | Name of the district (for all 25 districts) | Colombo |
| `Year` | The forecast year (2025 through 2035) | 2027 |
| `Scenario` | The adoption scenario | Medium |
| `Total_EVs` | Integer count of predicted EVs | 1910 |

## 4. Updates & Changes
If your component plan changes (e.g., adding new scenarios, breaking it down by vehicle type rather than total EVs), please update this document to reflect those changes before generating the sample data.
