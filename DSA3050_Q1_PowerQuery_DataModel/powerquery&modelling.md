# DSA 3050A – Power BI Project: FactSales Dataset

## Project Overview
This project is part of **DSA 3050A – Power Query + Data Modelling**.  
The objective is to clean, transform, and model a real-world dataset using **Power BI**, and create a star schema for analysis.  

The dataset used is **FactSales**, containing transactional sales data with two related dimension tables: **DimCustomer** and **DimProduct**.  

---

## Dataset Description
- **Fact Table:** `FactSales`
  - InvoiceNo, Quantity, UnitPrice, SalesAmount, InvoiceDate, CustomerID, ProductCode
- **Dimension Tables:**  
  - `DimCustomer`: CustomerID, Country  
  - `DimProduct`: ProductCode, Description  

- **Minimum Requirements Met:**  
  - ≥1,000 rows in the main table  
  - At least 1 numeric measure (`Quantity`, `UnitPrice`, `SalesAmount`)  
  - At least 1 date column (`InvoiceDate`)  
  - Screenshot of dataset source included in submission PDF  

---

## Project Steps

### Section A – Power Query
1. **Data Profiling & Quality Checks**  
   - Column quality, distribution, profile  
   - Identified data issues and applied fixes  

2. **Data Types & Locale Conversion**  
   - Correct types set for:  
     - `InvoiceDate` → Date  
     - `Quantity` → Whole number  
     - `UnitPrice` → Decimal  
   - Locale conversion applied where necessary  

3. **Text Standardization**  
   - Cleaned `Description` column with **Trim + Clean + Proper Case**  
   - Column names were already descriptive; no renaming applied  

4. **Conditional & Custom Columns**  
   - Conditional Column: `QuantityCategory` (Low / Medium / High)  
   - Custom Column: `SalesAmount = Quantity × UnitPrice`  

5. **Grouping**  
   - Grouped by `Country` (or `QuantityCategory`)  
   - Produced 2 aggregations: TotalQuantity, TotalSales  

---

### Section B – Data Modelling
1. **Star Schema Identification**  
   - Fact Table: `FactSales`  
   - Dimension Tables: `DimCustomer`, `DimProduct`  
   - No bridge table needed  

2. **Relationships**  
   - FactSales[CustomerID] → DimCustomer[CustomerID]  
   - FactSales[ProductCode] → DimProduct[ProductCode]  
   - Cardinality: Many-to-One  
   - Cross-filter direction: Single  
   - Active: Yes  

3. **Key Uniqueness**  
   - Verified `CustomerID` and `ProductCode` are unique in dimension tables  

4. **Date Table**  
   - Decision: Yes  
   - Reasons: Enables time intelligence calculations and consistent filtering  
   - Suggested Columns: Date, Year, Month, Quarter, Week Number  

---

### Bonus – Small Data Dictionary

| Table        | Column       | Meaning                              | Type      | Key/Attribute |
|-------------|-------------|--------------------------------------|-----------|---------------|
| FactSales   | InvoiceNo   | Unique invoice number                | Text      | Key           |
| FactSales   | Quantity    | Number of items sold                 | Whole     | Measure       |
| FactSales   | UnitPrice   | Price per item                       | Decimal   | Measure       |
| FactSales   | SalesAmount | Total sales per row (Quantity × UnitPrice) | Decimal | Measure |
| DimCustomer | CustomerID  | Unique customer identifier           | Text      | Key           |
| DimCustomer | Country     | Country of customer                  | Text      | Attribute     |
| DimProduct  | ProductCode | Unique product identifier            | Text      | Key           |
| DimProduct  | Description | Product description                  | Text      | Attribute     |

---

## Screenshots & Evidence
- **Power Query Applied Steps**: Screenshots included in submission PDF  
- **Model View Relationships**: Screenshots included in submission PDF  
- **Dataset Source Proof**: Screenshot included  

---

## How to Use
1. Open **Power BI Desktop**  
2. Load the `Retail_data` dataset  
3. Load dimension tables `DimCustomer` and `DimProduct`  
4. Apply transformations as outlined in the PDF (if not already applied)  
5. Explore the model view and verify relationships  
6. Use visuals to analyze sales by customer, product, and time  

---

## Author
**Selmah Tzindori**  

---

