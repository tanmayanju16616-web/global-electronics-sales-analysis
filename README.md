# Global Electronics Sales Analysis

Python and pandas analysis of a global electronics retailer. Five raw datasets are cleaned and merged into one analysis-ready table, revenue is normalised to USD, and the results are used to judge store efficiency, growth patterns and the effect of store age.

## Key Findings

| Metric | Value |
|---|---|
| Total revenue | **$55.35M** (62,884 sales lines) |
| Top category | Computers, **$19.1M** (35% of revenue) |
| Second category | Home Appliances, $10.7M (Computers and Home Appliances together are about 54%) |
| Weakest category | Games and Toys, $0.7M |
| Online channel (StoreKey 0) | **$11.4M**, about 21% of revenue and the largest single "store" |
| Best physical stores | Store 9 ($1.76M), Store 8 ($1.62M), Store 55 ($1.42M), Store 50 ($1.39M) |
| Best-selling products | Desktop PCs take all top 5 spots, led by WWI Desktop PC2.33 X2330 Black (550 units) |

**Business insights**
- **Bigger stores aren't always more efficient.** Revenue per square meter shows some smaller stores outperforming large ones, so floor space doesn't guarantee revenue. Recommendation: study the high-efficiency stores and review the large, low-efficiency ones.
- **Revenue is seasonal.** May–July are the strongest months and March–April the weakest across several countries. Europe grows faster but is more volatile; Canada is slower but steadier.
- **Store age:** stores aged 10–20 years generate most of the revenue, while the 5–10 year group lags and is a candidate for extra support.

## Approach
1. **Cleaning:** loaded five CSVs (customers, exchange rates, products, sales, stores), converted date columns to datetime, converted price columns from text (`$`, commas) to numbers, renamed overlapping country and state columns, and checked for duplicates (none) and missing values.
2. **Missing values:** 10 customer state codes (Napoli, Italy) identified; 1 store missing area; 79% of delivery dates missing, which is expected because only online orders (StoreKey 0) have deliveries.
3. **Merging:** joined sales with exchange rates (by date and currency), customers, products and stores into one table, `sales_full`.
4. **USD normalisation:** `Revenue_USD = Quantity × Unit Price USD × Exchange`, so revenue is comparable across currencies.
5. **Analysis:** revenue by category, store and product; revenue per square meter; month-on-month growth by store; revenue by store-age band.

## Metrics Used
```
Revenue per sqm = Total store revenue (USD) / Store area (sqm)      # physical stores only
MoM growth (%)  = (This month - Last month) / Last month × 100      # per store
Store age bands = 0–5, 5–10, 10–15, 15–20, 20+ years
```

## Notes and Limitations
- Store age is measured from today's date, so the bands can shift slightly when the notebook is run later.
- Online sales (StoreKey 0) are part of the store-age totals, so that analysis includes the online channel. Revenue per sqm excludes it.

## Tech Stack
Python · pandas · NumPy · Jupyter Notebook

## Run It
```bash
git clone https://github.com/tanmayanju16616-web/global-electronics-sales-analysis.git
cd global-electronics-sales-analysis
pip install -r requirements.txt
jupyter notebook Global_Electronics_Sales_Analysis.ipynb
```
The datasets are not included. Create a `Datasets/` folder and add `Customers.csv`, `Exchange_Rates.csv`, `Products.csv`, `Sales.csv` and `Stores.csv`.

## Author
**Anju Kanwar**
