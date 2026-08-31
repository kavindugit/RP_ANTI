# Statistical Sample Size Study (Primary Data)

You asked two very important methodological questions: 
1. What exact sampling method are we using?
2. Are 40 samples per typology *really* enough, mathematically?

Here is the exact statistical study and explanation you need to defend this to your PhD panel.

## 1. The Sampling Methodology
In your research, you are using a hybrid of two highly respected, standard sampling methods:
*   **Stratified Purposive Sampling:** You are "stratifying" (dividing) the population into 4 distinct groups (the Typologies). You are then "purposively" targeting specific people for each group (e.g., targeting hotel managers for T4, and office workers for T1). 
*   **Snowball Sampling:** Because EV owners are a "hard-to-reach" minority population in Sri Lanka, you will use snowball sampling. This means you will ask your initial survey respondents (e.g., in the "EV Sri Lanka" Facebook group) to forward the survey to other EV owners they know. 
> **Defense Statement:** *"Due to the data-scarce nature of the Sri Lankan EV population, a Stratified Purposive approach was utilized to guarantee representation across all 4 typologies, supplemented by Snowball Sampling to overcome the hard-to-reach nature of the demographic."*

## 2. Is 40-50 Samples Per Typology Enough? (The Math)
It is completely normal to feel like 40 is a small number! But in statistics, **sample size is dictated by math, not feelings.** 

Here are the two mathematical proofs that 160-200 total respondents (40-50 per typology) is more than enough for your PhD:

### Proof A: The Central Limit Theorem (CLT)
The standard statistical rule for parameterizing probability distributions (like we are doing for the Monte Carlo simulation) is the **Central Limit Theorem (CLT)**.
The CLT states that to accurately estimate the mean of a population and assume a normal distribution, a minimum sample size of **$n \ge 30$** per stratum (group) is required.
*   By targeting 40-50 per typology, you comfortably exceed the $n=30$ threshold required by the CLT.

### Proof B: Confidence Interval Equation (Cochran's Formula)
Let's look at the entire EV population of Sri Lanka. There are approximately 5,000 active EVs currently on the road.
If we want a **95% Confidence Level** with a **10% Margin of Error**, we use Cochran's formula:
$n = \frac{Z^2 \times p(1-p)}{e^2}$
*   $Z$ (for 95% confidence) = 1.96
*   $p$ (estimated variance) = 0.5
*   $e$ (margin of error) = 0.10
*   **Math:** $n = \frac{1.96^2 \times 0.25}{0.10^2} = 96$

**Conclusion:** To achieve a 95% statistical confidence level for the *entire country of Sri Lanka*, you only need **96 total respondents**. By targeting **160-200 total respondents** (40-50 per typology), your data will actually have a margin of error closer to **7%**, which is incredibly strong for a PhD thesis in a developing nation.

## 3. The Verdict
You DO NOT need 5,000 respondents. 
*   **Method:** Stratified Purposive + Snowball Sampling.
*   **Target:** 160–200 total responses (40-50 per typology).
*   **Justification:** Exceeds the CLT minimum ($n \ge 30$) and provides a >95% Confidence Level for the Sri Lankan EV population. 

I will now update your presentation plan to ensure these exact statistical terms are ready for you to use!
