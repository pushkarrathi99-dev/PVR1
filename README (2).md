# <img src="https://cdn-icons-png.flaticon.com/512/353/353288.png" width="5%" height="5%"> Wholesale Store: Orders Data ETL

<div align="center"> <img src="https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Assets/Wholesale%20Store%20Orders%20Data%20ETL%20Project%20Thumbnail%2BIcon.png" width="100%" height="100%"> </div>

This repository serves as my documentation for the WholesaleStore: Order Data Transformation - Alteryx Project.

The entire project has been implemented using Alteryx Designer 2024.1 (User) (with AMP Engine enabled).

The project raw data source and data output files have not been uploaded to this repository due to size restrictions, but they can be accessed thorugh the Project Workflow Package that has been uploaded.

---

## Contents:
Please find the sectional links for the project below:
- [Project Objective](#project-objective)
- [Tools used & Methodologies implemented](#tools-used)
- [About the Dataset](#about-the-dataset)
  - [Data Sources](#data-sources)
  - [Data Dictionary](#data-dictionary)
  - [Data Integrity](#data-integrity)
- [Project Implementation](#project-implementation)
- [Workflow Layout](#workflow-layout)
- [Data Outputs](#data-outputs)

---

## Project Objective:
You’re working as an analyst for a wholesale organization i.e a company selling goods to retailers and maintain their order data and customer data in data warehouse. You need to process order data from a Point of Sale (POS) system, as well as an export from the Order Returns department, and update the Orders and Customers table in the data warehouse. Each order placed in the POS system captures the customer details, the product details, price and quantity. Every month this data needs to be moved to a data warehouse where it is stored for long-term use and is used for reporting purposes.

### Assignment:
1. Update the Existing Data Warehouse Orders table with the latest POS orders, placed in August 2021.
We need to create a workflow to take the data from the POS system for August 2021 and move it into the existing order table in the data warehouse. Since data for the previous periods already exists in this destination, we need to add these new records to the existing data.
2. Update the POS and Existing Data Warehouse Orders table with the returns information i.e set the RETURNED column to the right value.
    - Note that a return received in August may be related to an order placed before August, and so sometimes we need to update an existing record in the data warehouse, and other times we need to update the new data from the POS system.
3. Update the Data Warehouse Customers table with the latest customer information from the POS input i.e a customer may have changed their details, like address (anything that is not the customer ID) during their latest order. We want the Data Warehouse to be updated with the most recent customer details. If a customer placed an order in August, we want to override the existing customer details with the details used during their most recent order.
    - Note that the POS system has the US State name in full. Ensure you change that to the State code prior to loading it into the Data Warehouse Customers table.

Note that we refer to data warehouse tables as orders and customer tables in this project, which would typically be database tables. But since we may not have access to a database for this project, we'll use Excel and CSV files instead.

## Tools used:
1. Alteryx Designer- for ETL (Data Import, Data Cleaning, Data Transformation and Data Export) process
2. GitHub - for documentation

## Skills & Methodologies implemented:
1. Data Import - **Input Data Tool & Text Imput Tool**
2. Data Validation - **Select Tool, Browse Tool**
3. Data Transformation - **Filter Tool, Join Tool, Find Replace Tool, Unique Tool, Formula Tool & Union Tool**
4. Data Export - **Output Data Tool**
5. Documentation - **Comment Tool, Tool Container Tool**

---

## About the Dataset:

### Data Sources:
1. Data Warehouse - ORDERS: (File: Orders Table.xlsx) This is the existing ORDERS table in the data warehouse. It contains all orders placed prior to August 2021.
2. Data Warehouse - CUSTOMERS: (File: CUSTOMERS.xlsx) This is the existing CUSTOMERS table in the data warehouse. It contains details for each customer.
3. POS Orders Data: (File: STORE_TRANSACTIONS_ALL_AUG_2021.csv) This is the Point of Sale (POS) data from August 2021
4. Returns: (File: Completed Returns - August 2021.xlsx) These are returns received in August 2021 (Order could be placed prior or during August 2021)
5. US State Codes Reference List: (File: Text Input) This static lookup list maps US state names to US State codes.

[Link to Data Sources](https://github.com/5ifar/WholesaleStore_Order_Data_Transformation/blob/main/Data%20%26%20Workflow%20Files/Links.md)

### Data Dictionary:
**1. Orders Table.xlsx: 482793 records | 10 fields**

|Column name|Data type|Description|
|-|-|-|
|ORDER_ID|V_String|Unique Order Id number|
|PRODUCT_SKU|V_String|Unique Product SKU (Stock Keeping Unit) number|
|QUANTITY|Double|Quantity of product ordered|
|ORDER_DATE|DateTime|Date the order was placed|
|CUSTOMER_ID|Double|Unique Customer Id number|
|RETURNED|Bool|Order Return Status|
|PRODUCT_NAME|V_String|Name of product|
|PRODUCT_DESC|V_String|Description of product|
|PRODUCT_PRICE|Double|Price of product|
|PRODUCT_CATEGORY|V_String|Category of product|

**2. CUSTOMERS.xlsx: 985857 records | 10 fields**

|Column name|Data type|Description|
|-|-|-|
|ID|Double|Unique Customer Id number|
|FirstName|V_String|First Name of customer|
|LastName|V_String|Last Name of customer|
|UserName|V_String|User Name of customer|
|Email|V_String|Email of customer|
|State|V_String|State of customer|
|City|V_String|City of customer|
|Street|V_String|Street of customer|
|PostCode|V_String|Postal Code of customer|
|Phone|V_String|Mobile number of customer|

**3. STORE_TRANSACTIONS_ALL_AUG_2021.csv: 67792 records | 18 fields**

|Column name|Data type|Description|
|-|-|-|
|ORDER_ID|V_String|Unique Order Id number|
|PRODUCT_SKU|V_String|Unique Product SKU (Stock Keeping Unit) number|
|QUANTITY|V_String|Quantity of product ordered|
|ORDER_DATE|V_String|Date the order was placed|
|CUSTOMER_ID|V_String|Unique Customer Id number|
|PRODUCT_NAME|V_String|Name of product|
|PRODUCT_DESC|V_String|Description of product|
|PRODUCT_PRICE|V_String|Price of product|
|PRODUCT_CATEGORY|V_String|Category of product|
|FirstName|V_String|First Name of customer|
|LastName|V_String|Last Name of customer|
|UserName|V_String|User Name of customer|
|Email|V_String|Email of customer|
|State|V_String|State of customer|
|City|V_String|City of customer|
|Street|V_String|Street of customer|
|PostCode|V_String|Postal Code of customer|
|Phone|V_String|Mobile number of customer|

**4. Completed Returns - August 2021.xlsx: 718 records | 2 fields**

|Column name|Data type|Description|
|-|-|-|
|ORDER_ID|V_String|Unique Order ID number|
|RETURNED|Bool|Order Return Status|

**5. US State Codes Text Input: 55 records | 2 fields**

|Column name|Data type|Description|
|-|-|-|
|State*|V_String|Name of State|
|State_Abbreviated|V_String|Abbreviation Code of State|

## Data Integrity:
ROCCC Evaluation:
- Reliability: MED - The raw dataset is created and updated by Hendrik Kleine (Udemy Instructor). It has total 4 files. All of them were utilized in the analysis.
- Originality: HIGH - First party provider (Hendrik Kleine, Udemy)
- Comprehensiveness: HIGH - Total 4 Files with a total of around 1.5 Million records were provided. Dataset contains multiple dimension parameters for Customers as well as comprehensive Order transaction data.
- Current: LOW - Dataset contains 2021 data i.e almost 3 years old. So its not very relevant. Any trends observed and insights gained need to be comprehended as a general (not yearly) trend.
- Citation: LOW - No official citation/reference available.

---

## Project Implementation:
Please find the documentation links for the project step-wise implementation below:
- [1. Configuring the Inputs](https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Project%20Implementation/Documentation.md#1-configuring-the-inputs)
- [2. Preview the loaded Input data](https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Project%20Implementation/Documentation.md#2-preview-the-loaded-input-data)
- [3. Data Validation](https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Project%20Implementation/Documentation.md#3-data-validation)
- [4. Data Transformation for Task 1 & 2](https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Project%20Implementation/Documentation.md#4-data-transformation-for-task-1--2)
- [5. Data Export for Task 1 & 2](https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Project%20Implementation/Documentation.md#5-data-export-for-task-1--2)
- [6. Data Transformation for Task 3](https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Project%20Implementation/Documentation.md#6-data-transformation-for-task-3)
- [7. Data Export for Task 3](https://github.com/5ifar/WholesaleStore_Orders_Data_ETL/blob/main/Project%20Implementation/Documentation.md#7-data-export-for-task-3)

---

## Workflow Layout:

<div align="center"> <img src="https://github.com/5ifar/WholesaleStore_Order_Data_Transformation/blob/main/Assets/Wholesale%20Store%20Order%20Data%20Transformation%20Project%20Workflow.png" width="100%" height="100%"> </div>

---

## Data Outputs:
[Link to Data Outputs](https://github.com/5ifar/WholesaleStore_Order_Data_Transformation/blob/main/Data%20%26%20Workflow%20Files/Links.md)

---
