# Technical Report: The Mathematics of N-BEATSx

You asked to understand the "complex math problem" behind N-BEATSx before making your final decision. To understand why N-BEATSx is harder to implement than an LSTM, we must look at how both AI models handle **Context Variables** (like District ID and Fleet Size).

---

## 1. How LSTM handles Context Variables (The Easy Way)
In an LSTM, data is processed chronologically, step-by-step. If you want to tell the LSTM that the current curve belongs to Colombo (District 1) and has 5,000 EVs, you simply **concatenate** (glue together) the numbers.

*   **LSTM Input Vector:** `[245 kW, District_1, 5000 EVs]`
*   **The Math:** The LSTM just treats `District_1` as another number in its standard matrix multiplication: $h_t = \sigma(W_x X_t + W_h h_{t-1} + b)$. 
*   **Difficulty:** Extremely simple. You just add columns to your excel sheet.

---

## 2. The Core Math of N-BEATS (The Interpretable Way)
N-BEATS does not look at data step-by-step. Instead, it uses **Basis Expansion Analysis**. 
It assumes that any complex curve can be mathematically broken down into two pure equations:
1.  **Trend (Polynomials):** $y = at^2 + bt + c$ (This captures the slow, multi-year growth of EV adoption).
2.  **Seasonality (Fourier Series):** $y = A \sin(\omega t) + B \cos(\omega t)$ (This captures the 24-hour daily peak cycles).

Instead of predicting the next hour's kW value, **N-BEATS predicts the coefficients** ($a, b, c$ and $A, B$). It draws the perfect trend line, draws the perfect daily cycle, and adds them together to get the final forecast. 

> [!TIP]
> This is why N-BEATS is "interpretable." You can literally print out the polynomial equations it used to draw the forecast.

---

## 3. The "Complexity": Enter N-BEATSx
The original N-BEATS was **univariate**—it only looked at historical kW values. 
To add our Context Variables (District ID, Fleet Size), researchers had to invent **N-BEATSx** (N-BEATS with Exogenous variables). 

Because N-BEATS operates by predicting polynomial and Fourier coefficients, you cannot simply "glue" the District ID to the input. 
Instead, the neural network must be fundamentally redesigned so that the **Context Variables directly influence the basis coefficients**.

**The Mathematical Problem:**
The N-BEATSx architecture must project the exogenous variables (District ID) into a shared mathematical space with the historical kW data, *before* passing them into the Trend and Seasonality stacks. 
*   **The Equation:** The model must learn a mapping function where $f(\text{District, Fleet Size})$ modifies the $a, b, c$ coefficients of the Trend block. 
*   **In Plain English:** The AI has to learn the complex calculus of how being in "Colombo" physically bends the polynomial growth curve, rather than just treating "Colombo" as a static label.

---

## 4. Implementation Reality (Coding it in Python)
If you had to write the calculus for N-BEATSx from scratch using raw PyTorch, it would take months. It is highly advanced math.

However, the good news is that in 2026, you do not have to write the calculus from scratch. Advanced Python libraries like **Nixtla's `NeuralForecast`** or **`Darts`** have pre-built the N-BEATSx architecture.

**The actual challenge for you:**
While the library handles the internal calculus, **formatting your data** to feed into an N-BEATSx model is incredibly strict. 
Unlike LSTM where you just pass a 3D tensor `(samples, timesteps, features)`, N-BEATSx requires you to strictly separate your variables into:
1.  *Target series* (The 24h kW curves)
2.  *Historical Exogenous series* (Variables that change over time)
3.  *Static Exogenous series* (Variables that never change, like District ID).

If you make a single mistake in how you structure the data arrays (e.g., misaligning the dimensions of the Static variables with the Target variables), the complex internal math will crash with dimension errors that are notoriously difficult to debug.

### Summary Verdict
*   **The Math:** N-BEATSx uses advanced polynomial/Fourier basis expansion instead of simple matrix multiplication. It forces the exogenous variables (Districts) to mathematically bend the trend lines.
*   **The Code:** You don't write the math, but formatting the Python arrays to satisfy the math is much harder and stricter than an LSTM.
*   **Is it worth it?** Yes. If you can get the Python arrays formatted correctly, the interpretable output (showing the pure trend vs seasonality) will make your PhD thesis significantly more impressive than a "Black Box" LSTM.
