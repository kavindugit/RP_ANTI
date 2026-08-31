# Research Report: Validation Methods for Component 2

Validating your research is the most critical part of defending a PhD. Because Sri Lanka does not have historical smart-meter data, you cannot simply compare your output to "real CEB data." This is a famous academic problem known as **Validating Synthetic Data in Data-Scarce Environments**.

Based on the latest academic literature, you must use a **Two-Tiered Validation Strategy**: one to validate the Monte Carlo simulator, and one to validate the N-BEATSx AI.

---

## Tier 1: Validating the N-BEATSx Forecast (The AI)
Validating the AI is purely mathematical. You need to prove that the AI actually learned the trend, rather than just guessing.

**Method: Chronological Hold-Out Validation (Time Series Split)**
*   **How to do it:** You generate Monte Carlo data for 2025–2031. You **hide** the years 2030 and 2031 from the AI. You only train the N-BEATSx model on 2025–2029. 
*   **The Test:** You ask the AI to predict 2030 and 2031. You then compare the AI's prediction against the "hidden" Monte Carlo data you generated for those years.
*   **The Metrics:** You will use two specific academic metrics to score the AI:
    1.  **MAPE (Mean Absolute Percentage Error):** Tells you the percentage of error (e.g., "The forecast was 95% accurate").
    2.  **RMSE (Root Mean Square Error):** Punishes the AI heavily if it completely misses the peak hour.

---

## Tier 2: Validating the Monte Carlo Synthetic Data
This is the harder part. How do you prove that your 2025 synthetic curve is actually realistic for Sri Lanka if no real data exists? You must use three methods:

### Method A: Heuristic (Physics) Validation
You mathematically prove that your synthetic data does not violate the laws of physics or hardware limits.
*   *Check 1:* Does any EV pull more than 7.2 kW if it is connected to a Level 2 charger? (If yes, the simulation is broken).
*   *Check 2:* Does the total energy (kWh) consumed by the 50,000 EVs in Colombo exactly match the total battery capacity required for the distances they traveled? (Energy Conservation).

### Method B: Surrogate Benchmarking
You compare the *shape* of your Sri Lankan curve against a country with similar demographics and climate (e.g., India or Thailand).
*   If India's residential charging peak happens at 7:30 PM, and your Monte Carlo simulation predicts Sri Lanka's peak at 7:00 PM, you have strong **Distributional Faithfulness**. If your simulation predicts a peak at 3:00 AM, you know something is wrong.

### Method C: Expert Delphi Method (Face Validity)
This is the ultimate PhD defense mechanism.
*   You print out your final 24-hour Demand Curves.
*   You organize a focus group or send a survey to **3 to 5 CEB (Ceylon Electricity Board) Grid Planning Engineers**.
*   You ask them to review the curves based on their 20 years of experience managing the grid. If the CEB engineers officially state, *"Yes, based on our knowledge of human behavior, this evening peak looks highly plausible,"* you have achieved **Expert Face Validity**.

---

### Summary for your Thesis
To pass your defense, you will add a "Validation Methodology" section that states:
> *"Because ground-truth smart meter data is unavailable, this study employs a multi-faceted validation framework. The N-BEATSx forecasting engine is validated mathematically using Chronological Hold-Out testing scored by MAPE and RMSE. The underlying synthetic Monte Carlo profiles are validated using Heuristic Physics constraints, Surrogate Benchmarking against regional neighbors, and Expert Face Validity via consultation with CEB grid engineers."*
