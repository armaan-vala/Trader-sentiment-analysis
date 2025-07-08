# 📈 Trader Sentiment Analysis – Linking Market Mood to Trader Behavior

This data science project explores how **market sentiment** (Fear or Greed) influences **trader behavior** and **performance outcomes** on a real-world crypto trading platform. Using Python, we merged trader data with sentiment data and conducted deep analysis with Pandas, supported by essential Matplotlib and Seaborn visualizations.




## 🎯 Project Objective

To uncover the relationship between **market sentiment** and **trader performance**, including:
- Profit/Loss behavior across different sentiments
- Trading volume and bias during Fear vs Greed
- Fee structure and execution tendencies
- Risk levels during extreme sentiment events



## 📁 Datasets Used

1. **Fear & Greed Index**  
   - Columns: `date`, `classification`  
   - Values like: Fear, Greed, Neutral, etc.

2. **Historical Trader Data (Hyperliquid Exchange)**  
   - Columns include:  
     `Timestamp IST`, `Side`, `Execution Price`, `Fee`, `Closed PnL`  
   - Time-stamped logs of every trade made on the platform

---

## ⚙️ Project Workflow

```python
# Step 1: Load CSVs
fear_greed = pd.read_csv("fear_greed_index.csv")
historical_data = pd.read_csv("historical_data.csv")

# Step 2: Clean & Select Required Columns
fear_greed = fear_greed[["date", "classification"]]
historical_data = historical_data[["Timestamp IST", "Closed PnL", "Side", "Execution Price", "Fee"]]

# Step 3: Format Date Columns
fear_greed["date"] = pd.to_datetime(fear_greed["date"]).dt.date
historical_data["Timestamp IST"] = pd.to_datetime(historical_data["Timestamp IST"], errors="coerce")
historical_data["date"] = historical_data["Timestamp IST"].dt.date

# Step 4: Merge DataFrames on Date
merged_df = pd.merge(historical_data, fear_greed, on="date", how="left")

```
## 📊 Key Analysis

✅ Average PnL per sentiment

✅ Trade volume (Buy/Sell) per sentiment

✅ Fees comparison by sentiment & side

✅ Standard deviation (volatility) of returns by sentiment

✅ Descriptive stats like Min, Max, Quartiles of PnL

## 📈 Visualizations

We used basic matplotlib and some seaborn for clear understanding of data via plots.

## 📈 Visualizations

We used basic `matplotlib` and some `seaborn` for cleaner styling.

### 📊 Bar plot: Avg PnL per sentiment
![Average PnL](images/avg_pnl_per_sentiment.png)

### 📊 Bar plot: Trade volume by sentiment
![Trade Volume](images/trade_volume_by_sentiment.png)

### 📊 Comparison: Fee for Buy vs Sell
![PnL Distribution](images/PnL_Distribution_per_Market_Sentiment.png)

### 📊 Distribution of PnL using `describe()` and quartiles
![PnL Distribution](images/Winrate_per_Market_Sentiment.png)


## 🔍 Key Findings
Extreme Greed days saw the highest average profit, but also higher volatility

Fear sentiment surprisingly had better win rates (less overconfidence?)

Buy trades had slightly higher fees than Sell

Most trades occurred during Greed, showing crowd confidence bias

Traders need to manage risk better during extreme sentiment events
