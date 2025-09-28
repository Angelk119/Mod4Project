# Bike Sharing Analysis — Evening Commuter Ridership Experiment

## Business Framing & Stakeholders
The product team launched a small app feature on **2012-09-01** aimed at increasing **commuter-hour ridership (5–7 PM) on working days when weather is good**.  
Key stakeholders:
- **Product Managers** — need to know if the feature drove meaningful engagement.  
- **Operations/City Planners** — interested in capacity planning if evening traffic grows.  
- **Data Science & Analytics** — ensuring results are statistically and practically sound.  

---

## Methods Summary
- **EDA (Exploratory Analysis):**
  - Examined seasonality, hourly usage, and weather effects.  
  - Compared registered vs. casual rider patterns.  
- **A/B Design:**
  - **Group A (Pre):** 2012-08-04 → 2012-08-31.  
  - **Group B (Post):** 2012-09-01 → 2012-09-28.  
  - Eligibility: working day, hr ∈ {17,18,19}, weather ∈ {clear/mist}, humidity ≤ 0.70.  
  - Stratified balance by **weekday × hour** ensured fairness.  
- **Statistical Tests:**
  - Welch’s *t*-test for primary metric (average rides/hour).  
  - Confidence intervals via `statsmodels`.  
  - Guardrail metrics tracked (registered vs. casual mix, weather conditions).  

---

## Visual Summary

  <p align="center">
  <img src="https://github.com/user-attachments/assets/235a5f03-3278-4fda-9ff8-a09c5552f307" alt="Hourly ridership pattern" width="500"/>
  <br>
  <em>Figure 1. Average hourly rides by working vs non-working day</em>
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/f4809495-fffd-4a8f-85ac-5a7df0b0b59a" alt="Pre vs Post commuter rides" width="500"/>
  <br>
  <em>Figure 2. Pre vs Post launch average rides during 17:00–19:00 (good weather, working days)</em>
</p>

---

## Top 3 Trends & Insights
1. **Evening commuter rides are strongly concentrated at 8 AM and 5–6 PM peaks.**  
   → Confirms product focus on evening commuter slots is well-placed.  
2. **Registered riders dominate evening traffic, while casual riders peak on weekends.**  
   → Suggests the feature should mainly target registered commuter needs.  
3. **Weather and season play a large role in ride volume.**  
   → Guardrails are necessary to separate product effects from external variation.  

---

## Results from Hypothesis Tests
**Primary Metric (avg hourly rides, 17:00–19:00, working days, good weather):**  
- Pre mean = **744.8**, Post mean = **788.6**  
- Diff (Post − Pre) = **+43.8 rides/hour**  
- Welch *t* = 1.57, two-tailed *p* = **0.121**  
- 95% CI = [−11.7, +99.3]  
- **Decision:** Fail to reject H₀ at α=0.05 (not statistically significant).  
- **Practical Significance:** Yes (increase > +5 rides/hour).  

**Guardrails:**  
- Registered riders ↑ (640 → 701), casual riders ↓ (104 → 88).  
- Slight ↑ in humidity and ↓ in temperature observed.  
- No strong evidence of harm, but weather differences may confound results.  

---

## Ethics & Limitations
- **Observational design:** While stratified balancing improves fairness, external factors (e.g., weather shifts, calendar effects) may bias results.  
- **Sample size:** Only 46 eligible slots in each group after balancing → limited power.  
- **Assumptions:** Welch’s *t*-test assumes independent samples and approximate normality.  
- **Equity:** Shifts in ridership composition (fewer casual riders) may raise concerns about inclusivity.  
- **Recommendation:** Iterate with a longer test window or controlled experiment before scaling decisions.  

---
