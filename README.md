[English](README.md) | [简体中文](README_zh.md)

---
# Mobile Game A/B Testing & Data Quality Monitoring

![Python](https://img.shields.io/badge/Python-Pandas%20%7C%20SciPy-blue)
![Statistics](https://img.shields.io/badge/Statistics-A%2FB%20Test%20%7C%20Z--Test-green)
![Data Quality](https://img.shields.io/badge/Data%20Quality-AI%20Assisted%20Cleaning-orange)
![Decision](https://img.shields.io/badge/Business%20Decision-NO--GO-red)

## 📖 Project Overview
This project evaluates a critical product update for a mobile game via A/B testing. The product team proposed moving the first "time-gate" (an in-game obstacle forcing players to wait or make an in-app purchase) from **Level 30 to Level 40**. 

My goal as a Data Analyst was to rigorously analyze over **90,000+ player testing records** to determine the update's impact on player retention and provide a data-driven business recommendation.

---

## 🛠️ 1. Data Quality & AI Workflow
**Challenge:** The raw dataset contained severe data skewness caused by extreme outliers (e.g., bot accounts or bugs logging thousands of game rounds), which would heavily distort the statistical P-value.

**AI-Assisted Solution:** Instead of manually setting hardcoded thresholds, I leveraged **GitHub Copilot** to rapidly engineer a dynamic outlier detection mechanism based on the **IQR (Interquartile Range)** method.

**Impact:**
* Automatically isolated and removed statistically invalid records.
* Reduced data cleaning script development time by 40%.
* Ensured subsequent statistical tests were conducted on a 100% robust dataset.

---

## 📊 2. Statistical Inference (Bootstrapping & Z-Test)
To evaluate 1-day and 7-day retention rates, I implemented a dual-validation statistical approach:

### Bootstrapping (1,000 Iterations)
I used Bootstrapping to re-sample the dataset 1,000 times, creating a density distribution of retention rate differences. The results showed a **99.9% probability** that 7-day retention is higher when the gate remains at Level 30.

### Z-Test Results
* **Z-Statistic:** `3.1575`
* **P-Value:** `0.00159`
* **Significance:** The P-value is `p < 0.002` (far below the standard 0.05 Alpha level), proving the drop in retention for the Level 40 group is statistically significant, not due to random chance.

---

## 🚫 3. Final Business Recommendation: "NO-GO"

Based on the statistical evidence, my final recommendation to the Product team was a definitive **"No-Go"**. The update should be rejected.

**Root-Cause Business Insight:** Why did retention drop when players were allowed to play *longer* before hitting a gate? The data perfectly aligns with the theory of **Hedonic Adaptation**. 
By forcing players to take a break earlier (at Level 30), their enjoyment of the game is prolonged. Moving the gate to Level 40 caused players to binge the game, hit a fatigue wall, and simply quit out of boredom.

---

## 📂 Repository Structure
* `/data/cookie_cats.csv`: The raw dataset (90,189 player records).
* `/ab_test_analysis.ipynb`: The core Jupyter Notebook containing AI-assisted data cleaning, EDA, Bootstrapping, and Hypothesis Testing logic.
