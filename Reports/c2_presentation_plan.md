# Component 2: Presentation Master Plan (Detailed Academic Defense)

**Time Strategy (4 Minutes):** You have 10 slides. To fit within 4 minutes, you must spend exactly **24 seconds per slide**. Do not read the slides word-for-word; the slides are there to prove your *theoretical rigor* to the panel, while your voice tells the story.

---

### Slide 1
*   **Slide Title:** Component 2: 24-Hour EV Charging Demand Profile Generation & Forecasting
*   **Visual:** Your picture (right), Component Title (left).
*   **Slide Text (Core Novelties):**
    *   **Data-Scarce Methodology:** A novel framework combining OpenStreetMap GIS data with primary stochastic modeling to bypass the lack of historical smart-meter data.
    *   **Context-Aware Deep Learning:** First study training an interpretable N-BEATSx neural network on synthetic Monte Carlo profiles to extract highly interpretable trend/seasonality demand evolution.
    *   **Tropical Battery Degradation:** Integrating temperature-dependent EV battery degradation rates unique to the Sri Lankan climate.
*   **Speaker Notes:** *"Welcome to Component 2. The fundamental problem in Sri Lanka is a lack of historical charging data. My core novelty is a data-scarce methodological framework that generates highly accurate district-level profiles using GIS and Stochastic Modeling, and then forecasts the future using an interpretable Context-Aware Deep Learning AI."*

---

### Slide 2
*   **Slide Title:** Introduction & Background: The Developing Grid Crisis
*   **Visual:** Split screen. Grid stress image (left), text (right).
*   **Slide Text:**
    *   **The Global Issue:** Unmanaged EV adoption causes severe distribution transformer overloading.
    *   **The Sri Lankan Context:**
        *   Sri Lanka’s grid is heavily reliant on fossil fuels (coal/diesel) during the 6 PM - 10 PM peak.
        *   Western demand models rely on massive historical datasets (which Sri Lanka lacks).
        *   Western models fail to account for developing-grid constraints (e.g., 3-phase smart meter upgrade requirements for TOU shifting).
*   **Speaker Notes:** *"Globally, EVs stress power grids. But in Sri Lanka, we face a unique crisis. Our evening peak is powered by coal and diesel, meaning EV charging is currently not 'green'. Furthermore, Western forecasting models cannot be used here because we lack historical data, and those models completely ignore local constraints like the lack of 3-phase domestic electricity."*

---

### Slide 3
*   **Slide Title:** Identified Research Gaps in Current Literature
*   **Visual:** The Literature Comparison Table (from your Defense Report).
*   **Slide Text:**
    *   *(Insert Table comparing your work to 4 recent 2023/2024 papers)*
    *   **The Theoretical Gap:** Current literature either relies purely on historical data (Deep Learning) OR purely on statistical probability (Monte Carlo) without spatial intelligence.
    *   **The Proposed Solution:** A hybrid approach bridging Spatial GIS, Primary Behavior, and Deep Learning.
*   **Speaker Notes:** *"As seen in this table of 2023 and 2024 literature, a clear theoretical gap exists. Existing studies use either Monte Carlo or Deep Learning independently, but none of them combine open-source GIS with primary behavioral constraints—like 3-phase metering—specifically tailored for a developing nation."*

---

### Slide 4
*   **Slide Title:** Research Objectives
*   **Visual:** Target icon branching into three pillars.
*   **Slide Text:**
    *   **Primary Objective:** Develop a highly reproducible EV demand forecasting framework without historical charging data.
    *   **O1:** Map Spatial Typologies using OpenStreetMap (OSM) GIS data.
    *   **O2:** Extract behavioural parameters via structured primary data collection.
    *   **O3:** Synthesize demand using a parameterized Monte Carlo simulation.
    *   **O4:** Forecast long-term grid impact (2032-2035) using Context-Aware N-BEATSx.
*   **Speaker Notes:** *"My primary objective is to build a reproducible forecasting framework without historical data. To achieve this, I map the geography using GIS, extract the human behavior through primary data, synthesize the current demand via Monte Carlo, and forecast the future using N-BEATSx."*

