# Forecasting Black Swans: The Fragility of "Normal" Forecasting

**Course:** Forecasting (M2 DSBA)  
**Project:** Project Idea - The Fragility of "Normal" Forecasting

## 📖 Project Overview

[cite_start]The core objective of this project is to demonstrate how and why standard forecasting models (built on the Normal distribution) fail in real-world financial contexts, and to implement a heavy-tailed alternative that provides a more robust risk assessment[cite: 1, 2].

[cite_start]We base our narrative on the concepts of **"Black Swans"** and Taleb’s **"Fourth Quadrant"**—a domain where events are rare, consequential, and unpredictable by standard models[cite: 8].

> [cite_start]**Thesis:** Classical time series analysis often assumes Normality ("First Quadrant") and is dangerously misleading when applied to real-world phenomena like finance that live in the "Fourth Quadrant"[cite: 9].

---

## 📊 The Data

To test our hypothesis, we utilize a time series known for "fat tails" and volatility:

* [cite_start]**Dataset:** S&P 500 Daily Returns (Ticker: `^GSPC`)[cite: 12].
* [cite_start]**Timeframe:** 2005 – Present[cite: 14].
* [cite_start]**Rationale:** This dataset covers major "Black Swan" clusters, specifically the **2008 Financial Crisis** and the **2020 COVID-19 Crash**[cite: 15].

---

## 🛠 Methodology

### 1. Exploratory Data Analysis (EDA)
We perform an EDA to prove that financial returns do not follow a Normal distribution:
* [cite_start]**Histogram:** Overlaid with a fitted Normal distribution to highlight the leptokurtic nature of the data (high peak, fat tails)[cite: 20, 21].
* [cite_start]**Q-Q Plot:** Used to visualize the "S" shape, confirming the existence of heavy tails[cite: 22, 23].
* [cite_start]**The Extremogram:** Based on Davis & Mikosch (2009), we plot the extremogram to visualize "volatility clustering"—the phenomenon where extreme events are correlated (one crash follows another)[cite: 24, 25, 27].

### 2. The Models
[cite_start]We compare two competing models forecasting the **99% Value-at-Risk (VaR)**[cite: 29, 51].

#### Model A: The "Fragile" Classical Model (The Straw Man)
* **Type:** ARIMA(p,d,q)
* **Assumption:** Residuals follow a **Normal (Gaussian)** distribution.
* [cite_start]**Hypothesis:** This model will underestimate risk during crises[cite: 30, 33].

#### Model B: The "Robust" Heavy-Tailed Model (The Hero)
* **Type:** ARIMA(p,d,q)-GARCH(1,1)
* **Assumption:** Residuals follow a **Student's t-distribution**.
* [cite_start]**Mechanism:** The ARIMA component models the mean, while the GARCH component models the variance (volatility) adaptively[cite: 39, 40]. [cite_start]The t-distribution accounts for heavy tails[cite: 42].

---

## ⚔️ The Showdown: Backtesting Experiment

[cite_start]We perform a **rolling window backtest** (starting with a 1000-day training window) to forecast the 1-day-ahead 99% VaR[cite: 47, 49, 51].

**Evaluation Metrics:**
* [cite_start]**Visual Inspection:** Comparing the VaR threshold (blue/red lines) against actual returns (grey) during the 2008 and 2020 crashes[cite: 64].
* **The "Killer Stat" (Breach Rate):** We count how often actual losses exceed the predicted VaR.
    * *Expectation:* A perfect model should be breached ~1% of the time.
    * [cite_start]*Failure Condition:* If the Normal model is breached 5-8% of the time, it is deemed "fragile"[cite: 68].

---

## 🚀 Results & Conclusion

By comparing these models, we aim to show that:
1.  [cite_start]The Normal model systematically fails during crises, with a breach rate far higher than the expected 1%[cite: 65].
2.  [cite_start]The GARCH-t model "adapts" by widening its risk estimates during volatility, resulting in a breach rate much closer to the target[cite: 66, 69].

**Conclusion:** Naively assuming a "Normal" world makes forecasters fragile to Black Swans. [cite_start]Heavy-tailed approaches (GARCH-t) do not predict the event itself, but they offer robustness and adaptability when the event unfolds[cite: 71, 72].

---

## 📚 References
* [cite_start]**Resource 1 & 2:** Davis & Mikosch (2009) - *The Extremogram*[cite: 24].
* [cite_start]**Resource 3 & 4:** Works by Nassim Nicholas Taleb (Black Swans, Fourth Quadrant)[cite: 7].
