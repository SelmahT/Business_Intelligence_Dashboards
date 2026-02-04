# AfriRetail Power Query Data Preparation
---

## Project Overview
AfriRetail Ltd needed clean, analysis-ready data for sales reporting across East Africa. Raw sales, product, and region data were messy and inconsistent.

---

## Data Preparation Workflow

### 1. Data Ingestion & Staging
- Loaded 3 datasets into Power BI.
### **Query Organization**

| Query Name | Type | Purpose | Table Type |
|------------|------|---------|------------|
| `Fact_Sales_Staging` | Staging | Raw sales transactions before cleaning | Fact Table |
| `Dim_Products_Staging` | Staging | Product reference data before cleaning | Lookup/Dimension Table |
| `Dim_Regions_Staging` | Staging | Country-region mapping before cleaning | Lookup/Dimension Table |
---

![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task1/01_Data_Ingestion_Staging_Queries.PNG](powerquery_screenshots/Task1/01_Data_Ingestion_Staging_Queries.PNG)

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
![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_Data_Profiling_View1.PNG](powerquery_screenshots/Task2/02_Data_Profiling_View1.PNG)
---
![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_Data_Profiling_View2.PNG](powerquery_screenshots/Task2/02_Data_Profiling_View2.PNG)
---
![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_Data_Profiling_View3.PNG](powerquery_screenshots/Task2/02_Data_Profiling_View3.PNG)
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

DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_FlagColumn_Creation.PNG

---

DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_FlagColumn_Results.PNG

---

**Individual Flag Columns:**
- **Quantity Flag:** `Flag_InvalidQuantity`
  - **Logic:** `IF Quantity ≤ 0 THEN "Invalid" ELSE "Valid"`
  - **Purpose:** Specific identification of quantity issues

---

![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_FlagColumn_Quantity.PNG](powerquery_screenshots/Task2/02_FlagColumn_Quantity.PNG)

---

![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_FlagQuantity_Results.PNG](powerquery_screenshots/Task2/02_FlagQuantity_Results.PNG)

---

**Audit Query Created:**
- **Name:** `Audit_ProblematicRecords`
- **Source:** Reference of `Fact_Sales_Staging`
- **Filter:** `DataQualityFlag = "Review Required"`
- **Count:** [3941] problematic records isolated

---

![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_AuditQuery_Creation.PNG](powerquery_screenshots/Task2/02_AuditQuery_Creation.PNG)

---

![DSA3020_PowerQuery_Lab/powerquery_screenshots/Task2/02_AuditQuery_Results.PNG](powerquery_screenshots/Task2/02_AuditQuery_Results.PNG)

---

## **DATA CLEANING & STANDARDIZATION**

### ** Column Removal & Rationalization**
**Removed Columns:**
- `ENTRYMETHOD`: Removed due to 235 missing values (23.5%) and low business relevance for sales analysis.

- Individual flag columns: Consolidated into main `DataQualityFlag` column to reduce redundancy.
---


**Column Retention Justification:**

- All remaining columns directly support sales performance analysis, financial reconciliation, and management reporting requirements.

---

![alt text](powerquery_screenshots/Task3/03_Remove_EntryMethod.PNG)


---

### **Text Field Standardization**
Applied consistent formatting to all text columns:
---

#### **BRANCH Column Cleaning**

***Issues:*** Leading/trailing spaces, mixed casing (" Kigali " vs "Nairobi CBD")

***Actions:*** Trim → Clean → Capitalize Each Word

---

![alt text](powerquery_screenshots/Task3/03_Clean_Branch.PNG)

---

![alt text](powerquery_screenshots/Task3/03_Clean_Branch_Result.PNG)

---

#### **COUNTRY Column Cleaning**

- ***Issues:*** Lowercase entries ("kenya"), abbreviations ("Tz", "Ug")

- ***Actions:*** Trim → Clean → Capitalize → Value standardization

- ***Replacements:*** "Tz"→"Tanzania", "Keny"→"Kenya", "Ug"→"Uganda", "Rw"→"Rwanda"

---

![alt text](powerquery_screenshots/Task3/03_Clean_Country.PNG)

---

![alt text](powerquery_screenshots/Task3/03_Clean_Country_Result.PNG)


---

#### **CATEGORY Column Cleaning**

- ***Issues:*** Inconsistent naming, trailing spaces ("peripherals ")

- ***Actions:*** Trim → Clean → Capitalize → "Peripherals"→"Accessories"

---
![alt text](powerquery_screenshots/Task3/03_Clean_Category.PNG)
---
![alt text](powerquery_screenshots/Task3/03_Clean_Category_Results.PNG)
*Figure: Standardizing product CATEGORY names*

---

#### **PAYMENTMETHOD Column Cleaning**

-***Issues:*** Leading spaces (" Card"), case inconsistencies

-***Actions:*** Trim → Clean → Capitalize → Standardize "MPESA"

---

#### **SALESREP Column Cleaning**

- ***Issues:*** Lowercase entries ("bob" vs "edward")

- ***Actions:*** Trim → Clean → Capitalize Each Word

---
![alt text](powerquery_screenshots/Task3/03_Clean_Payment&Salesp.PNG)

---

![alt text](powerquery_screenshots/Task3/03_Clean_Payment&Salesp_Result.PNG)

---

### **Data Type Conversion**

- Ensured all columns have appropriate data types:

#### **SALESAMOUNT Type Correction**

-***Issue:*** Text values including "error" entries

-***Actions:*** Replace "error"→null → Convert to Decimal Number

---

![alt text](powerquery_screenshots/Task3/03_SalesAmt_dtype.PNG)

---

![alt text](powerquery_screenshots/Task3/03_SalesAmt_newdtype.PNG)


---



### **Missing Value Handling**

#### **UNIT PRICE (192 missing values - 19.2%):**

-***Action:*** Replaced nulls with column average: 1387.17

-***Justification:*** Statistical imputation preserves data volume

---

![alt text](powerquery_screenshots/Task3/03_Replace_UnitPrice_Nulls.PNG)


---

#### **SALESAMOUNT (264 missing values - 26.4%):**

-***Action:*** Calculated missing values: Quantity × Unit Price

-***Justification:*** Mathematically accurate reconstruction

---

![alt text](powerquery_screenshots/Task3/03_New_Salesamt.PNG)

---

#### **TRANSACTIONDATE (202 missing values - 20.2%):**

- ***Action:*** Replaced nulls with most frequent date: 2024-03-20

- ***Justification:*** Maintains temporal consistency

---

![alt text](powerquery_screenshots/Task3/03_Fill_Dates.PNG)

---

### **Data Entry Error Correction**

#### **QUANTITY Column Issues:**

-***Problems:*** Negative values (minimum: -3), 68 zero values

-***Solution:*** Created cleaned column with logic: if ≤0 then 1 else original value

---

![alt text](powerquery_screenshots/Task3/03_Replace_Quantities.PNG)


---

### **Column Cleanup & Finalization**

#### **Temporary Column Removal**
**Actions:** Removed intermediate calculation columns, kept final cleaned versions


#### **Column Renaming**
**Actions:** Renamed cleaned columns to final names (Quantity_Cleaned→Quantity, etc.)

---