---

### Slide 5
*   **Slide Title:** Spatial Typology Framework & GIS Mapping
*   **Visual:** A simple matrix showing Dwell-Time vs Power for the 4 Typologies.
*   **Slide Text:**
    *   **The 4 Typologies:** Urban Commercial, Suburban Residential, Tourist, Highway Transit.
    *   **Academic Justification:** Mathematically captures 100% of the EV charging behavioral spectrum (Dwell-Time vs. Power Demand).
    *   **GIS Integration:** Typologies deliberately map to specific OpenStreetMap (OSM) tags (e.g., Commercial = `landuse=commercial`) to enable automated spatial density extraction via GeoPandas.
*   **Speaker Notes:** *"How did we select our 4 typologies? First, they mathematically capture the entire behavioral spectrum of dwell-time and power demand. Second, I specifically designed them to map directly to OpenStreetMap land-use tags. This allows us to use GeoPandas to automatically extract the exact spatial density of every district in the country."*

---

### Slide 6
*   **Slide Title:** Methodology: Intersecting Three Knowledge Domains
*   **Visual:** A Venn Diagram of the 3 domains.
*   **Slide Text:**
    *   **Geospatial Analysis (GIS):** Utilizing *OpenStreetMap (OSM) & GeoPandas* to map land-use densities across 25 districts.
    *   **Stochastic Modeling:** Utilizing a *Vectorized Monte Carlo Engine* to mathematically simulate probability distributions (Lognormal, Beta, Poisson) for human charging behavior.
    *   **Deep Learning:** Utilizing the *N-BEATSx (Neural Basis Expansion Analysis)* architecture to perform multi-variate, context-aware forecasting.
*   **Speaker Notes:** *"Theoretically, my methodology bridges three domains. I use OpenStreetMap and GeoPandas for geospatial mapping. I use a customized Monte Carlo engine to process stochastic behavioral distributions. Finally, I use the N-BEATSx architecture for deep learning forecasting."*

---

### Slide 7
*   **Slide Title:** Validation Protocol
*   **Visual:** Two-tier diagram (AI vs Synthetic Data).
*   **Slide Text:**
    *   **AI Validation:** Hold-Out Testing (RMSE, MAPE).
    *   **Data Validation:** Heuristic Checks & CEB Expert Delphi Method (Face Validity).
*   **Speaker Notes:** *"Because we are generating synthetic data, validation is critical. The AI is validated mathematically using standard metrics like RMSE and MAPE. The synthetic district curves are physically validated by senior CEB engineers using the Delphi Method to ensure absolute face-validity before forecasting."*

---

### Slide 8 (CRITICAL SLIDE)
*   **Slide Title:** Primary Data Collection & Ethical Clearance
*   **Visual:** A large **QR Code** linking to your Google Form.
*   **Slide Text:**
    *   **Academic Methodology:** Stratified Purposive & Snowball Sampling.
    *   **Statistical Sample Size:** 160-200 EV Owners (>95% Confidence Level).
    *   **Data Extracted:** Target SoC, Arrival Time (Beta), Trip Distance (Lognormal), 3-Phase Meter Availability.
    *   **Ethical Clearance:** Complete data anonymization. No Personally Identifiable Information (PII) collected from respondents.
*   **Speaker Notes:** *"Because we lack historical data, this primary survey is the engine of the research. You can scan the QR code to see it. We use Stratified Purposive and Snowball sampling, targeting 160 to 200 EV owners, giving us a >95% Confidence Level. Crucially, all data undergoes strict ethical clearance, meaning absolutely no PII is collected and all behavioral data is fully anonymized."*

---

