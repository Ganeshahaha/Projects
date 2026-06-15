# Risk-Profiled Stock Portfolio Recommender & Forecasting Tool

A Python-based investment analysis tool that segments investors by risk profile and generates tailored, diversified stock portfolio recommendations from S&P 500 equities using fundamental analysis, sector benchmarking, risk-return optimization, and time series forecasting.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

---

## Overview

This project combines **investor profiling**, **fundamental equity screening**, **portfolio analytics**, and **price forecasting** into a single end-to-end pipeline. A user answers a short risk-tolerance questionnaire, and the tool responds with a curated, risk-aligned, and optionally sector-diversified portfolio — complete with expected return/volatility estimates, price forecasts, and an optimized share allocation.

---

## Key Features

**1. Investor Risk Profiling**
An interactive questionnaire scores the investor across four dimensions — age, annual income, investment horizon, and capital available — and classifies them as **Low**, **Medium**, or **High** risk tolerance.

**2. Fundamental Data Collection**
Pulls two years of historical pricing and key fundamental ratios (P/E, P/B, ROE, ROA, Debt-to-Equity, Profit/Operating/Gross Margins) for a configurable universe of S&P 500 stocks via `yfinance`.

**3. Sector Benchmarking & Buy/Sell Rating**
Each stock is compared against its sector average across five metrics (P/E, P/B, Debt-to-Equity, volatility, and CAGR). Stocks meeting at least 3 of 5 favorable criteria are flagged as **"Good"** buys.

**4. Risk-Aligned Recommendations**
"Good"-rated stocks are filtered by a volatility threshold matched to the investor's risk profile, ranked by CAGR, and optionally diversified across sectors (top stock per sector).

**5. Portfolio Risk-Return Metrics**
Computes expected portfolio return and standard deviation for the recommended basket using equal weighting and a correlation-adjusted variance calculation.

**6. Price Visualization**
Interactive Plotly charts display two-year historical price trends for each recommended stock.

**7. Time Series Forecasting**
Uses Facebook **Prophet** to generate 30-day and 120-day price forecasts with confidence intervals, plotted against historical data.

**8. Portfolio Optimization**
Applies **PyPortfolioOpt's** Efficient Frontier to maximize the Sharpe ratio across recommended holdings, then converts optimal weights into a discrete share allocation for a given portfolio value.

---

## Tech Stack

| Category | Tools / Libraries |
|---|---|
| Data Retrieval | `yfinance` |
| Data Processing | `pandas`, `numpy` |
| Visualization | `plotly`, `matplotlib` |
| Forecasting | `prophet`, `darts` |
| Portfolio Optimization | `pypfopt` (PyPortfolioOpt) |

---

## How It Works

```
Investor Questionnaire → Risk Profile (Low / Medium / High)
        ↓
S&P 500 Data Pull → Fundamentals + 2yr Price History
        ↓
Sector Averages → Buy/Sell Rating per Stock
        ↓
Risk-Filtered, Diversified Stock Shortlist
        ↓
Portfolio Expected Return & Std Dev
        ↓
Price Charts + Prophet Forecasts (30d / 120d)
        ↓
Efficient Frontier Optimization → Discrete Share Allocation
```

---

## Installation

```bash
pip install yfinance pandas numpy plotly matplotlib darts prophet pypfopt
```

> **Note:** `prophet` and `darts` can have platform-specific dependencies (e.g., `pystan`/`cmdstanpy`). If installation fails, consult each library's documentation for OS-specific setup instructions.

---

## Usage

1. Run the script:
   ```bash
   python portfolio_recommender.py
   ```
2. Answer the risk-profiling prompts (age, income, time horizon, investment amount).
3. Choose whether you'd like a **sector-diversified** portfolio or one based purely on **highest historical returns**.
4. The tool will:
   - Display the collected fundamental data and sector summary
   - Print Buy/Sell ratings for all screened stocks
   - Output your top recommended stocks with fundamental ratios
   - Show historical price charts and Prophet-based forecasts
   - Print optimized portfolio weights and a discrete share allocation

### Output Files
- `sp500_2y_with_ratings.csv` — Full screened universe with Buy/Sell ratings
- `recommended_stocks.csv` — Final risk-aligned recommended portfolio

---

## Sample Output

```
Your overall risk-taking ability is: Medium

Recommended Stocks:
  Ticker  Company Name        Sector       CAGR     Std Deviation  Buy Rating
  NVDA    NVIDIA Corp         Technology   0.58      0.42           Good
  XOM     Exxon Mobil Corp    Energy       0.18      0.21           Good
  ...

Expected Portfolio Return: 24.30%
Expected Portfolio Standard Deviation: 19.85%

Optimized Portfolio Weights:
NVDA: 32.00%
XOM: 21.00%
...

Discrete Allocation: {'NVDA': 12, 'XOM': 45, ...}
Funds Remaining: $134.27
```

---

## Limitations & Future Enhancements

- **Correlation Assumption:** The portfolio variance calculation currently uses a simplified flat pairwise correlation (0.25) rather than computed historical correlations — replacing this with an actual correlation matrix would improve accuracy.
- **Static Ticker Universe:** The stock universe is a hardcoded sample list; this could be expanded to dynamically pull the full S&P 500 constituent list.
- **Interactive Inputs:** Risk profiling currently relies on console `input()` prompts — a natural next step is a Streamlit/web front end for broader accessibility.
- **Backtesting:** Adding historical backtests of recommended portfolios would validate the screening methodology against realized performance.
- **Forecasting Models:** Additional model comparisons (ARIMA, Exponential Smoothing via Darts, LSTM) could be benchmarked against Prophet using MAPE.

---

## Disclaimer

This project is for **educational and informational purposes only**. It does not constitute financial advice, investment recommendations, or an offer to buy or sell any security. All data is sourced from publicly available APIs and may be delayed, incomplete, or inaccurate. Always consult a licensed financial advisor before making investment decisions.

---

## Author

**Ganesh Goyal**
Financial Data Analyst | Power BI · SQL · Python · Financial Modeling
[LinkedIn](https://www.linkedin.com/in/ganesh-goyal13/) 
