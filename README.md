# 📈 Stock Market Analysis Dashboard (Python + Tableau)

This project demonstrates an **end-to-end data analytics workflow** using  
**Python (Pandas)** for data processing and **Tableau** for interactive visualization.

---

## 🖼️ Dashboard Preview

![Stock Market Dashboard](Stock%20Market%20Analytics.png)



# ============================================================
# STOCK MARKET DATA ANALYSIS PROJECT
# Author: Abdulsalam Alizada
# Tools: Python, Pandas
# Purpose:
#   - Process raw stock market data
#   - Perform time-series feature engineering
#   - Prepare analysis-ready datasets for Tableau dashboards
# ============================================================

# =========================
# 1. IMPORT LIBRARIES
# =========================
import pandas as pd

# Pandas is used for:
# - Reading CSV files
# - Handling time-series data
# - Calculating moving averages
# - Computing daily and percentage changes


# =========================
# 2. LOAD DATASETS
# =========================
# Each CSV file represents historical stock data for one company.
# Keeping them separate allows:
# - Company-level analysis
# - Easy comparison
# - Tableau company filters

apple = pd.read_csv("AAPL.csv")
facebook = pd.read_csv("FB.csv")
google = pd.read_csv("GOOGL.csv")
nvidia = pd.read_csv("NVDA.csv")
tesla = pd.read_csv("TSLA.csv")
twitter = pd.read_csv("TWTR.csv")


# =========================
# 3. INITIAL DATA CHECK
# =========================
# Checking the first rows ensures:
# - Data is loaded correctly
# - Column names are valid
# - No obvious data issues exist

print(apple.head())
print(facebook.head())
print(google.head())
print(nvidia.head())
print(tesla.head())
print(twitter.head())


# =========================
# 4. STORE DATAFRAMES IN A LIST
# =========================
# This allows us to apply the same transformations
# to all companies using loops (clean & scalable code)

dfs = [apple, facebook, google, nvidia, tesla, twitter]


# =========================
# 5. MOVING AVERAGE CALCULATION
# =========================
# Moving Averages help identify trends by smoothing price fluctuations.
# - MA50: Short to mid-term trend
# - MA200: Long-term trend
#
# These indicators are widely used in financial analysis
# to detect bullish or bearish market conditions.

for df in dfs:
    df["MA50"] = df["Close"].rolling(window=50).mean()
    df["MA200"] = df["Close"].rolling(window=200).mean()


# =========================
# 6. PREVIOUS DAY CLOSE PRICE
# =========================
# Using shift(1) to access previous day's closing price.
# This is a core time-series technique.
#
# Required for calculating:
# - Daily price change
# - Daily percentage change

for df in dfs:
    df["Previous_Close"] = df["Close"].shift(1)


# =========================
# 7. DAILY PRICE CHANGE (ABSOLUTE)
# =========================
# Measures how much the stock price changed in dollars.
# Business meaning:
# - Shows real gain or loss per day
# - Used in "Last Day Performance" analysis

for df in dfs:
    df["Price_Change"] = df["Close"] - df["Previous_Close"]


# =========================
# 8. DAILY PRICE CHANGE (PERCENTAGE)
# =========================
# Percentage change normalizes price movement.
# This allows fair comparison between companies
# with very different price levels (e.g., Apple vs Google).

for df in dfs:
    df["Price_Change_Pct"] = df["Close"].pct_change()


# =========================
# 9. PREVIOUS DAY VOLUME
# =========================
# Similar to price, volume is shifted by one day
# to calculate daily volume changes.

for df in dfs:
    df["Previous_Volume"] = df["Volume"].shift(1)


# =========================
# 10. DAILY VOLUME CHANGE (ABSOLUTE)
# =========================
# Helps identify:
# - Sudden trading spikes
# - Institutional buying/selling
# - Market reactions to news

for df in dfs:
    df["Volume_Change"] = df["Volume"] - df["Previous_Volume"]


