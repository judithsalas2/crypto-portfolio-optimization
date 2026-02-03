# Cryptocurrency Portfolio Optimization Using MILP

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Pyomo](https://img.shields.io/badge/Pyomo-6.0+-green.svg)](http://www.pyomo.org/)

A Mixed-Integer Linear Programming (MILP) approach to cryptocurrency portfolio optimization based on Modern Portfolio Theory (Markowitz, 1952) with practical market constraints.

## Overview

This project implements a portfolio optimization model that combines continuous capital allocation decisions with discrete asset selection, addressing real-world investment constraints such as:

- **Cardinality constraints**: Limiting the number of assets to reduce transaction costs and management complexity
- **Minimum investment thresholds**: Ensuring meaningful positions when assets are selected
- **Maximum concentration limits**: Preventing excessive exposure to single assets

The model uses the Konno-Yamazaki (1991) linear approximation of risk, enabling efficient solution with MILP solvers.

## Mathematical Formulation

### Objective Function
Minimize weighted portfolio risk:

$$\min \sum_{i \in I} w_i \cdot \sigma_i$$

### Constraints

| Constraint | Description | Formulation |
|------------|-------------|-------------|
| Budget | Full investment of capital | $\sum_{i} w_i = 1$ |
| Return | Minimum expected return | $\sum_{i} w_i \mu_i \geq R_{min}$ |
| Cardinality | Maximum number of assets | $\sum_{i} y_i \leq K$ |
| Linking | Continuous-binary link | $w_i \leq y_i$ |
| Min. Investment | Minimum per asset | $w_i \geq L \cdot y_i$ |
| Max. Investment | Maximum per asset | $w_i \leq U$ |

Where:
- $w_i \in [0,1]$: proportion invested in asset $i$ (continuous)
- $y_i \in \{0,1\}$: binary selection variable for asset $i$

## Features

- **Portfolio optimization** with 10 major cryptocurrencies (BTC, ETH, BNB, XRP, ADA, SOL, DOGE, DOT, MATIC, LINK)
- **Efficient frontier visualization** with cardinality constraints
- **Sensitivity analysis** on key parameters (minimum return, cardinality limit)
- **Correlation matrix heatmap** for asset relationships
- **Risk-return scatter plots** for individual assets

## Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/crypto-portfolio-optimization.git
cd crypto-portfolio-optimization

# Install dependencies
pip install -r requirements.txt

# Install GLPK solver (Ubuntu/Debian)
sudo apt-get install glpk-utils

# Or on macOS with Homebrew
brew install glpk
```

## Dependencies

```
numpy>=1.21.0
pandas>=1.3.0
matplotlib>=3.4.0
pyomo>=6.0.0
```

## Usage

Open and run the Jupyter notebook:

```bash
jupyter notebook crypto_portfolio_optimization.ipynb
```

Or run the optimization directly:

```python
from pyomo.environ import *
import numpy as np

# Define parameters
R_min = 0.028  # Minimum 2.8% monthly return
K_max = 5      # Maximum 5 assets
L_min = 0.05   # Minimum 5% per selected asset
U_max = 0.40   # Maximum 40% per asset

# Build and solve model
model = ConcreteModel()
# ... (see notebook for full implementation)
```

## Results

The model produces:
- **Optimal portfolio weights** satisfying all constraints
- **Expected return and risk metrics** for the optimal portfolio
- **Efficient frontier** showing the risk-return trade-off
- **Sensitivity analysis** demonstrating diversification benefits

### Key Findings

1. The cardinality constraint significantly impacts the risk-return profile
2. Marginal diversification benefits decrease rapidly after 5 assets
3. The MILP formulation provides computationally efficient solutions

## Project Structure

```
crypto-portfolio-optimization/
├── README.md
├── requirements.txt
├── crypto_portfolio_optimization.ipynb    # Main notebook with implementation
└── docs/
    └── Cryptocurrency_Portfolio_Optimization_MILP.pdf  # Academic paper
```

## Theoretical Background

This implementation is grounded in established financial theory:

- **Markowitz, H. (1952)** - Modern Portfolio Theory foundations
- **Sharpe, W.F. (1964)** - Capital Asset Pricing Model (CAPM)
- **Konno, H. & Yamazaki, H. (1991)** - Mean-Absolute Deviation (MAD) approach
- **Chang et al. (2000)** - Cardinality-constrained portfolio optimization

See the accompanying PDF document for a comprehensive literature review and detailed mathematical derivations.

## Limitations

- Historical returns do not guarantee future performance
- Cryptocurrency returns exhibit non-normal distributions (heavy tails)
- Correlations may increase during market stress periods
- The linear risk approximation is a simplification of true portfolio variance

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Author

**Judith M. Salas García**  
Mathematical Engineering Student  
Universidad Alfonso X el Sabio

## Acknowledgments

- Operations Research course at Universidad Alfonso X el Sabio
- GLPK (GNU Linear Programming Kit) development team
- Pyomo optimization modeling framework

---

*This project was developed as part of the Operations Research coursework (January 2026)*
