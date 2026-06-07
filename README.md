# 📈 Stock Trend Prediction using Machine Learning

## Overview

This project uses Machine Learning (Random Forest Classifier) and Technical Analysis Indicators to predict future stock trends using historical stock market data.

The model analyzes historical stock prices, calculates multiple technical indicators, and predicts whether the stock is likely to be:

- 🟢 Bullish (Expected rise greater than 5% in the next 20 trading days)
- 🔴 Bearish (Expected fall greater than 5% in the next 20 trading days)
- ⚪ Sideways (No significant movement)

This project demonstrates the application of Data Science, Feature Engineering, and Machine Learning in financial market analysis.

---

# Features

- Download 5 years of historical stock data using Yahoo Finance
- Generate technical indicators automatically
- Train a Random Forest Classification model
- Perform Time-Series Cross Validation
- Predict future stock trends
- Generate Bullish and Bearish signals
- Visualize predictions on stock price charts
- Evaluate model performance using accuracy and classification metrics

---

# Technologies Used

| Technology | Purpose |
|------------|---------|
| Python | Programming Language |
| Pandas | Data Processing |
| NumPy | Numerical Computation |
| yFinance | Stock Data Collection |
| Scikit-Learn | Machine Learning |
| Matplotlib | Data Visualization |

---

# Project Structure

```text
Stock-Trend-Prediction/
│
├── stock_prediction.py
├── requirements.txt
├── README.md
└── screenshots/
    └── prediction_chart.png
```

---

# Dataset

The dataset is fetched directly from Yahoo Finance using the yFinance API.

Example Stock:

```python
STOCK = "CUPID.NS"
```

Time Range:
- Last 5 Years of Historical Data
- Daily Closing Prices

Data Source:
- Yahoo Finance

---

# Technical Indicators Used

## 1. Exponential Moving Averages (EMA)

- EMA 20
- EMA 50
- EMA 100

These indicators help identify short-term, medium-term, and long-term trends.

### EMA Slope

```text
EMA_50(today) - EMA_50(5 days ago)
```

Measures trend direction and strength.

---

## 2. Relative Strength Index (RSI)

14-day RSI is used to identify:
- Overbought conditions
- Oversold conditions

Formula:

```text
RSI = 100 - (100 / (1 + RS))
```

---

## 3. Momentum Indicators

### Momentum 10

```text
Close Price - Close Price (10 days ago)
```

### Momentum 20

```text
Close Price - Close Price (20 days ago)
```

Measures the speed of price movement.

---

## 4. Volatility

```text
20-day Rolling Standard Deviation
```

Measures market risk and uncertainty.

---

## 5. Trend Confirmation

A bullish trend is confirmed when:

```text
EMA20 > EMA50 > EMA100
```

Returns:
- 1 → Trend Confirmed
- 0 → Trend Not Confirmed

---

# Target Variable Creation

Future return is calculated as:

```text
Future_Return =
(Close Price after 20 days - Current Close Price)
/ Current Close Price
```

Classification Rules:

| Future Return | Target |
|--------------|---------|
| > 5% | 1 (Bullish) |
| < -5% | -1 (Bearish) |
| Between -5% and 5% | 0 (Sideways) |

This creates a three-class classification problem.

---

# Machine Learning Model

## Random Forest Classifier

Parameters:

```python
RandomForestClassifier(
    n_estimators=300,
    max_depth=6,
    random_state=42,
    class_weight='balanced'
)
```

### Why Random Forest?

- Handles non-linear relationships
- Resistant to overfitting
- Works well with technical indicators
- Provides stable predictions

---

# Feature Set

The model uses the following features:

```python
[
 'EMA_20',
 'EMA_50',
 'EMA_100',
 'EMA_Slope',
 'RSI',
 'Momentum_10',
 'Momentum_20',
 'Volatility',
 'Trend_Confirm'
]
```

---

# Data Preprocessing

### Standardization

Features are scaled using:

```python
StandardScaler()
```

This ensures all features contribute equally to the model.

---

# Model Validation

The project uses:

```python
TimeSeriesSplit(n_splits=5)
```

instead of random train-test splitting.

### Why TimeSeriesSplit?

Financial data is sequential.

Using traditional random splits can cause data leakage and unrealistic performance estimates.

TimeSeriesSplit preserves chronological order.

---

# Model Evaluation

Metrics Used:

- Accuracy Score
- Precision
- Recall
- F1-Score
- Classification Report

Example:

```python
classification_report(
    y,
    model.predict(X_scaled)
)
```

---

# Signal Generation

After training, the model calculates probabilities:

```python
Bull_Prob
Bear_Prob
```

Signal Rules:

### Bullish

```text
Bull_Prob > 0.60
```

### Bearish

```text
Bear_Prob > 0.60
```

### Sideways

```text
Otherwise
```

---

# Visualization

The project visualizes:

- Closing Price
- EMA 50
- Bullish Signals
- Bearish Signals

Markers:

| Signal | Marker |
|---------|---------|
| Bullish | ▲ |
| Bearish | ▼ |

This helps investors identify potential trend opportunities visually.

---

# Installation

Clone the repository:

```bash
git clone https://github.com/your-username/stock-trend-prediction.git
```

Move into the project directory:

```bash
cd stock-trend-prediction
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Required Libraries

```bash
pip install yfinance pandas numpy matplotlib scikit-learn
```

---

# Running the Project

Execute:

```bash
python stock_prediction.py
```

The program will:

1. Download stock data
2. Generate indicators
3. Train the model
4. Evaluate performance
5. Generate signals
6. Display prediction chart

---

# Future Enhancements

### Deep Learning Models

- LSTM Networks
- GRU Networks
- Transformer Models

### Advanced Technical Indicators

- MACD
- Bollinger Bands
- ADX
- ATR
- Stochastic Oscillator

### Alternative Data Sources

- Financial News Sentiment
- Social Media Sentiment
- Economic Indicators

### Deployment

- Flask Web Application
- Spring Boot Backend Integration
- Real-Time Dashboard
- Cloud Deployment (AWS / Azure)

---

# Learning Outcomes

Through this project, we learned:

- Financial Data Collection
- Feature Engineering
- Technical Analysis
- Machine Learning Classification
- Time Series Validation
- Model Evaluation
- Data Visualization

---

# Disclaimer

This project is developed for academic and educational purposes only.

The predictions generated by this model should not be considered financial advice. Stock market investments involve risk, and users should conduct their own research before making investment decisions.
