[English](README.md) | [简体中文](README_zh.md)

---

# Mobile Game A/B Testing Analysis

![Python](https://img.shields.io/badge/Python-Pandas%20%7C%20SciPy-blue)
![Statistics](https://img.shields.io/badge/Statistics-A%2FB%20Test%20%7C%20Z--Test-green)
![Data Quality](https://img.shields.io/badge/Data%20Quality-AI%20Assisted%20Cleaning-orange)
![Decision](https://img.shields.io/badge/Business%20Decision-NO--GO-red)

## 📖 Project Background
This project evaluates an in-game progression update via A/B testing. The product team proposed moving the game's first "time-gate" (an obstacle forcing players to wait) from **Level 30 to Level 40**. 

As a Data Analyst, I analyzed over **90,000 player records** to assess the update's actual impact on user retention and provide a data-driven business recommendation.

---

## 1. Data Cleaning & Outlier Handling
**Issue:** The raw dataset contained extreme outliers (e.g., bot accounts logging thousands of game rounds), which would skew the P-value of our hypothesis testing.

**Solution:** To avoid manually hardcoding thresholds, I used **GitHub Copilot** to assist in writing an automated outlier removal script based on the **IQR (Interquartile Range)** method.

**Results:**
* Automatically removed invalid samples.
* Improved script development efficiency by ~40%.
* Ensured the reliability of the subsequent statistical tests by working with a clean dataset.

---

## 2. Retention Analysis (Bootstrapping & Z-Test)
To evaluate 1-day and 7-day retention rates, I cross-validated the results using two statistical methods:

### Bootstrapping (1,000 Iterations)
By resampling the dataset 1,000 times with replacement, we observed the distribution of retention rate differences. The results showed a **99.9% probability** that 7-day retention is higher when the gate remains at Level 30.

### Two-Sample Z-Test
* **Z-Statistic:** `3.7041`
* **P-Value:** `0.00021`
* **Conclusion:** The P-value is `p < 0.001` (well below the standard 0.05 significance level). This indicates that the drop in retention for the Level 40 group is statistically significant, not just random noise.

---

## 3. Conclusion & Recommendation: NO-GO

Based on the data, I recommended that the product team **reject this update** and keep the gate at Level 30.

**Reasoning:** Why did retention drop when players were allowed to play longer before hitting an obstacle? This aligns with the theory of **Hedonic Adaptation**. Forcing players to take a break at Level 30 prolongs their enjoyment and anticipation. Moving the gate to Level 40 caused players to binge the game early on, hit a fatigue wall, and quit out of boredom.

---

## Repository Structure
* `/data/cookie_cats.csv`: The raw dataset (90,189 player records).
* `/ab_test_analysis.ipynb`: The core analysis notebook (contains outlier cleaning, EDA, Bootstrapping, and Hypothesis Testing logic).
