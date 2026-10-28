
<p align="center"><img src="screenshots/01-executive-summary.png" alt="Geographic Analysis dashboard" width="900"></p>

<p align="center"><img src="screenshots/02-geographic-analysis.png" alt="Geographic Analysis dashboard" width="900"></p>

<p align="center"><img src="screenshots/03-product-detail.png" alt="Product Detail dashboard" width="900"></p>


<p align="center"><img src="screenshots/04-customer-analysis.png" alt="Customer Analysis dashboard" width="900"></p>

# Power BI Sales Analytics Dashboard

**An interactive sales analysis project built with Microsoft Power BI**

This project is part of my Data Analytics learning journey through DigiSkills. I created a multi-page Power BI report using the Adventure Works Cycles business scenario to explore sales performance, product results, geographic distribution, and customer patterns.

The aim is to present business data in a clear format and make it easier to explore key performance indicators, trends, and differences across products, regions, and customers.

## Project at a Glance

- **Tool:** Microsoft Power BI Desktop
- **Business scenario:** Adventure Works Cycles
- **Report pages:** Executive Summary, Map, Product Detail, and Customer Detail
- **Main focus:** Sales, profit, orders, returns, product performance, geography, and customer analysis

## Dashboard Preview

> If your image filenames are different, update the paths below to match the exact filenames in your `screenshots/` folder.

### 1. Executive Summary

The Executive Summary brings key sales indicators and trends into one view. It includes KPI cards, monthly performance, product information, and interactive slicers.

![Executive Summary dashboard](screenshots/executive-summary.png)

**What this page helps explore**
- Total revenue, total profit, and order volume
- Return rate
- Monthly sales and profit trends
- Product and category performance
- Filtering by continent, month, and year

### 2. Geographic Analysis

The map page helps users explore order distribution across geographic areas. The report includes a continent slicer and a map using country and sales-related measures.

![Geographic analysis dashboard](screenshots/geographic-analysis.png)

**What this page helps explore**
- Geographic distribution of orders
- Differences between countries and continents
- Revenue, profit, cost, and order measures by location

### 3. Product Detail

The Product Detail page is configured for drillthrough by product name. The current report configuration includes the Mountain Tire Tube example. It combines product-level KPIs with weekly revenue and order trends.

![Product detail dashboard](screenshots/product-detail.png)

**What this page helps explore**
- Product revenue and order performance
- Return activity
- Weekly revenue trends
- Revenue forecasting visuals

Forecasts are estimates and should not be treated as guaranteed future results.

### 4. Customer Detail

The Customer Detail page is configured as a tooltip page. Its visuals include a customer table, customer-level revenue and order measures, customer breakdowns, and monthly trends. The page is designed to provide additional customer context when supported by the report's interactions.

![Customer detail dashboard](screenshots/customer-detail.png)

**What this page helps explore**
- Customer-level revenue and orders
- Customer comparisons
- Customer breakdowns by available attributes
- Monthly order and revenue patterns

## Key Metrics

The Executive Summary preview displays these headline values in the shown report view:

| Metric | Displayed value |
|---|---:|
| Total Revenue | $18.51M |
| Total Profit | $7.86M |
| Total Orders | 22,534 |
| Return Rate | 2.14% |

These are the values visible in the portfolio screenshot, not a guarantee that the same values will appear under every filter selection. Before using them for business decisions, check the measure definitions and the current report filters in Power BI.

## Business Questions

The report is designed to help explore questions such as:

1. How do revenue and profit change over time?
2. How do order volumes differ across geographic areas?
3. Which products contribute most to revenue and profit?
4. How do order and return measures vary by product?
5. Which customers generate the most revenue or orders?
6. What patterns appear in monthly sales and customer activity?

## Key Business Insights

I will document specific findings here after checking the report values and filter context. The aim is to report evidence-based observations rather than make assumptions from the chart design alone.

Potential areas to investigate include:
- The products or categories with the highest revenue or profit.
- Geographic areas with the highest order volume.
- Changes in revenue and profit over the reporting period.
- Customers with the highest order or revenue values.
- Products or periods with notable return activity.

*These are analysis questions, not confirmed findings. Add a finding only after validating the relevant values in the report.*

## Interactive Features

The report configuration includes:
- Continent, month, and year slicers on the Executive Summary.
- A continent slicer on the map page.
- Product-name drillthrough on the Product Detail page.
- A Customer Detail tooltip page for additional customer context.

The effect of each filter can depend on the visual interactions configured in Power BI. Test the report before describing any additional cross-filtering behavior.

## Measures Referenced in the Report

The report visuals reference measures including:
- Total Revenue
- Total Profit
- Total Orders
- Return Rate
- Total Cost
- Total Returns (the report's internal measure label appears as `Total Retuens`)
- Revenue, order, and return comparisons across time

This list identifies measures referenced by report visuals. Their DAX formulas and business definitions should be reviewed in Power BI before they are documented in detail.

## Tools and Skills

**Tool used:** Microsoft Power BI Desktop

This project demonstrates report-building and business-visualization work in areas such as:
- KPI presentation
- Time-based trend analysis
- Geographic analysis
- Product performance analysis
- Customer analysis
- Interactive slicers and drillthrough
- Report layout and visual consistency

The exact data-preparation steps, data-model relationships, and DAX logic should be documented after reviewing the model and formulas.

## Technical Approach

The project follows a business-focused reporting workflow:

1. **Define the questions** — identify the sales and customer areas to explore.
2. **Review the data and measures** — understand the fields and calculations used in the report.
3. **Build the report pages** — organize the analysis into executive, geographic, product, and customer views.
4. **Add interactions** — use slicers, drillthrough, and tooltip behavior where configured.
5. **Review the results** — check values, filter behavior, labels, and visual clarity before drawing conclusions.

This describes the reporting workflow at a high level. It does not claim specific Power Query transformations or data-model relationships that have not yet been verified.

## Project Files

| File or folder | Purpose |
|---|---|
| `DigiSkills-Sales-Analytics.pbix` | Main Power BI report |
| `screenshots/` | Dashboard preview images |
| `README.md` | Project documentation |

## How to View the Report

1. Download or clone this repository.
2. Open `DigiSkills-Sales-Analytics.pbix` in Microsoft Power BI Desktop.
3. Explore the report pages.
4. Try the available slicers and drillthrough interactions.
5. Review the measures and filter context before interpreting the results.

Power BI Desktop is required to open and interact with the PBIX file.

## Scope and Limitations

This is a learning and portfolio project, not a live business reporting system. The analysis reflects the dataset, measures, filters, and report design included in the PBIX file.

Forecasts are estimates. Business conclusions should be based on the underlying data and verified measure definitions. The KPI values shown above come from the portfolio screenshot and may change with report filters.

## About This Project

I created this project to develop my data analysis and business intelligence skills through practical dashboard work. It gave me an opportunity to organize sales-related information into several views and practise communicating data through visual reports.

I am continuing to improve my skills in Power BI, analytical thinking, and presenting findings in a clear and practical way. Feedback and suggestions are welcome.