# =========================
# 11. DAILY VOLUME CHANGE (PERCENTAGE)
# =========================
# Percentage-based volume change highlights
# abnormal trading activity and market sentiment.

for df in dfs:
    df["Volume_Change_Pct"] = df["Volume"].pct_change()


# =========================
# 12. EXPORT DATA FOR TABLEAU
# =========================
# The enriched datasets are exported as CSV files.
# These files are used directly in Tableau to build
# interactive dashboards and visual analytics.

apple.to_csv("Apple_Processed.csv", index=False)
facebook.to_csv("Facebook_Processed.csv", index=False)
google.to_csv("Google_Processed.csv", index=False)
nvidia.to_csv("Nvidia_Processed.csv", index=False)
tesla.to_csv("Tesla_Processed.csv", index=False)
twitter.to_csv("Twitter_Processed.csv", index=False)


# =========================
# 13. FINAL SUMMARY
# =========================
print("Data processing completed successfully.")
print("Processed files are ready for Tableau dashboard analysis.")



---

## 🔍 Data Processing & Feature Engineering

The raw stock market data was enriched using Python Pandas to create analytical features required for advanced analysis and visualization.

### 1️⃣ Data Loading
- Imported multiple CSV files, each representing a different company
- Stored them as separate Pandas DataFrames

**Purpose:**  
To enable individual company analysis and cross-company comparison.

---

### 2️⃣ Data Validation
- Checked column structure and sample rows using `.head()`
- Verified date, price, and volume columns

**Purpose:**  
To ensure data integrity before applying transformations.

---

### 3️⃣ Moving Average Calculation
- Calculated **50-day Moving Average (MA50)**
- Calculated **200-day Moving Average (MA200)**

**Why this matters:**
- Identifies short-term and long-term trends
- Reduces market noise
- Commonly used in technical analysis

---

### 4️⃣ Previous Day Metrics (Time-Series Shift)
- Used `shift(1)` to capture previous day’s:
  - Closing price
  - Trading volume

**Purpose:**  
To calculate daily changes accurately using time-series logic.

---

### 5️⃣ Price Change Calculations
- **Daily Price Change (Absolute):**
  - Difference between today’s and yesterday’s close price
- **Daily Price Change (Percentage):**
  - Normalized change for better comparison across stocks

**Business Value:**
- Measures gains and losses
- Helps assess volatility and risk

---

### 6️⃣ Volume Change Analysis
- Calculated:
  - Daily volume change
  - Percentage change in volume

**Why volume matters:**
- Confirms price movements
- Helps detect panic selling or institutional trading
- Differentiates real market moves from false signals

---

### 7️⃣ Data Export for Tableau
- Exported enriched datasets as new CSV files
- Used these files as inputs for Tableau dashboards

**Outcome:**  
A clean and analysis-ready dataset optimized for visualization.

---

## 📊 Tableau Dashboard Insights
The processed data was used to create an interactive dashboard featuring:

- KPI cards (Highest Price, Lowest Price, Total Volume)
- Time-series price and volume trends
- Daily percentage change distribution
- Company performance comparison
- Moving Average vs Price visualization

---

## 🎯 Key Insights
- Stock prices exhibit high volatility during certain periods
- Price movements combined with high trading volume indicate strong market reactions
- Moving averages help identify trend reversals and risk zones
- Percent-based metrics enable fair comparison across companies

---

## 🚀 Conclusion
This project demonstrates an **end-to-end data analytics workflow**, from raw data processing to business-focused visualization.

It showcases:
- Python data manipulation skills
- Time-series feature engineering
- Financial data analysis
- Business Intelligence dashboard development

---

## 👤 Author
**Abdulsalam Elizade**  
Data Analyst | Python | Tableau | Data Visualization

---

## 📌 Future Improvements
- Add technical indicators (RSI, Bollinger Bands)
- Automate data updates
- Extend analysis to other market sectors
