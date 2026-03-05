# Nifty 500 Analytics Dashboard
### From Chaos to Clarity: Transforming 30 Years of Indian Stock Market Data into Actionable Insights

---

## Executive Summary

This project presents an end-to-end analytics pipeline built on 30 years of historical data for all 500 stocks in India's Nifty 500 index (1996–2025). Using Python for data engineering and Power BI for visualization, raw price data is converted into meaningful financial metrics — returns, volatility, and risk-adjusted performance — and surfaced through an interactive dashboard.

---

## Project Overview

What began as a mathematics poster competition entry evolved into a full-scale analytics solution demonstrating how mathematics, statistics, Python, and data visualization work together to solve complex financial problems.

The dashboard enables users to:

- Compare any stock within the Nifty 500
- Measure risk and return across custom date ranges
- Identify top and bottom performers by risk-adjusted return
- Analyze long-term market behavior interactively

---

## Event Details

**Presented at:** Dr. S. B. Nimse Amrit Mahotsav – Poster Exhibition  
**Date:** November 12, 2025  
**Venue:** Mathematics Department, New Arts, Commerce and Science College, Ahmednagar  

**Organized by:** Mathematics Department (NACSC), Savitribai Phule Pune University, Indian Mathematical Society, Alumni Association

---

## Project Team

| Name | Role |
|---|---|
| Girish Sabale | Project Lead, Dashboard Design & Visualization |
| Ganesh Gangarde | Data Collection & Integration Pipeline |
| Babita Mourya | Data Transformation & Statistical Analysis |

---

## Problem Statement

Analyzing 500 stocks over three decades presents several challenges:

- Massive data volume requiring efficient storage and processing
- Missing values caused by market holidays and trading halts
- Inconsistent data formats across sources
- Raw stock prices that are not directly comparable across stocks or time periods

Meaningful analysis requires transformation from raw prices into percentage returns, volatility, and risk-adjusted metrics.

---

## Pipeline Overview

The solution is structured as a six-phase analytics pipeline.

### Phase 1 — Data Collection
- **Source:** Yahoo Finance via the `yfinance` Python library
- **Scope:** Daily OHLC prices for 500 stocks from 1996 to 2025
- **Output:** 500 individual CSV files (~500 MB total)

### Phase 2 — Data Consolidation
- Extracted `Date` and `Close Price` from each file
- Merged all 500 files into a single master dataset using `Date` as the join key
- **Result:** One CSV with 501 columns (Date + 500 stock tickers)

### Phase 3 — Price-to-Returns Conversion
- Applied forward-fill to handle missing values from non-trading days
- Converted closing prices to daily percentage returns

```
Daily Return = ((Price_today - Price_yesterday) / Price_yesterday) × 100
```

### Phase 4 — Power BI Transformation
- **Problem:** 500 stock columns (wide format) cannot be filtered or visualized efficiently
- **Solution:** Unpivot transformation in Power Query converts wide to long format
- **Result:** Three-column structure — `Date`, `Stock Name`, `Daily Return`
- Fixed data type issues: converted `Daily Return` from text to decimal and replaced NaN/error values

### Phase 5 — Analytics Engine (DAX Measures)

**Average Daily Return**
```dax
AVERAGE(Returns[Daily Return])
```

**Volatility (Standard Deviation)**
```dax
STDEV.P(Returns[Daily Return])
```

**Annualized Sharpe Ratio**
```dax
(Avg Daily Return / Volatility) * SQRT(252)
```

**Cumulative Trend Line** — implemented with error handling for long time series stability.

### Phase 6 — Dashboard Design

**Page 1: Welcome Screen**
- Project overview and team details
- Navigation to the Insights Dashboard

**Page 2: Insights Dashboard**

*Controls:*
- Stock Selector (all 500 stocks)
- Date Range Slicer

*Key Metrics:*
- Average Daily Return
- Volatility
- Sharpe Ratio

*Visualizations:*
- Stock Performance Line Chart
- Risk–Return Treemap (all 500 stocks)
- Top 10 and Bottom 10 Sharpe Ratio Stocks
- Top 10 Most Volatile Stocks

---

## Mathematical & Statistical Foundations

**Statistics:** Mean, Standard Deviation, Percentage Change  
**Financial Mathematics:** Daily Returns, Risk vs. Return, Sharpe Ratio, Annualization Factor (√252)  
**Data Science:** Wide-to-long normalization, time-series analysis, error handling, pipeline optimization

---

## Challenges & Solutions

| Challenge | Solution |
|---|---|
| Massive data volume | Incremental merging and optimized pandas operations |
| Missing data from market holidays | Forward-fill interpolation |
| NaN values imported as text strings | Data type conversion and explicit error replacement |
| Dashboard performance lag | Optimized DAX measure design |
| Tight competition deadline | Clear division of responsibilities across team members |

---

## Dataset Scale

| Attribute | Value |
|---|---|
| Stocks | 500 (Nifty 500 Index) |
| Time Period | 1996–2025 |
| Total Records | ~500,000+ data points |
| Final PBIX File Size | 500+ MB |

---

## How to Reproduce

1. Run the Python scripts to download historical stock data using `yfinance`
2. Merge the 500 individual CSV files into a single master dataset
3. Convert price data into daily percentage returns
4. Load the master CSV into Power BI Desktop
5. Apply Power Query → Unpivot Columns to normalize the dataset
6. Create DAX measures for return, volatility, and Sharpe Ratio
7. Refresh visuals and explore insights

---

## Tools & Technologies

- **Python 3.x** — `pandas`, `yfinance`, `os`
- **Power BI Desktop**
- **Power Query (M)**
- **DAX**

---

## Future Enhancements

**Technical**
- Live market data integration
- Predictive analytics using machine learning
- Portfolio optimization modeling
- Correlation and sector-level analysis

**Usability**
- Mobile-responsive layout
- Exportable reports
- Saved views and alert thresholds

**Scalability**
- Cloud database backends (Azure SQL / Snowflake)
- Incremental data refresh
- Expansion to global market indices

---

## Key Learnings

- Real-world financial data is inherently messy and requires deliberate cleaning
- Data structure decisions have a greater impact on performance than tool selection
- Simple, robust solutions outperform complex ones in production environments
- Clear team roles and task ownership accelerate delivery under time constraints
- Statistical rigor transforms raw numbers into genuine decision-making tools

---

## Contact

**Girish Sabale** — Project Lead, Data Visualization  
LinkedIn: [linkedin.com/in/girishsabale](https://linkedin.com/in/girishsabale)

---

*Mathematics is not just theoretical — it is operational. When paired with automation, statistics, and visualization, it becomes a powerful engine for decision-making.*
