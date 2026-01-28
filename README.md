# Dashboard 001
---
## 📊Sales Performance Dashboard | Power BI
---

### Project Overview
This Power BI dashboard provides insights into sales performance across regions, countries, products, and salespersons.  
It allows users to track revenue trends, top products, and units sold using interactive visuals and slicers.  
The dashboard emphasizes professional design with clear hierarchy, consistent colors, and readable typography.

---

### Dashboard Preview
📄 **View the dashboard design:** [sales_dashboard.pdf](sales_dashboard.pdf)

---

### Key Insights
📈 **Total Revenue:** $5 million – Strong overall sales performance  
📦 **Total Units Sold:** 2,000 units with an average unit price of $3,000 – High-value product portfolio  
🌏 **Top Country:** India generates the highest revenue  
🌍 **Top Region:** Europe leads in revenue performance  
💻 **Top Product Category:** Laptops contribute the highest share of total revenue  

---

### Dataset
**File:** `Sales_Data.xlsx`  
**Sheet:** `Sales`  

**Columns:**
- Date (Date)
- Region (Text)
- Country (Text)
- Product Category (Text)
- Product (Text)
- Salesperson (Text)
- Units Sold (Number)
- Unit Price (Number)
- Revenue (Number, pre-calculated)
  
---

## Visuals Included
- **Revenue by Region** (Bar Chart)
- **Top 10 Products** (Column Chart)
- **Units Sold Over Time** (Line Chart)
- **Sales by Salesperson** (Horizontal Bar Chart)
- **Revenue by Country** (Map Visual)
- **Key Metrics** (Card Visuals)

---

## Features
✅ **Interactive Slicers** – Filter by Date, Region, Country, Product, and Salesperson  
✅ **Cross-filtering** – Click on visuals to drill down into specific data  
✅ **Professional Design** – Consistent color scheme and intuitive layout  
✅ **KPI Indicators** – Quick view of total revenue, units sold, and average sales  
✅ **Trend Analysis** – Track sales performance over time  

---

## Requirements
- **Power BI Desktop** (latest version recommended)
- **Sales_Data.xlsx** file in the project folder
- Windows 10 or later (for Power BI Desktop)

---

## How to Use
1. **Open the Project**: Launch Power BI Desktop and open the dashboard file
2. **Load Data**: Ensure `Sales_Data.xlsx` is in the same folder or update the data source path
3. **Interact with Visuals**: Use slicers to filter data or click on chart elements for cross-filtering
4. **Analyze Trends**: Monitor revenue trends, identify top performers, and track regional performance
5. **Export Results**: Use Power BI's export features to share insights in PDF or PowerPoint format

---

## Data Refresh
- Update `Sales_Data.xlsx` with new sales records
- Refresh the data source in Power BI (Home → Refresh)
- The dashboard will automatically update all visuals

---

## File Structure
```
Business_Intelligence_Dashboards/
├── README.md
├── Sales_Data.xlsx
└── Dashboard_001.pbix (Power BI file)
```

---

## Notes
- Ensure data is formatted consistently (dates in MM/DD/YYYY format, numbers without special characters)
- The Revenue column should be pre-calculated in the source data
- All currency values are displayed in USD (customize as needed)

---

## Author
Created: January 28, 2026  
Version: 1.0

For questions or updates, refer to the project documentation or contact the dashboard administrator.
