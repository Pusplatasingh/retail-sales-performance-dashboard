# Retail Sales Performance Dashboard

An end-to-end Power BI dashboard analyzing retail sales, regional profitability, and the impact of discounting on profit margins using the Sample Superstore dataset (2014–2017, ~9,800 orders).

## Problem

A retail business needs visibility into where it makes money and where it doesn't — across time, geography, and product lines — in order to make informed decisions about pricing, discounting, and regional strategy. Raw transactional data alone doesn't answer this; it needs to be modeled and visualized to surface actionable patterns.

## Solution

I built a 3-page interactive Power BI dashboard covering:

- **Executive Overview** — high-level KPIs, sales trend over time, and category revenue split
- **Regional Analysis** — geographic breakdown of sales and profitability by region and state
- **Product & Discount Insight** — identifying which sub-categories and products are profitable vs. loss-making, and how discounting affects margin

The dashboard is built on a custom data model with a dedicated Date table for time intelligence, calculated columns for discount bucketing, and DAX measures for all core business metrics. Full measure documentation is in `docs/DAX_measures.md`.

## Key Metrics Tracked

- Total Sales, Total Profit, Profit Margin %
- Total Orders, Average Order Value
- Year-over-Year Sales Growth
- Regional and state-level profitability
- Discount rate vs. profit correlation

## Screenshots

### Executive Overview
![Executive Overview](screenshots/overview_page.png)

### Regional Analysis
![Regional Analysis](screenshots/regional_page.png)

### Product & Discount Insight
![Product Insight](screenshots/product_page.png)

## Tech Stack

- **Power BI Desktop** (Free) — data modeling, DAX, visualization
- **Power Query** — data cleaning and transformation
- **DAX** — calculated columns, measures, time intelligence

## How to Use

1. Download `retail_sales_dashboard.pbix` from the `/powerbi` folder
2. Open in Power BI Desktop (free download from Microsoft)
3. Explore using the Date range slider and Region filters on each page

## Key Insights Found

- **Discounting is directly eroding margin in specific sub-categories.** The Tables sub-category generated roughly 185K in sales but posted a **-16K loss in profit** — one of the clearest cases in the dataset of high sales volume masking an unprofitable product line, driven by heavier-than-average discount rates.

- **Some of the highest-selling states are the least profitable.** Texas ranks among the top 5 states by total sales (133K) but carries a **-18.95% profit margin**, the worst in the top 10. Ohio (-24.67%) and Illinois (-19.93%) show the same pattern — strong revenue undermined by aggressive discounting or pricing issues specific to those states.

- **Profit is concentrated in two regions.** West and East together account for roughly **77K and 65K in profit respectively**, well ahead of South (32K) and Central (26K), despite all four regions showing more comparable sales volumes — indicating regional differences in discount strategy or cost structure are driving the profit gap more than revenue itself.

- **The discount-profit relationship is visible at the product level, not just in aggregate.** The Bottom 10 products by profit are dominated by large discounted furniture items (conference tables, printers), while the Top 10 are led by lower-discount office electronics (copiers, printers sold near list price) — reinforcing that discount depth, not category alone, is the strongest driver of loss.

*(See `docs/DAX_measures.md` for full documentation of all measures and calculated columns used.)*

## Future Improvements

- Add a forecasting page using Power BI's built-in forecasting on the trend line
- Incorporate a what-if parameter to simulate the profit impact of capping discounts at a threshold
- Automate data refresh via a scheduled Power BI Service dataflow (would require Pro license)

## Author

Pusplata Singh
[LinkedIn](https://linkedin.com/in/pusplatasingh) | pusplatasingh1104@gmail.com