### Slide 9 (CRITICAL SLIDE)
*   **Slide Title:** Implementation: Bottom-Up Spatial Scaling
*   **Visual:** Diagram: [Survey Shape] x [OSM/DMT Scale] = [25 District Curves]
*   **Slide Text:**
    *   **Methodology:** Bottom-Up Spatial Scaling (Spatial Micro-Simulation).
    *   **Step 1 (The Shape):** The Monte Carlo engine processes the survey data to output 4 normalized probability curves (representing the 4 Typologies).
    *   **Step 2 (The Scale):** District Fleet Size (DMT Data) and District Typology Weights (OSM GIS Data) act as scaling multipliers.
    *   **Step 3 (The Generation):** `Typology Shape` × `District Fleet Size` × `OSM GIS Weights` = 25 Unique District-Level Demand Profiles (in MW).
    *   **Computational Scale:** Rigorous Convergence Test ($N^*$) executed across **3,300 simulation combinations** to output Low, Medium, and High adoption scenarios.
*   **Speaker Notes:** *"How do we generate 25 district curves without surveying all 25 districts? We use a globally recognized mathematical standard called Bottom-Up Spatial Scaling. The Monte Carlo engine generates the 'shape' of the curves from our survey data. Then, we use the GIS OpenStreetMap weights and DMT fleet size to 'scale' those curves. Finally, we run a rigorous statistical Convergence Test to execute exactly 3,300 simulation combinations, outputting Low, Medium, and High demand scenarios for the grid."*

---

### Slide 10
*   **Slide Title:** Implementation: Interpretable AI Forecasting
*   **Visual:** Flowchart (Curves ➡️ Augmentation ➡️ N-BEATSx ➡️ Trend/Seasonality).
*   **Slide Text:**
    *   **Data Augmentation:** Gaussian Noise & Time Jittering (Expanding 175 base curves to 1,750+ training sequences to prevent overfitting).
    *   **Model:** Context-Aware N-BEATSx.
    *   **Static Exogenous Inputs:** District ID, Typology, Fleet Size.
    *   **Forecast Output:** Mathematically interpretable `Trend Curve` (Y-o-Y growth) and `Seasonality Curve` (daily peak shape).
*   **Speaker Notes:** *"Finally, we augment those district curves using Gaussian noise to generate over 1,700 training sequences to prevent AI overfitting. We feed this into a Context-Aware N-BEATSx model, utilizing District IDs as exogenous inputs. The result is a highly interpretable forecast that outputs exactly how the grid demand trend and daily seasonality will evolve up to 2035. Thank you."*

---

### Slide 11 (Extra: System Architecture Diagram)
*   **Slide Title:** Component 2 System Architecture
*   **Visual:** A clean, left-to-right flowchart. Use 3 distinct colors for the 3 main phases (Inputs, Synthesis, Forecasting). Do not clutter the screen; use large boxes with clear arrows.
    *   *Block 1 (Left - The Inputs):* Two boxes stacked vertically. Top box: `Primary Survey Data (Behavioral Shape)`. Bottom box: `OSM & DMT Data (Spatial Scale)`. Both point to...
    *   *Block 2 (Middle - The Engine):* A large gear icon labeled `Vectorized Monte Carlo Simulation`. This points to...
    *   *Block 3 (Middle Right - The Link):* A box labeled `25 District Profiles + Gaussian Augmentation (1,750 Curves)`. This points to...
    *   *Block 4 (Right - The AI):* A brain/network icon labeled `Context-Aware N-BEATSx Engine`.
    *   *Final Output (Far Right):* `2035 Trend & Seasonality Forecast`.
*   **Slide Text:** Keep text minimal. Let the flowchart do the talking. Use standard arrow notation to show the data flow.
*   **Speaker Notes:** *"This diagram represents the complete data pipeline of Component 2. On the left, we ingest our primary survey data and GIS weights. These feed into the Monte Carlo engine in the center to generate synthetic district curves. Those curves are augmented and fed into the N-BEATSx forecasting engine on the right, which outputs our final 2035 trend predictions. It is a seamless flow from raw spatial data to deep learning forecasts."*
*   **Presenter Tip:** You can keep this as Slide 11 (Backup), or move it to **Slide 5** to give the panel a high-level "map" of your component before you explain the specific methodologies!
