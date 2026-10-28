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

---

## Core DAX Calculations

Below are the primary DAX measures written for this dashboard:

```dax
// Total Revenue
Total Revenue = 
SUMX(
    'Sales_Data', 
    'Sales_Data'[OrderQuantity] * RELATED('Products_Lookup'[ProductPrice])
)

// Total Profit
Total Profit = 
[Total Revenue] - SUMX(
    'Sales_Data', 
    'Sales_Data'[OrderQuantity] * RELATED('Products_Lookup'[ProductCost])
)

// Total Orders
Total Orders = DISTINCTCOUNT('Sales_Data'[OrderNumber])

// Return Rate
Return Rate = DIVIDE([Total Returns], [Total Orders], 0)
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

