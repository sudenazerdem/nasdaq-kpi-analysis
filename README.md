# nasdaq-kpi-analysis
NASDAQ Stock Price Data Quality KPI Analysis
# Data Card — NASDAQ Stock Price Dataset

## 1. Source of Data

- **Provider:** Yahoo Finance API (via `yfinance` Python library)
- **Exchange:** NASDAQ (National Association of Securities Dealers Automated Quotations)
- **Data type:** Daily closing price (USD)
- **Collection date:** April 2026
- **Interval:** 1 business day
- **Format:** CSV, one file per company

| Ticker | Company | Period | Trading Days |
|--------|---------|--------|--------------|
| NVDA | NVIDIA Corporation | 2024-01-02 → 2024-12-31 | 252 |
| MSFT | Microsoft Corporation | 2024-04-01 → 2024-12-31 | 191 |
| PLTR | Palantir Technologies | 2024-07-01 → 2024-12-31 | 128 |
| TSLA | Tesla Inc. | 2024-10-01 → 2024-12-31 | 64 |
| META | Meta Platforms Inc. | 2024-12-02 → 2024-12-31 | 21 |

Each dataset contains two columns: `Date` and `Close` (closing price in USD).

---

## 2. Descriptive Statistics

| Ticker | Count | Mean | Std | Min | Max |
|--------|-------|------|-----|-----|-----|
| NVDA | 252 | $107.77 | $26.95 | $47.54 | $148.82 |
| MSFT | 191 | $419.97 | $15.55 | $383.44 | $461.32 |
| PLTR | 128 | $44.47 | $17.43 | $24.09 | $82.38 |
| TSLA | 64 | $321.74 | $79.85 | $213.65 | $479.86 |
| META | 21 | $605.85 | — | — | — |

---

## 3. KPI Results

### KPI A — Completeness
Measures the percentage of non-missing values in the dataset.

| Ticker | Total Rows | Missing | Completeness |
|--------|-----------|---------|--------------|
| NVDA | 252 | 0 | 100.00% |
| MSFT | 191 | 0 | 100.00% |
| PLTR | 128 | 0 | 100.00% |
| TSLA | 64 | 0 | 100.00% |
| META | 21 | 0 | 100.00% |

All 5 datasets are fully complete with no missing values.

---

### KPI B — Latency
Measures how old the data is (days between last record and today).

| Ticker | First Record | Last Record | Data Age (days) |
|--------|-------------|-------------|-----------------|
| NVDA | 2024-01-02 | 2024-12-31 | 471 |
| MSFT | 2024-04-01 | 2024-12-31 | 471 |
| PLTR | 2024-07-01 | 2024-12-31 | 471 |
| TSLA | 2024-10-01 | 2024-12-31 | 471 |
| META | 2024-12-02 | 2024-12-31 | 471 |

All datasets end at 2024-12-31, meaning the data is approximately 471 days old.

---

### KPI C — Accuracy
Measures the percentage of valid records (no negative or zero prices).

| Ticker | Negative | Zero | Outliers (IQR) | Accuracy |
|--------|----------|------|----------------|----------|
| NVDA | 0 | 0 | 0 | 100.00% |
| MSFT | 0 | 0 | 3 | 100.00% |
| PLTR | 0 | 0 | 0 | 100.00% |
| TSLA | 0 | 0 | 0 | 100.00% |
| META | 0 | 0 | 0 | 100.00% |

All prices are positive and valid. MSFT has 3 statistical outliers detected via IQR method, but these are real market prices — not data errors.

---

### KPI D — Consistency
Measures data type uniformity, duplicate rows, and unexpected date gaps.

| Ticker | Data Type | Duplicates | Large Gaps (>3 days) |
|--------|-----------|------------|----------------------|
| NVDA | float64 | 0 | 5 |
| MSFT | float64 | 0 | 2 |
| PLTR | float64 | 0 | 1 |
| TSLA | float64 | 0 | 0 |
| META | float64 | 0 | 0 |

All datasets use consistent `float64` data type with zero duplicates. Large gaps in NVDA, MSFT, and PLTR correspond to holiday periods (e.g. Christmas, New Year) — not data quality issues.

---

## 4. Conclusion

The Yahoo Finance API provides high-quality stock market data for all 5 NASDAQ companies analyzed. Key findings:

- **Completeness:** 100% across all datasets — no missing values detected.
- **Latency:** All data ends at 2024-12-31, making it approximately 471 days old. For real-time AI model training, more recent data would be required.
- **Accuracy:** 100% accurate — no negative or zero prices. MSFT's 3 outliers are legitimate market movements, not errors.
- **Consistency:** All datasets use the same data type (float64), have zero duplicates, and date gaps are fully explained by public holidays.

**Overall assessment:** This dataset is clean, consistent, and reliable. It would be suitable for training AI models for stock price prediction, trend analysis, or financial forecasting. The main limitation is latency — the data is from 2024 and does not reflect current market conditions. For production AI systems, a real-time data pipeline would be recommended.

---

*Dataset collected using [Yahoo Finance API](https://pypi.org/project/yfinance/) | Analysis notebook: [KPI_Project.ipynb](KPI_Project.ipynb)*
