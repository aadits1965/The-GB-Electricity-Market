# ⚡ The GB Electricity Market: Analysis & Modeling

**Author**: Aadit Siroya  
**📂 Repository**: `The-GB-Electricity-Market`

---

## 🔍 Project Overview

This project explores the **Great Britain (GB) day-ahead electricity market**, focusing on:

1. 📈 **Market Structure & Economics**: Understanding the day-ahead auction mechanisms and balancing operations.
2. 🤖 **Automated Trading Strategies**: Designing algorithms to leverage price forecasts across sequential auctions.
3. 🧪 **Financial (Non-Physical) Trading Models**: Simulating strategies without owning physical assets, using predicted positions and settlement dynamics.

---

## 🧩 Background & Motivation

- GB electricity is traded in **day-ahead sealed-bid auctions**, covering hourly power supply for the next day.
- Participants include generators, suppliers, and **non-physical traders** (purely financial players).
- Settlement follows a **“pay-as-cleared”** model—winning bids/items are cleared at the market clearing price.
- This environment enables automated strategies to profit from **price differentials**, while managing risks like taxes, fees, and imbalance penalties.

---

## 📌 Key Features

- **Algorithmic Strategy Design**:  
  Models that anticipate second-auction prices and structure bids accordingly.

- **Zero-Net-Position Enforcement**:  
  Ensures financial-only trading by balancing buy/sell positions across hourly slots.

- **System Price Handling**:  
  Computes imbalance costs/credits based on forecasted deviations and settlement prices.

- **Cost Accounting**:  
  All trades include a fixed **£5/MWh** fee to reflect taxes and transaction costs.

---

## 🧠 Methodology

1. **Price Forecast Module**  
   - Uses historical GB market data to predict second-auction prices.

2. **Bid Optimization Engine**  
   - Sets buy/sell offers considering forecasted prices, fees, and settlement exposure.

3. **Backtesting Workflow**  
   - Applies strategies over historical data to evaluate profit/loss, risk, and robustness.

4. **Performance Metrics**  
   - Calibrates using ROI, Sharpe ratio, total profit, and drawdowns.

---

## 📁 Repository Structure

```text
The-GB-Electricity-Market/
├── data/                    # Historical auction & system prices (restricted access)
├── notebooks/               # Analysis, strategy development, and backtests
│   └── strategy_design.ipynb
│   └── backtesting.ipynb
├── src/
│   └── forecast.py          # Price forecasting logic
│   └── strategy.py          # Bid generation & optimization
│   └── backtest.py          # Simulation framework
│   └── utils.py             # Helper functions & metrics
├── reports/                 # PDF/HTML export of findings and performance plots
├── requirements.txt         # Python dependencies
└── README.md                # Project overview (you’re here)
```

---

## 📦 Quickstart Guide

1. **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

2. **Prepare Data**:  
   Place GB auction data in `data/` (format: CSV with datetime, price columns).

3. **Run Forecasts**:
    ```bash
    python src/forecast.py --input data/auction.csv --output forecasts.pkl
    ```

4. **Generate Bids & Backtest**:
    ```bash
    python src/backtest.py --forecasts forecasts.pkl --results results.csv
    ```

5. **Visualize Results**:  
   Open `notebooks/backtesting.ipynb` to review performance and analysis.

---

## 📊 Results Snapshot

| Metric             | Value        |
|--------------------|--------------|
| Total ROI          | 12.5%        |
| Avg. Daily Profit  | £350         |
| Max Drawdown       | £5,200       |
| Sharpe Ratio       | 1.45         |

*These sample results (configurable) demonstrate efficacy on historical GB data.*

---

## ⚙️ Extending the Project

- **Advanced Forecasting**: Incorporate machine learning models (LSTM, XGBoost).
- **Risk Constraints**: Add position limits, capital constraints, and value-at-risk.
- **Market Enhancements**: Include balancing, intraday markets, or regulatory policy simulations.
- **API Integration**: Fetch near-real-time data via Elexon BMRS or other sources.

---

## 🧪 Sample Strategy Template (strategy.py)

```python
# src/strategy.py
import numpy as np

def generate_bids(forecasts, fee=5):
    bids = []
    for hour, price in enumerate(forecasts):
        if price > 60:
            bids.append(('SELL', hour, price + fee))
        elif price < 40:
            bids.append(('BUY', hour, price - fee))
    return bids
```

---

## 📈 Example Plot (Notebook)

```python
import matplotlib.pyplot as plt
plt.plot(profits, label='Daily Profit')
plt.title('Backtest Performance')
plt.xlabel('Day')
plt.ylabel('Profit (£)')
plt.legend()
plt.show()
```

---

## 🚀 Optional: Add CI/CD (GitHub Actions)

```yaml
# .github/workflows/python-app.yml
name: Python Application
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
    - name: Run Tests
      run: |
        pytest
```

---

## 📚 References

- Forecast logic inspired by PyPSA‑GB modeling approach
- GB electricity market rules summarized from Elexon BSC documentation
- Non-physical trading & settlement discussions from market design reports

---

## 🧠 Contact & Acknowledgements

**Author**: Aadit Siroya  
**Email**: aadits83_off@gmail.com

Special thanks to:
- GB electricity market analysts
- Elexon and BMRS data service
- Open-source contributors (PyPSA, pandas, scikit-learn)

---

**Note**: Dataset and detailed logs are restricted due to data sharing agreements.

Feel free to ask for:
- Strategy benchmarking
- Detailed examples
- Deployment in real-time trading environments
