# Full System Architecture Plan: Unified EV Infrastructure & Grid Forecasting System

This document outlines the master system architecture connecting all four components of your research into a single, cohesive workflow. This is critical for your overall thesis, as it shows how the outputs of one component serve as the inputs for the next.

## 1. The Core Data Flow (How the 4 Components Connect)

The research follows a logical, sequential progression from predicting EV numbers to placing charging stations:

1. **Component 1 (EV Adoption Forecasting):** 
   - **What it does:** Predicts *how many* EVs will exist in each district from 2026-2035.
   - **Where it goes:** Feeds the exact EV Fleet Size count (`N_EVs`) into **Component 2** (to calculate total power draw) and **Component 3** (to show where demand for chargers will be highest).
2. **Component 2 (24-Hour Demand Profiling):**
   - **What it does:** Takes the EV count from C1, combines it with your Primary Survey and OSM data, and predicts *when and how much* power those EVs will draw from the grid.
   - **Where it goes:** Feeds the "Uncontrolled Load Baseline" into **Component 4** (so it knows what needs optimizing) and provides the "Grid Stress Risk" to **Component 3** (so we avoid putting fast chargers on overloaded grid segments).
3. **Component 4 (Grid Optimization & Smart Charging):**
   - **What it does:** Takes the raw, uncontrolled power draw from C2 and runs it through an LP Scheduler against CEB solar and generation data to optimize charging times, reduce curtailment, and flatten the peak curve.
   - **Where it goes:** Outputs the final, optimized grid impact metrics.
4. **Component 3 (Spatial Infrastructure Siting):**
   - **What it does:** Takes demand density (from C1), grid stress limits (from C2/C4), and geospatial data to output the exact geographic locations for charging stations in phased rollouts (2027, 2030, 2035).

All components ultimately converge into the **Grid Pulse EV Web Dashboard** for delivery to the CEB Planning Directorate.

---

## 2. Eraser.io Diagram Code

You can copy and paste the following code directly into the left-hand text editor in **[Eraser.io](https://app.eraser.io/)** (create a new "Diagram as Code" or "Architecture Diagram"). It will automatically generate the flowchart for you.

```eraser
title Unified EV Infrastructure & Grid Forecasting Architecture (Sri Lanka)

// --- Shared Data Layer ---
Data Sources [icon: database, color: gray] {
  Macro & Policy Data (DMT, Census)
  Spatial GIS Data (OSM, DMC)
  Primary EV Owner Survey
  Utility Data (CEB, Solar)
}

// --- Component 1 ---
Component 1: EV Adoption [icon: car, color: blue] {
  Multi-Agent Framework
  Scenario Engine (Monte Carlo)
  District EV Fleet Projections (2026-35)
}

// --- Component 2 ---
Component 2: Demand Profiling [icon: activity, color: green] {
  Vectorized Monte Carlo Simulation
  N-BEATSx Deep Learning Forecasts
  24-Hour Uncontrolled Load Profiles
}

// --- Component 4 ---
Component 4: Grid Optimization [icon: zap, color: orange] {
  Net Demand & Curtailment Risk
  Curtailment-Aware LP Scheduler
  Optimized Grid Outcomes
}

// --- Component 3 ---
Component 3: Infrastructure Siting [icon: map-pin, color: purple] {
  Multi-Criteria Scoring Engine
  Set Covering Optimization Model
  Phased Station Siting (2027-35)
}

// --- Delivery Layer ---
Outputs [icon: monitor, color: yellow] {
  Grid Pulse EV Web Dashboard
  CEB Planning Directorate
}

// --- Connections & Data Flow ---
Macro & Policy Data (DMT, Census) > Multi-Agent Framework
Spatial GIS Data (OSM, DMC) > Vectorized Monte Carlo Simulation
Primary EV Owner Survey > Vectorized Monte Carlo Simulation
Utility Data (CEB, Solar) > Net Demand & Curtailment Risk
Spatial GIS Data (OSM, DMC) > Multi-Criteria Scoring Engine

Multi-Agent Framework > Scenario Engine (Monte Carlo)
Scenario Engine (Monte Carlo) > District EV Fleet Projections (2026-35)

// C1 feeds C2 and C3
District EV Fleet Projections (2026-35) > Vectorized Monte Carlo Simulation: Fleet Size (N_EVs)
District EV Fleet Projections (2026-35) > Multi-Criteria Scoring Engine: Demand Projections

Vectorized Monte Carlo Simulation > N-BEATSx Deep Learning Forecasts: Synthetic Curves
N-BEATSx Deep Learning Forecasts > 24-Hour Uncontrolled Load Profiles

// C2 feeds C4 and C3
24-Hour Uncontrolled Load Profiles > Net Demand & Curtailment Risk: Uncontrolled Baseline
24-Hour Uncontrolled Load Profiles > Multi-Criteria Scoring Engine: Grid Stress Risk

Net Demand & Curtailment Risk > Curtailment-Aware LP Scheduler
Curtailment-Aware LP Scheduler > Optimized Grid Outcomes

Multi-Criteria Scoring Engine > Set Covering Optimization Model
Set Covering Optimization Model > Phased Station Siting (2027-35)

// All flow to Dashboards
District EV Fleet Projections (2026-35) > Grid Pulse EV Web Dashboard
24-Hour Uncontrolled Load Profiles > Grid Pulse EV Web Dashboard
Optimized Grid Outcomes > Grid Pulse EV Web Dashboard
Phased Station Siting (2027-35) > Grid Pulse EV Web Dashboard

Grid Pulse EV Web Dashboard > CEB Planning Directorate: Decision Support
```

---

## 3. Eraser.io Styling & Presentation Tips

Once the diagram generates in Eraser.io, you should make a few manual adjustments to make it look perfect for an academic presentation:

1. **Layout Direction:** If the diagram looks too tall, look for the layout button in Eraser (usually a gear icon or layout toggle) and switch the flow direction from **Top-to-Bottom** to **Left-to-Right**. This usually fits better on a 16:9 presentation slide.
2. **Color Coding:** Notice that I added `color: blue`, `color: green`, etc., to the groups. In Eraser, this creates colored bounding boxes. Make sure these colors match the color scheme you used in your individual component slides.
3. **Line Routing:** You can click on the connection lines in Eraser and change their routing style from "Orthogonal" (sharp 90-degree corners) to "Curved" to make the flow look smoother.
4. **Exporting:** When exporting, choose **PNG (Transparent Background)** or **SVG**. Do not export with a solid white background, as it will look unprofessional if you paste it onto a dark-themed presentation slide.
