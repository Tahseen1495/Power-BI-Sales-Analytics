# Power BI Sales Analytics Dashboard

**An interactive multi-page business intelligence report built with Microsoft Power BI**

This project was developed during the DigiSkills Data Analytics & Business Intelligence course under the guidance and instruction of **Sir Jahangir Sachwani**. Using the Adventure Works Cycles business scenario, the dashboard transforms complex sales data into interactive views to help business stakeholders explore revenue trends, geographic performance, product margins, and customer behavior.

---

## Project at a Glance

- **Tool:** Microsoft Power BI Desktop
- **Business Scenario:** Adventure Works Cycles
- **Report Pages:** Executive Summary, Geographic Analysis, Product Detail, Customer Detail
- **Main Focus Areas:** Revenue, profit, order volume, product return rates, regional performance, and customer segmentation

---

## Dashboard Preview

### 1. Executive Summary
The Executive Summary brings key sales indicators and trends into one view. It includes live KPI cards, monthly performance, product information, and interactive slicers.

<p align="center"><img src="screenshots/01-executive-summary.png" alt="Executive Summary dashboard" width="900"></p>

**What this page covers:**
- Revenue, profit, order volume, and return rate
- Monthly sales and profit trends
- Product and category performance
- Filtering by continent, month, and year

### 2. Geographic Analysis
The Map page helps users explore order distribution across geographic areas. It includes a continent slicer and location-based visuals.

<p align="center"><img src="screenshots/02-geographic-analysis.png" alt="Geographic Analysis dashboard" width="900"></p>

**What this page covers:**
- Geographic distribution of orders
- Regional comparisons between countries and continents
- Location-based sales and order metrics

### 3. Product Detail
The Product Detail page is configured for item-level deep dives with dynamic drillthrough capabilities (demonstrated using the *Mountain Tire Tube*).

<p align="center"><img src="screenshots/03-product-detail.png" alt="Product Detail dashboard" width="900"></p>

**What this page covers:**
- Product revenue and order performance
- Return volume tracking
- Weekly revenue trendlines
- Native Power BI forecasting visuals *(Forecasts are estimates based on historical data)*

### 4. Customer Detail
The Customer Detail page is configured as an interactive report page tooltip to provide immediate customer context without cluttering primary reporting canvases.

<p align="center"><img src="screenshots/04-customer-analysis.png" alt="Customer Analysis dashboard" width="900"></p>

**What this page covers:**
- Customer-level revenue and order counts
- Top customer rankings and comparisons
- Customer breakdowns by available demographic attributes
- Monthly order and revenue patterns

---

## Key Metrics Summary

| Metric | Displayed Value |
|---|---:|
| **Total Revenue** | $18.51M |
| **Total Profit** | $7.86M |
| **Total Orders** | 22,534 |
| **Return Rate** | 2.14% |

*Note: Headline values represent default filter context and will adjust based on report slicer selections.*

---
## 🔍 Key Business Findings & Operational Insights

Analyzing the Adventure Works Cycles dataset across the report pages highlighted several important business insights:

* **Strong Revenue and Margins:** The business generated **$18.51M in total revenue** and **$7.86M in net profit** across 22,534 customer orders. This shows a solid overall profit margin and healthy business baseline.
* **Controlled Return Rates:** The overall return rate is low at **2.14%**. However, checking individual products—like the *Mountain Tire Tube*—shows return spikes during specific months, which suggests potential seasonal issues or product quality concerns.
* **Geographic Concentration:** The map view shows that sales are heavily concentrated in North America and Europe. This indicates strong core markets, but also points to untapped growth opportunities in other regions.
* **Impact of High-Value Products:** Custom DAX measures, such as `High Ticket Orders` and 3-month rolling totals (`03-Month Cum Orders`), reveal that expensive products drive a large portion of steady monthly revenue, even when order quantities are lower.
* **Key Customer Contributions:** Using interactive tooltips on top customers (such as *Mr. Maurice Shan*) shows that repeat buyers make up a significant portion of total revenue, proving the value of targeted customer retention efforts.
---
  ## Data Architecture & Modeling

To ensure optimal performance and accurate filter context propagation, the report follows a clean **Star Schema** dimensional model:

| Table Name | Entity Type | Purpose |
|---|---|---|
| `Sales_Data` | Fact Table | Primary sales transactions, quantities, and prices |
| `Returns_Data` | Fact Table | Product return records and quantities |
| `Calendar_Lookup` | Dimension | Centralized date dimension enabling time-intelligence functions |
| `Customers_Lookup` | Dimension | Customer demographics, locations, and names |
| `Products_Lookup` | Dimension | Product names, SKU details, costs, and list prices |
| `Product_Subcategories_Lookup` | Dimension | Intermediate product categorization |
| `Product_Categories_Lookup` | Dimension | High-level product categories |
| `Territories_Lookup` | Dimension | Geographic regions, countries, and continents |



<p align="Left"><img src="screenshots/Data Normalization.jpeg"width="900"></p>

---
## 🧠 Key Learnings & Technical Takeaways

Building this executive sales analytics dashboard provided valuable hands-on experience across the entire business intelligence lifecycle:

* **Star Schema Optimization:** Mastered centralized dimensional modeling (Star Schema) to optimize Power BI performance. Separating transactional data (`Sales_Data`, `Returns_Data`) from lookup dimensions (`Calendar_Lookup`, `Products_Lookup`, `Customers_Lookup`) drastically simplified filter context propagation and accelerated report rendering.
* **Advanced DAX & Context Transition:** Gained deep expertise in utilizing `CALCULATE`, context modification (`ALL`, `ALLEXCEPT`), and Time Intelligence (`SAMEPERIODLASTYEAR`, `DATESYTD`, `DATEADD`). Understanding row-to-filter context transition was key for building accurate cumulative and comparative measures.
* **Executive UI/UX Design:** Implemented visual hierarchy standards using dark navy, slate blue, and gold accents alongside borderless cards and hidden gridlines to reduce cognitive load for stakeholders.
* **Data Hygiene & ETL:** Applied rigorous Power Query transformations (data type validation, null handling, key normalization) upfront to ensure high data integrity before DAX modeling.

