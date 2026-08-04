# 📊 Interactive KPI Dashboard — Superstore Sales

*A 1-page interactive sales dashboard built in Google Sheets, covering regional performance, category trends, and top customers.*

🔗 **Live Dashboard:** *(https://docs.google.com/spreadsheets/d/10HTrc656qbuX3ehX-AfILYh_PX9PJS-hEPQSDziBCsw/edit?usp=sharing)*

---

## 1. Project Objective
This dashboard tracks sales performance across regions, product categories, and time for a retail superstore, with an interactive region filter that lets a viewer drill into performance for any single region or view the business as a whole.

---

## 2. Data Source
- **Dataset name:** Superstore Sales Dataset
- **Source:** Kaggle (Rohit Sahoo)
- **Size:** 4,922 unique orders (multiple product rows per order)
- **Date range covered:** 2014–2018
- **Columns available:** Row ID, Order ID, Order Date, Ship Date, Ship Mode, Customer ID, Customer Name, Segment, Country, City, State, Postal Code, Region, Product ID, Category, Sub-Category, Product Name, Sales

---

## 3. Data Cleaning

- [x] Verified Sales column was already numeric — no fix needed
- [x] Checked Category, Sub-Category, and Region columns for blank cells and inconsistent casing — none found
- [x] Verified Order Date / Ship Date — found they were stored as text in mixed/inconsistent date formats, causing parsing errors
- [x] Fixed date parsing using a custom formula combining `DATE`, `LEFT`, `MID`, and `RIGHT` to correctly read the text as DD/MM/YYYY, avoiding the default US MM/DD/YYYY misread
- [x] Applied the fix via helper columns, verified the results, then pasted values over the original Order Date / Ship Date columns and removed the helper columns
- [x] Formatted both date columns consistently (Format → Number → Date)

---

## 4. KPIs Chosen

| KPI | Result | Why it matters |
|---|---|---|
| Total Sales | $2,261,536.78 | Overall business performance at a glance |
| Total Orders | 4,922 | Volume of transactions |
| Average Sale per Order | $459.48 | Order value trends |
| Top Region by Sales | West ($710,219.68) | Where revenue is concentrated |
| Top Category by Sales | Technology ($827,455.87) | Best-performing product lines |
| Sales Trend Over Time | Built as a monthly pivot (Jan–Dec) | Seasonality and growth patterns |
| Top 5 Customers by Sales | Sean Miller ($25,043.05) leads, followed by Tamara Chand, Raymond Buch, Tom Ashbrook, Adrian Barton | Key accounts driving revenue |

**Build notes:**
- Total Sales, Total Orders, and Average Sale per Order were built with `SUM`, `COUNTUNIQUE`, and a simple division formula
- Top Region, Top Category, Sales Trend, and Top Customers were each built as separate pivot tables (Rows = category field, Values = SUM of Sales)
- Sales Trend pivot groups Order Date by month across all years combined, useful for spotting seasonality (e.g., Nov/Dec appear to be peak months)
- Top 5 Customers was sorted descending by SUM of Sales within the pivot table editor, then manually styled into a clean KPI card for the dashboard layout

---

## 5. Dashboard Build

- **Layout:** Full-width title bar ("Superstore Sales Dashboard") at the top, followed by KPI cards (Total Sales, Total Orders, Average Sale per Order) and a Top 5 Customers card side by side with the Region filter dropdown, then three chart sections stacked below — Regional Performance and Product Category Breakdown side by side, Monthly Sales Breakdown spanning the full width underneath. Raw pivot table data was moved to a separate "Pivot data" tab to keep the Dashboard tab to a single clean page.
- **Filters/interactivity:** A dropdown (Data Validation) lets the user filter by Region (Central/East/South/West/All). Total Sales, Total Orders, and Average Sale per Order all update live via `IF` + `SUMIF`/`SUMIFS` formulas referencing the dropdown cell.
- **Charts used:** Column chart for Sales by Region, pie chart for Sales by Category, line chart for Sales trend by month — all recolored to a consistent navy/gold/grey palette.
- **Functions/features used:** SUM, COUNTUNIQUE, SUMIF/SUMIFS, a helper column for counting unique orders under a filter, Data Validation (dropdown), Pivot Tables, and chart customization (colors, titles).
- **Design polish:** Removed gridlines, added a colored header bar above each chart section, unified all fills/text/borders to one navy/white/gold palette, matched KPI card row heights and borders for a consistent "card" look.

---

## 6. Screenshots

![Dashboard](Images/dashboard.png)

---

## 7. Insights

1. The West region generates the most revenue ($710,219.68), notably higher than the South region, its weakest performer ($389,151.46).
2. Technology is the top-performing category ($827,455.87), narrowly ahead of Furniture and Office Supplies, which are close to each other.
3. Sales show clear seasonality — dips in the early and mid-year months, with a strong climb from September through November before tapering slightly in December.

---

## 8. Tools Used
- Google Sheets
- Pivot Tables, SUMIF/SUMIFS, COUNTUNIQUE, Data Validation (dropdown filters), chart customization, custom date-parsing formulas

---

## 9. Reflection

The trickiest part of the data cleaning stage was realizing the date parsing issue wasn't a missing-format problem but a locale mismatch (DD/MM vs MM/DD). Building the KPI engine involved a mix of simple formulas (SUM, COUNTUNIQUE) and pivot tables for category-based breakdowns. A couple of early mistakes — a pivot table's data range only covering one column, and summing the wrong field — were good reminders to double check ranges and fields before trusting the numbers.
