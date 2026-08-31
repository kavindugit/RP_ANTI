# Evaluation Report: Component 2 - EV Charging Demand Modelling

**Component Lead:** Herath H M K M  
**Focus:** District-level hourly and seasonal EV charging demand modelling using behavioural simulation and deep learning.

---

## 1. Overall Verdict
Component 2 is an **exceptionally strong research proposal** with high academic and practical value. It tackles a well-known problem in EV infrastructure planning (demand forecasting) but introduces a highly novel approach designed specifically for data-scarce, developing-country contexts. The methodology is robust, blending statistical simulation with advanced machine learning, and it perfectly bridges the gap between Component 1 (vehicle adoption) and Components 3 & 4 (grid constraints and spatial placement).

## 2. Research Value & Novelty (Is it good?)
**High Research Value.** Your component addresses a critical blind spot in current literature:
*   **The Data Scarcity Problem:** Most existing EV charging models rely on historical charging session data from smart meters or extensive public charging networks. Developing nations like Sri Lanka do not have this data yet. Your approach of using **Monte Carlo simulation calibrated with demographic priors** to generate synthetic data is a highly valuable methodological contribution that other researchers in similar countries can adopt.
*   **Contextualizing International Data:** Directly applying ACN-Data (US-based) to Sri Lanka would yield inaccurate results because driving habits, vehicle types, and battery sizes differ wildly. Your plan to "re-weight" or calibrate this data using Sri Lankan behavioural parameters (shorter commutes, income constraints, different battery profiles) is a brilliant way to leverage open datasets while maintaining local validity.
*   **Spatio-Temporal Granularity:** Providing district-resolved, seasonally stratified (wet vs. dry season) hourly demand curves is a massive step up from national-level aggregate forecasts, offering practical utility for real-world grid operators.

## 3. Feasibility in Sri Lanka (Is it doable?)
**Highly Feasible, with Specific Manageable Risks.**

| Aspect | Feasibility | Comments & Mitigation Strategies |
| :--- | :--- | :--- |
| **Open Datasets** | **High** | ACN-Data and UK datasets are publicly available and easily accessible. |
| **Local Calibration Data** | **Medium-High** | Census data and fuel prices are available via the CBSL and Dept of Census and Statistics. The **EV Owner Survey** is the biggest bottleneck. *Risk Mitigation:* Since Sri Lanka's current EV population is small (mostly Nissan Leafs and newer Chinese imports), getting a massive sample size will be hard. You should aim for a statistically acceptable sample (e.g., 100-200 respondents) and rely heavily on secondary data (e.g., average commute lengths from existing transport studies) to fill gaps. |
| **Computational Feasibility** | **High** | Monte Carlo simulations and training BiLSTM/Transformer models can be executed on modern personal computers or free cloud tiers (like Google Colab). |
| **Validation Data (CEB)** | **Medium** | Validating against CEB load data requires CEB to share hourly load profiles. *Risk Mitigation:* If CEB is reluctant to share highly granular data, you can validate against aggregated publicly available load curves from the CEB Statistical Digest, or use ACN holdout sets as your primary quantitative validation. |

## 4. Key Strengths of the Approach
*   **Hybrid Methodology:** Combining physics/behaviour-based simulation (Monte Carlo) with data-driven forecasting (Transformers/BiLSTM) gives you the "best of both worlds." The simulation provides the data, and the deep learning models learn the complex, non-linear temporal dependencies.
*   **Interoperability:** Your outputs are structured perfectly to act as the "engine" for the rest of the group. You take Component 1's numbers and turn them into power (kW/MW) load curves, which Components 3 and 4 desperately need.

## 5. Recommendations for Enhancing the Research
To make your research even more robust, consider addressing the following in your thesis or implementation:
1.  **Vehicle Classes (Crucial for Sri Lanka):** Make sure your simulation explicitly accounts for **Electric 2-wheelers (motorcycles) and 3-wheelers (tuk-tuks)**. In South Asia, the electrification of 2/3-wheelers will likely happen faster than 4-wheelers. Their battery capacities (e.g., 2-5 kWh) and charging behaviours (swapping vs. plug-in, 13A home socket vs. fast charger) are very different from a 40kWh Nissan Leaf. Addressing this will significantly boost the novelty of your research.
2.  **Time-of-Use (TOU) Tariffs:** Sri Lanka's CEB heavily utilizes TOU tariffs (Off-peak, Day, Peak). Your simulation *must* include a probability variable that models users shifting their charging to off-peak hours (10:30 PM - 5:30 AM) to save money. This is a massive driver of charging behaviour in income-constrained environments.
3.  **Transformer vs. BiLSTM Comparison:** In your methodology, clearly justify *why* you are comparing Transformers and BiLSTMs against ARIMA. Transformers are excellent for long-sequence attention, which is great for capturing both daily and seasonal seasonality simultaneously.

## Conclusion
Your component is incredibly solid. It has high academic merit because it solves the "missing data" problem for EV forecasting in developing nations, and it has high practical merit because the output is exactly what utility companies (like CEB) need to prevent grid collapse. With careful execution of the behavioural survey and inclusion of local nuances like TOU tariffs and 2/3-wheelers, this could easily result in a high-impact journal publication.
