# Trader-Performance-vs-Market-Sentiment
### Primetrade.ai — Data Science Intern Assignment

## Overview
This project analyzes how Bitcoin Fear/Greed sentiment correlates with trader behavior and performance on Hyperliquid.

---

## Project Structure
```
primetrade_project/
├── data/
│   ├── fear_greed.csv       ← Bitcoin Fear/Greed index (daily)
│   └── trader_data.csv      ← Hyperliquid historical trades (tab-separated)
├── notebook.ipynb           ← Main analysis notebook
├── charts/                  ← Auto-generated charts (created on run)
└── README.md
```

---

## Setup & How to Run

### 1. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

### 2. Place data files
- Put `fear_greed.csv` in the `data/` folder
- Put `trader_data.csv` in the `data/` folder

### 3. Launch the notebook
```bash
jupyter notebook notebook.ipynb
```

### 4. Run all cells
Use **Kernel → Restart & Run All** to execute the full analysis.

---

## Methodology

### Data Preparation (Part A)
- Loaded both datasets, checked for missing values and duplicates
- Parsed `Timestamp IST` from trader data to extract daily dates
- Simplified Fear/Greed classifications into 3 buckets: **Fear**, **Neutral**, **Greed**
- Computed daily per-account metrics: PnL, win rate, trade count, volume, long ratio
- Merged on date to align sentiment with trader performance

### Analysis (Part B)
- **Q1:** Compared median daily PnL, win rate, and PnL volatility across sentiment groups
- **Q2:** Measured trade frequency, long/short bias, and volume by sentiment
- **Q3:** Segmented traders into 3 pairs: High/Low Leverage · Frequent/Infrequent · Consistent/Inconsistent
- Explored interaction effects between sentiment and trader segments

### Predictive Model (Bonus)
- **Target:** Binary — will a trader have a profitable day? (PnL > 0)
- **Features:** trade_count, avg_size_usd, win_rate, long_ratio, fg_score, sentiment (encoded)
- **Model:** Random Forest (100 trees, max_depth=6)
- **Evaluation:** Classification report + confusion matrix

---

## Key Insights

| # | Insight |
|---|---------|
| 1 | Fear days suppress trader PnL — median returns are lower during Fear sentiment |
| 2 | Traders exhibit stronger long bias during Greed days |
| 3 | High-leverage traders suffer most on Fear days — worst risk-adjusted outcome |
| 4 | Consistent winners amplify gains during Greed — sentiment acts as a performance multiplier |

---

## Strategy Recommendations

### 🔴 Rule 1 — Fear Days: Reduce Leverage
> When the Fear/Greed index drops below 30, high-leverage traders should cap position size to ≤50% of their typical size. Fear days significantly increase PnL volatility and reduce win rates.

### 🟢 Rule 2 — Greed Days: Consistent Traders Scale Up
> Traders in the top 50% win-rate bucket can safely increase daily trade frequency by up to 1.5× when the index is above 60. Infrequent or inconsistent traders should NOT follow this rule — their performance does not improve with frequency.

---

## Charts Generated
| File | Description |
|------|-------------|
| `charts/01_performance_by_sentiment.png` | PnL, win rate, volatility by sentiment |
| `charts/02_behavior_by_sentiment.png` | Trade frequency, long ratio, volume by sentiment |
| `charts/03_trader_segments.png` | PnL by leverage / frequency / consistency segments |
| `charts/04_sentiment_x_leverage.png` | Interaction: sentiment × leverage on PnL |
| `charts/05_model_results.png` | Feature importance + confusion matrix |

Submitted by:

Charu

charubhalla14@gmail.com, www.linkedin.com/in/charu-bhalla-720814312
