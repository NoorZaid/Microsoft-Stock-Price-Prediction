# Microsoft Stock Price Prediction

A Python-based time-series prediction project that analyzes historical stock market data for **Microsoft Corporation (NASDAQ: MSFT)** and uses Linear Regression to predict the next trading day's closing price.

## Project Overview

This notebook downloads Microsoft stock data with `yfinance`, explores historical closing prices, prepares a one-step-ahead prediction target, trains a Linear Regression model, and evaluates its predictions against a held-out test period.

The historical data is requested from **January 1, 2004 through December 29, 2024** (the `yfinance` end date is exclusive).

## Objectives

- Retrieve historical MSFT market data.
- Visualize Microsoft closing-price trends.
- Create a target representing the following trading day's closing price.
- Train a Linear Regression model using the current closing price.
- Evaluate predictions on a chronological test set.
- Visualize actual versus predicted closing prices.

## Tools & Libraries

- Python
- yfinance
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn

## Workflow

1. **Install and import libraries** — set up the required Python packages.
2. **Download stock data** — retrieve MSFT historical market data using `yfinance`.
3. **Explore and visualize** — plot the historical closing prices.
4. **Feature engineering** — create `Target` by shifting the `Close` column by one row, so each row's target is the next trading day's close.
5. **Clean and prepare data** — remove rows with missing values and use `Close` as the input feature.
6. **Train/test split** — use an 80/20 split without shuffling, preserving chronological order.
7. **Model training** — fit a scikit-learn `LinearRegression` model.
8. **Evaluation** — calculate Mean Absolute Error (MAE) and Mean Squared Error (MSE).
9. **Visualization** — compare actual and predicted values over the test dates.

## Model Results

The notebook reports the following evaluation results on its held-out test set:

| Metric | Result |
|---|---:|
| Mean Absolute Error (MAE) | 3.6199 |
| Mean Squared Error (MSE) | 23.3944 |

These values are reproduced from the notebook output. They are in the same price units as the downloaded `Close` values.

## Important Methodology Note

The notebook's final June 2025 forecast section needs correction before its results can be interpreted as valid stock-price forecasts.

The model is trained with **`Close` as its single input feature**, but the future-prediction section passes **elapsed-day values** (`future_days`) to that same model. These are different feature definitions, so the resulting forecast values (approximately 7,832–7,861) are not valid predictions from the trained setup.

To make a future forecast consistent with the model, the prediction input must represent a closing price. For a genuine multi-step forecast, the notebook would also need an explicit strategy for generating or obtaining each subsequent day's input. Alternatively, a model designed with time-based features could be trained and evaluated using those same features.

## Repository Structure

```text
.
├── Stock_Data_for_Microsoft_Corporation.ipynb
└── README.md
```

## How to Run

1. Clone or download this repository.
2. Open `Stock_Data_for_Microsoft_Corporation.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
3. Install the dependencies if needed:

   ```bash
   pip install yfinance pandas numpy matplotlib seaborn scikit-learn
   ```

4. Run the notebook cells in order.

The notebook downloads data from Yahoo Finance, so an internet connection is required. Historical data returned by `yfinance` may change as the data provider updates its records.

## Disclaimer

This project is for educational and demonstration purposes only. It is not financial advice and should not be used as the sole basis for investment decisions. Stock prices are affected by many factors that are not represented in this simple one-feature Linear Regression model.
