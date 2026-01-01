# Analysis of Trader Behavior vs. Market Sentiment

**Candidate:** Sourabh Khamankar
**Date:** December 31, 2025

## 📌 Project Overview
This project investigates the relationship between **Bitcoin Market Sentiment** (Fear & Greed Index) and **Trader Behavior** (Hyperliquid historical trading data). The objective was to identify whether market sentiment influences risk appetite, trading volume, and profitability, and to derive data-driven trading strategies from these patterns.

## 📂 Directory Structure
The project adheres to the strict submission format:

```text
ds_Sourabh_Khamankar/
├── notebook_1.ipynb       # Main analysis code (Data Aggregation, Merging, Visualization)
├── ds_report.pdf          # Executive Summary, Key Insights, and Strategic Recommendations
├── README.md              # Project documentation (this file)
├── csv_files/             # Raw Datasets
│   ├── fear_greed_index.csv
│   └── historical_data.csv
└── outputs/               # Generated Visualizations
    ├── risk_analysis.png  # Average Trade Size vs. Sentiment
    ├── volume_analysis.png# Volume Distribution vs. Sentiment
    └── pnl_analysis.png   # Net PnL vs. Sentiment

```

## ⚙️ Methodology & Implementation Details

### 1. Data Loading & Preprocessing

* **Datasets:** Loaded `historical_data.csv` (Trading Logs) and `fear_greed_index.csv` (Sentiment Data).
* **Date Synchronization:**
* Converted `Timestamp IST` in the trading data to datetime objects.
* Normalized timestamps to a daily `Date` format to align with the daily resolution of the Fear & Greed Index.



### 2. Metric Derivation (Crucial Implementation Note)

* **Risk Proxy:** The raw dataset did not contain a `leverage` column. To accurately measure risk appetite, I calculated **Average Trade Size ($)** (`Size USD`) per day.
* *Assumption:* Larger position sizes indicate higher trader confidence and risk tolerance.


* **Volume & PnL:** Calculated `Total Volume` (Sum of Size USD) and `Net PnL` (Sum of Closed PnL) for each day.
* **Sentiment Classification:** Mapped daily sentiment values to standard classes: *Extreme Fear, Fear, Neutral, Greed, Extreme Greed*.

### 3. Data Merging

* Performed an **Inner Join** on the `Date` column to ensure analysis was performed only on days where both Trading and Sentiment data were available.

## 📊 Visual Analysis & Outputs

The code generates three key visualizations in the `outputs/` folder:

1. **`risk_analysis.png` (Bar Chart):**
* **Finding:** Traders increase position sizes by ~400% during "Extreme Greed" ($8,000 avg) compared to "Extreme Fear" ($2,000 avg).
* **Conclusion:** Risk appetite is strongly pro-cyclical.


2. **`volume_analysis.png` (Box Plot):**
* **Finding:** "Extreme Fear" periods show a wide distribution of volume with many high outliers, despite low individual trade sizes.
* **Conclusion:** Indicates panic selling and capitulation events.


3. **`pnl_analysis.png` (Scatter Plot):**
* **Finding:** "Greed" periods correlate with high PnL volatility (both large wins and large losses), whereas "Fear" periods show tighter clustering around break-even.



## 🚀 How to Run

1. Open `notebook_1.ipynb` in Google Colab.
2. Ensure the `csv_files` folder contains `fear_greed_index.csv` and `historical_data.csv`.
3. Run all cells sequentially.
4. The script will:
* Load and clean data.
* Perform the aggregation and merge.
* Save the resulting graphs automatically to the `outputs/` folder.



## 💡 Strategic Recommendation

Based on the analysis, the report recommends a **Dynamic Position Sizing** strategy: automatically capping maximum trade sizes when the Sentiment Index exceeds 75 (Extreme Greed) to protect capital from the high-variance outcomes observed in the data.

