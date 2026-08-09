# DAX Measures Documentation

## Core Measures

### Total Sales
```dax
Total Sales = SUM(Orders[Sales])
```
Sums the Sales column across all orders. Primary revenue metric used throughout the dashboard.

### Total Profit
```dax
Total Profit = SUM(Orders[Profit])
```
Sums the Profit column across all orders.

### Profit Margin %
```dax
Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)
```
Profit as a percentage of sales. Uses DIVIDE to safely return 0 instead of an error when Total Sales is 0.

### Total Orders
```dax
Total Orders = DISTINCTCOUNT(Orders[Order ID])
```
Counts unique orders. DISTINCTCOUNT is used instead of a row count because a single order can span multiple rows (one per product line item).

### Avg Order Value
```dax
Avg Order Value = DIVIDE([Total Sales], [Total Orders], 0)
```
Average revenue generated per order.

### Avg Discount %
```dax
Avg Discount % = AVERAGE(Orders[Discount])
```
Average discount rate applied across all orders. Used in the discount vs. profit analysis.

### Total Quantity Sold
```dax
Total Quantity Sold = SUM(Orders[Quantity])
```
Total number of units sold across all orders.

---

## Time Intelligence Measures

### Sales PY (Prior Year)
```dax
Sales PY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DateTable[Date]))
```
Returns Total Sales for the same period one year earlier, using a dedicated Date table marked as the official date table for time intelligence.

### Sales Growth %
```dax
Sales Growth % = DIVIDE([Total Sales] - [Sales PY], [Sales PY], 0)
```
Year-over-year growth rate, comparing current period sales to the prior year.

### Sales YTD
```dax
Sales YTD = TOTALYTD([Total Sales], DateTable[Date])
```
Running total of sales from the start of the calendar year to the latest date in the current filter context.

---

## Ranking Measures

### Product Rank by Sales
```dax
Product Rank by Sales = RANKX(ALL(Orders[Product Name]), [Total Sales])
```
Ranks each product by total sales, ignoring any active filters on Product Name (using ALL), so the ranking reflects each product's position across the full catalog.

---

## Calculated Columns (Data Model)

### Year-Month
```dax
Year-Month = FORMAT(DateTable[Date], "YYYY-MM")
```
Text label used for chronological grouping in trend charts (e.g., "2014-01").

### Year-Month Sort
```dax
Year-Month Sort = YEAR(DateTable[Date]) * 100 + MONTH(DateTable[Date])
```
Numeric sort key used to force Year-Month to display in correct chronological order in visuals, since text fields sort alphabetically by default.

### Discount Band (Power Query)

if [Discount] = 0 then "No Discount"
else if [Discount] <= 0.2 then "Low (0-20%)"
else if [Discount] <= 0.4 then "Medium (20-40%)"
else "High (40%+)"

Buckets the continuous Discount value into readable categories for simpler visual grouping.

---

## Notes on Conditional Formatting Logic

For the Profit Margin % conditional formatting (used in the Regional Analysis table), rules were applied using raw decimal (Number) thresholds rather than percentage-formatted values, since Profit Margin % is stored internally as a decimal (e.g., 0.15 for 15%) despite being displayed as a percentage:
- `< 0` → Red (loss-making)
- `0` to `0.10` → Yellow (weak margin, under 10%)
- `>= 0.10` → Green (healthy margin, 10%+)