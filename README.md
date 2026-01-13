# Golden State Warriors Moneyline Odds Forecasting
A time-series forecasting project that models **Golden State Warriors (GSW) moneyline odds** by converting historical betting lines into **win probabilities** and forecasting future probabilities using multiple methods (ARIMA, ETS, Holt-Winters, NNETAR, Prophet, and an ensemble). Performance is evaluated using **RMSE, MAE, and MAPE**.
> Report included: **Forecasting_GSW_Moneyline_Odds.docx**

---

## Features

### Dataset & Problem Setup
- Dataset: **Kaggle NBA odds** (moneylines, totals, spreads, etc.) for NBA regular season games
- Seasons available: **2008–2023**
- Used seasons: **2008–2019**
  - Excluded **2020** (COVID-shortened season) and incomplete recent seasons
- Focused only on **Golden State Warriors (GSW)** games
- Converted **moneyline odds → implied probability** for interpretability and modeling
  - Positive odds: `100 / (odds + 100)`
  - Negative odds: `-odds / (-odds + 100)`
- Time series frequency set to **82** (games per season)

---

### Modeling Goal
- Forecast **GSW implied win probability** over time using only historical market information
- Explore whether betting odds show **patterns/trends/seasonality**, even in a competitive market
- Demonstrate a simplified framework for identifying potential **value betting**:
  - If forecasted probability differs meaningfully from sportsbook implied probability

---

## Models Implemented
- **ARIMA (auto.arima)**
- **ETS**
- **Holt-Winters**
- **NNETAR**
- **Prophet**
- **Combined Model (Ensemble)**
  - Average of the **3 best-performing models** (by RMSE/MAE/MAPE)

---

## Evaluation

### Train/Test Split
- **Train:** Seasons **2008–2017**
- **Test:** Seasons **2018–2019**

### Metrics
- **RMSE** (primary)
- **MAE**
- **MAPE**

---

## Key Findings
- **ARIMA performed best overall** (lowest forecast errors on the test set)
- **ETS** was competitive but ignored seasonality due to high frequency limitations
- **Holt-Winters** required interpolation for missing values and showed higher error
- **NNETAR** captured dynamics well (residual ACF/PACF mostly within bounds) but did not outperform ARIMA
- **Prophet performed worst** with large error and residual autocorrelation
- The **ensemble** (ARIMA + ETS + NNETAR) did not beat ARIMA alone

---

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/gsw-moneyline-forecasting.git
cd gsw-moneyline-forecasting
```
2. Install R dependencies (example):
```bash
install.packages(c("tidyverse", "forecast", "tseries", "lubridate", "prophet", "ggplot2"))
```
If you use renv, you can initialize and restore packages:
```bash
install.packages("renv")
renv::init()
renv::restore()
```

## Usage
```bash
rmarkdown::render("Forecasting_GSW_Moneyline.Rmd")
```

## Project Structure
```bash
gsw-moneyline-forecasting/
├── oddsData.csv
├── Forecasting_GSW_Moneyline.Rmd
├── Forecasting_GSW_Odds.pdf
├── README.md
└── LICENSE
```

## Development
### Reproducibility
- Fixed train/test season split
- Frequency set to 82 games per season
- Missing values handled explicitly (interpolation where required)

### (Optional) Future Improvements
- Add exogenous covariates (injuries, rest days, opponent strength, trades)
- Multivariate models (ARIMAX / dynamic regression)
- Backtesting a rules-based “value bet” strategy with bankroll simulation

## Contributions

To contribute:
1. Fork the repository
2. Create a feature branch (git checkout -b feature/YourFeature)
3. Commit your changes (git commit -m "Add YourFeature")
4. Push to the branch (git push origin feature/YourFeature)
5. Open a Pull Request

## License
This project is licensed under the MIT License.

## Acknowledgments
- Kaggle dataset: NBA odds data (2008–2023)
- forecast package for ARIMA/ETS/NNETAR modeling
- prophet package for Prophet forecasting
