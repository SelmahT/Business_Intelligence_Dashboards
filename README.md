# Dashboard 001
---
## 📊Sales Performance Dashboard | Power BI
---

### Project Overview
This Power BI dashboard provides insights into sales performance across regions, countries, products, and salespersons.  
It allows users to track revenue trends, top products, and units sold using interactive visuals and slicers.  
The dashboard emphasizes professional design with clear hierarchy, consistent colors, and readable typography.

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

| # | Visual | Type | Notes |
|---|--------|------|-------|
| 1 | Total Revenue | Card | Sum of Revenue |<img width="141" height="92" alt="image" src="https://github.com/user-attachments/assets/08c14e43-39df-42d6-9ec2-d9ff7c299726" />
| 2 | Total Units Sold | Card | Sum of Units Sold |<img width="144" height="89" alt="image" src="https://github.com/user-attachments/assets/8f735e41-d0af-4c57-b9b8-6cc4ef77f0e4" />

| 3 | Average Unit Price | Card | Average of Unit Price |
| 4 | Revenue by Region | Clustered Column Chart | Interactive by slicers |
| 5 | Revenue by Country | Bar Chart | Sorted descending |
| 6 | Revenue by Product Category | Donut Chart | Shows share by category |
| 7 | Top Products by Revenue | Bar Chart | Top 5 filter applied |
| 8 | Sales Trend Over Time | Line Chart | Month hierarchy |
| 9 | Units Sold by Salesperson | Stacked Column Chart | Sorted descending |
| 10 | Detailed Sales Table | Table | Full data view |


