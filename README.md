# Valuation-Based Contrarian Trading Strategy
This repository presents a valuation-driven, mean-reversion trading strategy applied to **NVIDIA (NVDA)** stock, using its **Price-to-Earnings (P/E) ratio** as a valuation anchor. The strategy employs **Kalman filtering** and a **Quasi-Fisher transformation** to smooth and normalize valuation signals and uses a **dual-threshold system** to generate long and short trades. It aims to exploit behavioral mispricings in high-volatility, sentiment-driven markets.

## 🧠 Strategy Overview

This contrarian trading model is built on the principle that extreme P/E valuations often indicate overreaction by investors. The model:
- Goes **long** when the Kalman-filtered, Quasi-Fisher transformed P/E ratio falls below a rolling lower threshold (undervaluation).
- Goes **short** when the transformed P/E ratio exceeds a rolling upper threshold (overvaluation).
- Exits positions based on secondary inner thresholds or stop-loss rules.
- Requires **two consecutive threshold crossings** to trigger trade execution, reducing noise.

---

## 📊 Dataset

- **Price Data**: Daily closing prices of NVIDIA from **Yahoo Finance**.
- **Fundamentals**: Monthly trailing twelve-month (TTM) P/E ratio from **Bloomberg**.
- Data resampled to **monthly frequency** to align indicators and manage volatility.

---

## 🔧 Methodology & Implementation

### 📌 Key Steps:
1. **Data Preprocessing**:
   - Merged daily price and monthly P/E data.
   - Resampled both to monthly frequency.

2. **Feature Engineering**:
   - Applied **Quasi-Fisher Transformation** to normalize P/E ratio.
   - Smoothed with a **Kalman Filter** to reduce high-frequency noise.

3. **Thresholds & Signal Logic**:
   - Used **rolling maxima/minima** to set dynamic outer (U1, L1) and inner (U2, L2) thresholds.
   - Trades executed only after **two consecutive signals** to reduce false positives.
   - Incorporated a **10% stop-loss** to minimize downside risk.

4. **Hyperparameter Tuning**:
   - Performed **grid search** on U1/L1 thresholds with returns, drawdown, Sharpe as metrics.
   - Visualized performance with **heatmaps** to select optimal parameters.

5. **Walk-Forward Optimization**:
   - Re-optimized thresholds **annually** to adapt to changing market regimes.
   - Enabled robust performance over different volatility regimes.

6. **Benchmark Comparison**:
   - Strategy compared to a **Buy-and-Hold baseline**.
   - Metrics included: Cumulative Return, Max Drawdown, Sharpe Ratio, Sortino Ratio, Alpha/Beta, ROA, CCROR.

---

## 📈 Results Summary

| Metric                      | Contrarian Strategy | Buy-and-Hold |
|----------------------------|---------------------|--------------|
| Annualized Return          | –0.52%              | –26.69%      |
| Max Drawdown               | –97.75%             | –99.81%      |
| CCROR                      | –8.52%              | –99.48%      |
| Sharpe Ratio               | –0.0601             | –0.7313      |
| Sortino Ratio              | –0.1146             | –1.3952      |
| Alpha                      | +0.003              | –0.0185      |
| Beta                       | –0.0222             | –0.3731      |
| ROA (Capital Preserved)    | 93.6%               | 0.52%        |

📌 **Directional accuracy** of signals passed binomial forecast tests at 5% significance.

---

## 📌 Visualizations

- Signal overlays on Kalman-filtered P/E ratios and price
- Buy/sell points with arrows on price charts
- Cumulative returns over time vs. Buy-and-Hold
- Annual evolution of optimized hyperparameters (U1, U2, L1, L2)
- Heatmap of return performance across threshold combinations

---

## 🛠️ Technologies Used

- **Python** (Pandas, NumPy, Matplotlib, Statsmodels)
- **Kalman Filtering** (Custom implementation via state-space model)
- **Jupyter Notebook** for EDA and testing
- **Yahoo Finance API**, Bloomberg (manual data export)

---

## 🚀 Future Work

- Compare with **momentum-based** strategies and other fundamental indicators (e.g., EV/EBITDA).
- Test without inner thresholds to evaluate uncapped gain potential.
- Apply to other sentiment-driven, high-volatility stocks.
- Incorporate **macroeconomic signals** or VIX as regime filters.

---

## 👩‍💻 Authors

- Kanupriya Parashar  
- Nicholas Pelonis  
- Akshita Khajuria  
- Raghavi Rajumojan  

---

## 📜 License

This project is for educational purposes under UCLA's Econ 409 course. All data and research methods are original unless cited otherwise.

---
