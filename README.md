# 📈 Cryptocurrency Market Automation & Analysis Pipeline

> An automated data pipeline that continuously fetches live cryptocurrency market data from the CoinMarketCap API, stores it persistently, and generates multi-timeframe percent-change visualizations for the top 10 cryptocurrencies.

---

## 🚀 Project Overview

This project automates the collection of real-time cryptocurrency market data using the **CoinMarketCap Pro API** and builds a structured data analysis and visualization pipeline. The system runs on a scheduled loop (every 24 hours), incrementally appending market snapshots to a local CSV — enabling trend analysis across multiple timeframes (24h, 7d, 30d, 60d, 90d).

---

## 🛠️ Tech Stack

| Tool/Library | Purpose |
|---|---|
| `Python 3.x` | Core language |
| `urllib` / `ssl` / `certifi` | Secure HTTP requests to CoinMarketCap API |
| `pandas` | Data normalization, transformation, and CSV I/O |
| `matplotlib` | Plotting and chart rendering |
| `seaborn` | Statistical visualization (categorical point plots) |
| `os` / `time` / `sleep` | File management and scheduling |
| `CoinMarketCap Pro API` | Live crypto market data source |

---

## ✨ Features

- **Automated Data Collection** — Runs in a loop every 24 hours, fetching the latest listings for the top 10 cryptocurrencies by market cap
- **Secure API Integration** — Uses SSL context with `certifi` for safe HTTPS connections
- **Incremental CSV Storage** — Appends each API response to a persistent CSV file without overwriting historical data
- **Data Normalization** — Flattens nested JSON API responses using `pd.json_normalize` with timestamping for time-series tracking
- **Multi-Timeframe Analysis** — Groups and averages percent changes across 24h, 7d, 30d, 60d, and 90d windows
- **Interactive Visualizations** — Generates seaborn categorical point plots comparing percent changes per coin across all timeframes

---

## 📁 Project Structure

```
cryptoautomation/
│
├── api_testing.ipynb       # Main Jupyter Notebook with full pipeline
├── cryptodata.csv          # Auto-generated; stores all historical API snapshots
└── README.md               # Project documentation
```

---

## ⚙️ Setup & Installation

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/cryptoautomation.git
cd cryptoautomation
```

### 2. Install Dependencies
```bash
pip install pandas matplotlib seaborn certifi
```

### 3. Configure API Key
Replace the placeholder API key in the notebook with your own CoinMarketCap Pro API key:
```python
"X-CMC_PRO_API_KEY": "YOUR_API_KEY_HERE"
```
> Get a free API key at [coinmarketcap.com/api](https://coinmarketcap.com/api/)

### 4. Run the Notebook
Open `api_testing.ipynb` in Jupyter and run all cells. The pipeline will:
1. Fetch data from CoinMarketCap
2. Save/append to `cryptodata.csv`
3. Analyze percent changes
4. Display the visualization

---

## 📊 How It Works

### Step 1 — API Request
Sends a secure GET request to the CoinMarketCap `/v1/cryptocurrency/listings/latest` endpoint, fetching the top 10 coins with USD conversion.

### Step 2 — Data Normalization & Timestamping
The JSON response is flattened into a pandas DataFrame using `pd.json_normalize`. A `timestamp` column is added to track when each snapshot was captured.

### Step 3 — Scheduled Loop (24-Hour Automation)
```python
for i in range(5):
    api_runner()
    sleep(86400)  # Waits 24 hours between each run
```
Runs 5 cycles by default (configurable). Each run appends a new row to the CSV.

### Step 4 — Percent Change Analysis
Groups data by cryptocurrency name and computes mean percent changes across five timeframes:
- `24h`, `7d`, `30d`, `60d`, `90d`

### Step 5 — Visualization
Generates a **seaborn categorical point plot** comparing each coin's performance across all timeframes — making trend patterns immediately visible.

---

## 📸 Sample Output

The visualization displays a point plot with:
- **X-axis**: Timeframe (24h, 7d, 30d, 60d, 90d)
- **Y-axis**: Average percent change (%)
- **Hue**: Cryptocurrency name (BTC, ETH, BNB, etc.)

---

## 🔧 Configuration Options

| Parameter | Default | Description |
|---|---|---|
| `start` | `1` | Starting rank of coin listings |
| `limit` | `10` | Number of coins to fetch |
| `convert` | `USD` | Fiat currency for conversion |
| `sleep(86400)` | 24 hours | Interval between API calls |
| Loop count | `5` | Number of data collection cycles |

---

## 📌 Future Improvements

- [ ] Add CLI arguments for configurable coin limit and loop count
- [ ] Integrate database storage (PostgreSQL / SQLite) instead of CSV
- [ ] Deploy as a scheduled cloud job (AWS Lambda / GitHub Actions)
- [ ] Add email/Slack alerts for significant price movements
- [ ] Build an interactive dashboard with Plotly or Streamlit

---


## 🙋 Author

**Your Name**
- GitHub: [@bhuvanesh13459](https://github.com/bhuvanesh13459)
- LinkedIn: [Bhuvanesh Jakkula](https://www.linkedin.com/in/bhuvanesh-jakkula-data-analyst/)

---

> ⭐ If you found this project useful, please consider giving it a star!
