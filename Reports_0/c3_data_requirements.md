# Component 3: Prototype Data Requirements & Integration Plan

**Component:** Grid Hosting Capacity & Stress Assessment
**Member:** Wijesuriya W A A I

## 1. Purpose of this Data
To build a unified, interactive dashboard for our proposal presentation, we need to combine the outputs of all 4 research components. This document outlines exactly what sample/simulated data is needed from Component 3 to build the final prototype. 

The data you provide will be used to visualize the stress on the national grid. It will color-code the interactive map of Sri Lanka, allowing the panel to instantly see which districts are at a "Red" risk of grid failure and in what year it will happen.

## 2. What to Provide
Please generate a realistic **synthetic/sample data** CSV file (since this is for the proposal, we don't need the final accurate model outputs yet, just realistic approximations).

**Suggested Filename:** `c3_grid_risk_assessment.csv`

## 3. Required CSV Structure
Your CSV must map each of the 25 districts to its primary grid substation, risk level, and capacity exhaustion year.

| Column Name | Description | Example Value |
| :--- | :--- | :--- |
| `District` | Name of the district (for all 25 districts) | Gampaha |
| `Substation_Name` | The primary grid substation for that area | Sapugaskanda 132kV |
| `Risk_Level` | The risk classification (Green / Amber / Orange / Red) | Red |
| `Exhaustion_Year` | The year the substation hits its capacity | 2028 |
| `Constraint_Type` | The type of constraint (Thermal / Voltage / None) | Thermal |

## 4. Updates & Changes
If your component plan changes (e.g., assessing at a more granular feeder level rather than the 132/33kV substation level), please update this document to reflect those changes before generating the sample data.