---

## 💻 Core DAX Calculations & Modeling Logic

To power the dashboard's dynamic interactivity, time intelligence, and advanced filtering, the following custom DAX measures were authored:

### 1. Core Financial & Volume Measures
```dax
// Calculates total gross revenue from sales transactions and product prices
Total Revenue = 
SUMX(
    'Sales_Data', 
    'Sales_Data'[OrderQuantity] * RELATED('Products_Lookup'[ProductPrice])
)

// Computes net profit by subtracting total product costs from total revenue
Total Profit = 
[Total Revenue] - SUMX(
    'Sales_Data', 
    'Sales_Data'[OrderQuantity] * RELATED('Products_Lookup'[ProductCost])
)

// Counts unique transaction orders to avoid row-level duplication
Total Orders = DISTINCTCOUNT('Sales_Data'[OrderNumber])

// Computes overall return percentage relative to total orders
Return Rate = DIVIDE([Total Returns], [Total Orders], 0)
``` 
## 💻 Time Intelligence Measures
```dax
// Calculates Year-to-Date revenue using centralized calendar lookups
YTD Revenue = CALCULATE([Total Revenue], DATESYTD(Calendar_Lookup[Date]))

// Evaluates previous month revenue for comparative growth analysis
Prev.Month Revenue = CALCULATE([Total Revenue], DATEADD(Calendar_Lookup[Date], -1, MONTH))

// Tracks product returns from the prior month
Prev Month Return = CALCULATE([Total Returns], DATEADD(Calendar_Lookup[Date], -1, MONTH))
```
## 💻 Advanced Filtering & Custom Aggregations
```dax
// Determines the overall average retail price across all products
Overall Avg. Price = CALCULATE([Avg Retail Price], ALL(Products_Lookup))

// Filters orders exceeding the baseline average retail price
High Ticket Orders = CALCULATE([Total Orders], FILTER(Products_Lookup, Products_Lookup[ProductPrice] > [Overall Avg. Price]))

// Computes a rolling 3-month cumulative order volume
03-Month Cum Orders = CALCULATE([Total Orders], DATESINPERIOD(Calendar_Lookup[Date], MAX(Calendar_Lookup[Date]), -3, MONTH))
```
## Key Business Questions Answered

The dashboard is designed to help stakeholders explore and answer critical operational questions:
1. **Revenue & Profit Trends:** How do top-line revenue and net profit change across monthly and yearly timelines?
2. **Geographic Distribution:** Which countries and continents drive the highest order volumes and sales contributions?
3. **Product Performance:** Which product categories and individual items contribute most heavily to revenue and profitability?
4. **Return Activity:** How do product return rates vary across different inventory lines?
5. **Customer Segmentation:** Which individual customers generate the highest order frequency and revenue totals?


---

## Technical Workflow

The project followed an end-to-end business intelligence development lifecycle:
1. **Data Preparation & Transformation:** Utilized Power Query to clean raw datasets, handle data types, and normalize lookup fields.
2. **Data Modeling:** Established a robust Star Schema architecture connecting fact tables to centralized dimension lookup tables with proper relationship cardinalities.
3. **DAX Measure Development:** Authored custom DAX formulas for dynamic aggregations, profit calculations, and return rate tracking.
4. **Interactive Report Design:** Built multi-page layouts emphasizing executive clarity, borderless card containers, custom drillthroughs, and report-page tooltips.
5. **Quality Assurance:** Tested cross-filtering behavior, slicer propagation, and visual formatting across all canvas views before publication.

---

## Tools & Skills Demonstrated

* **Tool:** Microsoft Power BI Desktop
* **Core Competencies:** 
  * Star Schema Data Modeling
  * Power Query ETL & Data Cleaning
  * DAX (Data Analysis Expressions) & Time Intelligence
  * Geographic Data Visualization (Map Integration)
  * Executive UI/UX Design & Visual Hierarchy
  * Interactive Slicers, Drillthroughs, and Tooltip Configurations

---

## Project Files

| File or Folder | Purpose |
|---|---|
| `DigiSkills-Sales-Analytics.pbix` | Main Power BI interactive report file |
| `screenshots/` | High-resolution dashboard preview images |
| `README.md` | Comprehensive project documentation |

---

## How to View the Report

1. Clone or download this repository.
2. Open `DigiSkills-Sales-Analytics.pbix` using **Microsoft Power BI Desktop**.
3. Explore the report pages, test the interactive slicers, and use drillthrough/tooltip features to analyze findings.

*Note: Microsoft Power BI Desktop is required to open and interact with the `.pbix` source file.*

---

## Scope & Limitations

This is a portfolio and learning project designed to demonstrate business intelligence capabilities using the Adventure Works dataset. Insights reflect the specific filter context, measures, and data model structure included in the PBIX file. Forecast visuals are predictive estimates based on historical trends rather than guaranteed future outcomes.

---

## About This Project

Developed as part of my practical training in data analytics and business intelligence, this dashboard gave me the opportunity to transform raw operational data into structured, actionable visual reports. 

I am continuously working to sharpen my Power BI expertise, analytical thinking, and executive presentation standards. Feedback, suggestions, and professional connections are always welcome!

