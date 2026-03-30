# 📈 NIFTY 50 Options — Volatility Analysis & SABR Calibration

---

## Overview

This project provides a comprehensive framework for analysing the **volatility surface** of NIFTY 50 index options. Starting from raw NSE option chain data, it constructs the implied volatility (IV) smile, examines term-structure and skew dynamics, and calibrates the **SABR stochastic volatility model** to extract market-implied risk asymmetry — all with direct relevance to trading and hedging strategies.

---

## Key Features

| Module | Description |
|---|---|
| **Data Ingestion** | Fetches / processes live or historical NSE option chain snapshots |
| **IV Extraction** | Black–Scholes inversion to derive implied volatility per strike |
| **Smile Construction** | Strike-wise IV curves across multiple expiries |
| **Skew Analysis** | Put–call skew, risk-reversal, and butterfly metrics |
| **SABR Calibration** | Parameter fitting (α, β, ρ, ν) via non-linear least squares |
| **Surface Visualisation** | 3-D volatility surface and 2-D smile plots |
| **Strategy Insights** | Vol-based signals for directional & hedging decisions |

---

## Methodology

### 1 · Implied Volatility Smile
Black–Scholes IV is inverted numerically (Brent's method / Newton–Raphson) for each option strike. The resulting smile reveals market-priced skew and convexity that flat-vol models miss.

### 2 · Skew & Risk Asymmetry
- **Put skew** — elevated IV on OTM puts reflects tail-risk demand  
- **Risk-reversal** — 25Δ RR captures directional sentiment  
- **Butterfly** — 25Δ fly measures excess kurtosis / vol-of-vol premium  

### 3 · SABR Model Calibration
The SABR model (Hagan et al., 2002) is calibrated to match the market smile:

$$dF = \alpha F^\beta \, dW_1, \quad d\alpha = \nu \alpha \, dW_2, \quad \langle dW_1 dW_2 \rangle = \rho \, dt$$

Calibration minimises the RMSE between model-implied and market-implied vols across strikes.

---

## Project Structure

```
nifty-options-volatility-analysis/
├── data/
│   ├── raw/                  # Raw NSE option chain CSVs
│   └── processed/            # Cleaned, enriched datasets
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_iv_extraction.ipynb
│   ├── 03_smile_construction.ipynb
│   ├── 04_sabr_calibration.ipynb
│   └── 05_strategy_insights.ipynb
├── src/
│   ├── black_scholes.py      # BS pricing & IV inversion
│   ├── sabr.py               # SABR model & calibration
│   ├── skew_metrics.py       # Risk-reversal, butterfly, skew
│   └── visualisation.py      # Plotting utilities
├── requirements.txt
└── README.md
```

---

## Quickstart

```bash
# 1. Clone the repo
git clone https://github.com/anujpanwarma2024/nifty-options-volatility-analysis.git
cd nifty-options-volatility-analysis

# 2. Create & activate virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch Jupyter
jupyter notebook notebooks/
```

---

## Results & Insights

- Persistent **negative skew** in NIFTY options confirms asymmetric downside hedging demand.  
- SABR calibration achieves < 0.5 vol-point RMSE across strikes for near-term expiries.  
- Elevated **vol-of-vol (ν)** near earnings/budget events — actionable for straddle/strangle sizing.  
- Term-structure inversion ahead of major macro events provides early-warning signals.

---

## References

- Hagan, P. S. et al. (2002). *Managing Smile Risk.* Wilmott Magazine.  
- Black, F. & Scholes, M. (1973). *The Pricing of Options and Corporate Liabilities.*  
- NSE India — Option Chain Data: [nseindia.com](https://www.nseindia.com)

---

## Author

**Anuj Panwar** · [GitHub](https://github.com/anujpanwarma2024)

---

*This project is for educational and research purposes only. Nothing herein constitutes financial advice.*
