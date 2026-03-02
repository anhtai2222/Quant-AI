# ETH/USDT Trading Strategy Backtest

A comprehensive backtesting project for an EMA-based trend-following strategy applied to ETHUSDT cryptocurrency pair, with support for leverage and compounding analysis.

## 📋 Project Overview

This project contains:
- **ETHUSDT Backtesting Notebook** - A Jupyter notebook implementing a trend-following strategy using EMA200
- **Historical Data** - ETHUSDT.csv with OHLCV (Open, High, Low, Close, Volume) data
- **Supporting Scripts** - Python utilities for fault injection testing and data processing

## 🎯 Strategy Description

### Core Logic
The strategy implements a simple yet effective trend-following approach:

- **Entry Signal**: When `Close(t-1) > EMA200(t-1)` → Enter LONG at `Open(t)`
- **Exit Signal**: When `Close(t-1) ≤ EMA200(t-1)` → Exit position and hold USDT
- **No Lookahead Bias**: All signals are computed from previous candle data before execution on current candle

### Key Features
- **Trend Filter**: Uses 200-period Exponential Moving Average (EMA200)
- **Leverage & Compounding**: Optional leverage multiplier for performance comparison
- **Fee & Slippage**: Configurable trading costs to simulate real market conditions
- **Risk Metrics**: Calculates Sharpe ratio, maximum drawdown, CAGR, and ROI

## 📊 Performance Targets

The strategy aims to achieve:
- **Sharpe Ratio (annualized)** > 0.3
- **CAGR (annualized return)** > 15%
- **Outperformance** over Buy & Hold strategy on the same period

## 📁 File Structure

```
testdemo/
├── README.md                      # This file
├── ETHUSDT_Strategy.ipynb         # Main backtest notebook
├── ETHUSDT.csv                    # Historical price data
├── venv/                          # Python virtual environment
├── .git/                          # Git repository
└── testdemo/
    └── demo_fault_ai.py.save      # Fault injection testing utilities
```

## 🔧 Configuration

The notebook supports the following tunable parameters:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `EMA_LEN` | Period for EMA calculation | 200 |
| `LEVERAGE` | Leverage multiplier | 1.0 |
| `FEE_BPS` | Trading fees in basis points | TBD |
| `SLIP_BPS` | Slippage in basis points | TBD |

## 📈 Data Cleaning

The notebook implements robust data validation:
- ✅ Removes duplicate timestamps (keeps first occurrence)
- ✅ Filters invalid OHLC candles:
  - `high < low`
  - `close` outside `[low, high]`
- ✅ Removes candles with `volume <= 0`
- ⚠️ Note: Keeps `high == low` candles as they may represent low volatility periods

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- Virtual environment setup with required packages

### Installation

```bash
# Activate virtual environment
source venv/bin/activate

# Install dependencies (if needed)
pip install pandas numpy matplotlib jupyter
```

### Running the Backtest

```bash
# Launch Jupyter Notebook
jupyter notebook ETHUSDT_Strategy.ipynb
```

Then execute all cells to:
1. Load and clean the ETHUSDT.csv data
2. Calculate EMA200 values
3. Generate entry/exit signals
4. Run the backtest simulation
5. Generate performance reports and visualizations

## 📊 Outputs

The notebook generates:
- **Equity Curve Chart** - Portfolio value over time
- **Drawdown Chart** - Peak-to-trough declines
- **Performance Metrics**:
  - Sharpe Ratio (annualized)
  - Maximum Drawdown
  - CAGR (Compound Annual Growth Rate)
  - Total ROI
- **Comparison Table** - Strategy vs Buy & Hold performance

## 🔍 Fault Injection Testing

The `demo_fault_ai.py.save` file contains utilities for testing strategy robustness under various fault conditions:
- **Sensor Bias**: Simulates biased market observations
- **Sensor Noise**: Adds Gaussian noise to price data
- **Actuator Weakness**: Simulates failed order executions

## 📝 Data Format

Expected CSV format with columns:
```
timestamp, open, high, low, close, volume
```

## ⚠️ Important Notes

- **Backtesting Bias**: Results are historical and do not guarantee future performance
- **Market Conditions**: Past performance under specific market conditions may not repeat
- **Slippage & Fees**: Real trading includes slippage and fees that may impact returns
- **Data Quality**: Ensure input data is clean and from a reliable source

## 📧 Notes

- Strategy documentation is in Vietnamese (Notebook)
- All backtest calculations follow industry standard methodologies
- Consider stress testing before deploying with real capital

## 🔗 Requirements Met

- Trend-following strategy based on EMA filter
- No lookahead bias
- Comprehensive performance metrics
- Leverage and compounding analysis
- Sharpe ratio and drawdown tracking

---

**Last Updated**: March 2, 2026
