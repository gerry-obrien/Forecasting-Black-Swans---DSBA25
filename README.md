# Forecasting Black Swans: The Fragility of "Normal" Forecasting

**Course:** Forecasting (M2 DSBA)  
**Project:** Project Idea - The Fragility of "Normal" Forecasting

## 📖 Project Overview

The core objective of this project is to demonstrate how and why standard forecasting models (built on the Normal distribution) fail in real-world financial contexts, and to implement a heavy-tailed alternative that provides a more robust risk assessment.

We base our narrative on the concepts of **"Black Swans"** and Taleb’s **"Fourth Quadrant"**—a domain where events are rare, consequential, and unpredictable by standard models.

**Thesis:** Classical time series analysis often assumes Normality ("First Quadrant") and is dangerously misleading when applied to real-world phenomena like finance that live in the "Fourth Quadrant".

---

## 📊 The Data

To test our hypothesis, we utilize a time series known for "fat tails" and volatility:

* ]**Dataset:** S&P 500 Daily Returns (Ticker: `^GSPC`).
* **Timeframe:** 2005 – Present.
* **Rationale:** This dataset covers major "Black Swan" clusters, specifically the **2008 Financial Crisis** and the **2020 COVID-19 Crash**.

---

## 🛠 Methodology

### 1. Exploratory Data Analysis (EDA)
We perform an EDA to prove that financial returns do not follow a Normal distribution:
* **Histogram:** Overlaid with a fitted Normal distribution to highlight the leptokurtic nature of the data (high peak, fat tails).
* **Q-Q Plot:** Used to visualize the "S" shape, confirming the existence of heavy tails.
* **The Extremogram:** Based on Davis & Mikosch (2009), we plot the extremogram to visualize "volatility clustering"—the phenomenon where extreme events are correlated (one crash follows another).

### 2. The Models
We compare two competing models forecasting the **99% Value-at-Risk (VaR)**.

#### Model A: The "Fragile" Classical Model (The Straw Man)
* **Type:** ARIMA(p,d,q)
* **Assumption:** Residuals follow a **Normal (Gaussian)** distribution.
* **Hypothesis:** This model will underestimate risk during crises.

#### Model B: The "Robust" Heavy-Tailed Model (The Hero)
* **Type:** ARIMA(p,d,q)-GARCH(1,1)
* **Assumption:** Residuals follow a **Student's t-distribution**.
* **Mechanism:** The ARIMA component models the mean, while the GARCH component models the variance (volatility) adaptively. The t-distribution accounts for heavy tails.

---

## ⚔️ The Showdown: Backtesting Experiment

We perform a **rolling window backtest** (starting with a 1000-day training window) to forecast the 1-day-ahead 99% VaR.

**Evaluation Metrics:**
* **Visual Inspection:** Comparing the VaR threshold (blue/red lines) against actual returns (grey) during the 2008 and 2020 crashes.
* **The "Killer Stat" (Breach Rate):** We count how often actual losses exceed the predicted VaR.
    * *Expectation:* A perfect model should be breached ~1% of the time.
    * *Failure Condition:* If the Normal model is breached 5-8% of the time, it is deemed "fragile".

---

## 🚀 Results & Conclusion

By comparing these models, we aim to show that:
1.  The Normal model systematically fails during crises, with a breach rate far higher than the expected 1%.
2.  The GARCH-t model "adapts" by widening its risk estimates during volatility, resulting in a breach rate much closer to the target.

**Conclusion:** Naively assuming a "Normal" world makes forecasters fragile to Black Swans. Heavy-tailed approaches (GARCH-t) do not predict the event itself, but they offer robustness and adaptability when the event unfolds.

---

## 📚 References
* **Resource 1 & 2:** Davis & Mikosch (2009) - *The Extremogram*.
* **Resource 3 & 4:** Works by Nassim Nicholas Taleb (Black Swans, Fourth Quadrant).
