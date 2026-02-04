# AfriRetail Power Query Data Preparation
---

## Project Overview
AfriRetail Ltd needed clean, analysis-ready data for sales reporting across East Africa. Raw sales, product, and region data were messy and inconsistent.

---

## Data Preparation Workflow

### 1. Data Ingestion & Staging
- Loaded 3 datasets into Power BI.
- Created staging queries:
  - `Fact_Sales_Staging` (fact table)
  - `Dim_Products_Staging` (lookup)
  - `Dim_Regions_Staging` (lookup)
---

- Screenshot:

![alt text](powerquery_screenshots/01_Data_Ingestion_Staging_Queries.PNG)

---

### 2. Data Profiling & Quality Assessment

After loading the sales data into Power Query, we used built-in profiling tools to identify data quality issues.

#### Steps Performed

1. **Enable Column Profiling**
   - Clicked **View** → Checked:
     - **Column Quality**
     - **Column Distribution**
     - **Column Profile**
   - **Purpose:** To visually inspect which columns contain nulls, errors, or inconsistent data.

---
![alt text](powerquery_screenshots/02_Data_Profiling_View1.PNG)
---
![alt text](powerquery_screenshots/02_Data_Profiling_View2.PNG)
---
![alt text](powerquery_screenshots/02_Data_Profiling_View3.PNG)
---

## Data Quality Issues Identified in Sales Data

- **Missing and inconsistent transaction dates**
  - `TransactionDate` has 202 empty records
  - Multiple date formats detected (e.g. `03-20-2024`, `2024/04/10`)

- **Inconsistent text formatting**
  - Leading/trailing spaces and mixed casing found in:
    - `Country`
    - `Branch`
    - `Category`
    - `PaymentMethod`
    - `SalesRep`
  - Examples: ` kenya` vs `Uganda`, `Manual` vs `manual`

- **Invalid quantity values**
  - `Quantity` contains zero and negative values
  - Minimum value = `-3`
  - Zero-value records = `68`

- **Missing and erroneous numeric values**
  - `Unit Price` has `192` missing values
  - `SalesAmount` has `264` missing values and error entries

---

### **Data Quality Flag Implementation**
**Main Flag Column:**
- **Name:** `DataQualityFlag`
- **Logic:** `IF (TransactionDate = null OR Quantity ≤ 0 OR UnitPrice = null OR SalesAmount = null) THEN "Review Required" ELSE "Clean"`
- **Results:** [2259] Clean records, [3941] Review Required records

---

![alt text](powerquery_screenshots/02_FlagColumn_Creation.PNG)

---

![alt text](powerquery_screenshots/02_FlagColumn_Results.PNG)

---

**Individual Flag Columns:**
- **Quantity Flag:** `Flag_InvalidQuantity`
  - **Logic:** `IF Quantity ≤ 0 THEN "Invalid" ELSE "Valid"`
  - **Purpose:** Specific identification of quantity issues

---

![alt text](powerquery_screenshots/02_FlagColumn_Quantity.PNG)

---

![alt text](powerquery_screenshots/02_FlagQuantity_Results.PNG)

---

**Audit Query Created:**
- **Name:** `Audit_ProblematicRecords`
- **Source:** Reference of `Fact_Sales_Staging`
- **Filter:** `DataQualityFlag = "Review Required"`
- **Count:** [3941] problematic records isolated

---

![alt text](powerquery_screenshots/02_AuditQuery_Creation.PNG)

---

![alt text](powerquery_screenshots/02_AuditQuery_Results.PNG)

---

