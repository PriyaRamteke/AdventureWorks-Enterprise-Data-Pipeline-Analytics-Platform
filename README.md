
# 🚀 AdventureWorks Enterprise Data Engineering & Analytics Platform

End-to-end Azure data engineering solution implementing dynamic ingestion, cloud data lake architecture, PySpark transformations, Silver layer processing, and Power BI analytics.

# Overview
The **AdventureWorks Enterprise Data Engineering & Analytics Platform** is a production-style cloud data pipeline built using Microsoft Azure services.

The project demonstrates a complete modern data engineering workflow:

- Extract enterprise datasets
- Store raw data in Azure Data Lake
- Transform data using PySpark
- Create optimized Silver layer datasets
- Prepare analytical datasets
- Generate business insights using Power BI


The solution follows a **Medallion Architecture** approach:
~~~text
Source Data
|
|
Bronze Layer
(Raw Data)
|
|
Silver Layer
(Cleansed & Transformed Data)
|
|
Analytics Layer
(Power BI Reports)
~~~

# Business Problem

Organizations receive large amounts of raw operational data from multiple sources.

Challenges:

- Data arrives in different formats
- Manual processing is difficult
- Data quality issues impact analytics
- Reporting requires clean structured datasets

This project solves these problems by building a scalable automated data platform.

---

# Key Features


## 🔹 Dynamic Data Ingestion

The ingestion pipeline extracts AdventureWorks datasets dynamically.

Supported datasets:

- Customers
- Products
- Product Categories
- Product Subcategories
- Sales
- Returns
- Territories
- Calendar


---

## 🔹 Azure Data Lake Storage Architecture


Data is organized using Bronze and Silver layers.
~~~text
Azure Data Lake Storage Gen2

bronze/

AdventureWorks_Customers
AdventureWorks_Products
AdventureWorks_Sales

silver/

AdventureWorks_Customers
AdventureWorks_Products
AdventureWorks_Sales
~~~
## 🔹 PySpark Transformation Engine

The Silver layer is developed using Spark transformations.


Implemented operations:

- Column creation
- Data type conversion
- String manipulation
- Date extraction
- Data cleansing
- Aggregation
- Parquet conversion


---
# Architecture
https://github.com/PriyaRamteke/AdventureWorks-Enterprise-Data-Pipeline-Analytics-Platform/blob/main/images/Architecture.png
# Data Processing Workflow
https://github.com/PriyaRamteke/AdventureWorks-Enterprise-Data-Pipeline-Analytics-Platform/blob/main/images/Data%20Processing%20Workflow.png

# Technology Stack
| Category       | Technology                   | Purpose                      |
| -------------- | ---------------------------- | ---------------------------- |
| Cloud          | Microsoft Azure              | Cloud platform               |
| Data Pipeline  | Azure Data Factory / Synapse | Data ingestion               |
| Storage        | Azure Data Lake Storage Gen2 | Data lake                    |
| Processing     | Apache Spark                 | Distributed processing       |
| Language       | PySpark                      | Transformations              |
| Notebook       | Databricks Notebook          | Data engineering development |
| Warehouse      | Azure Synapse SQL            | Analytics                    |
| Visualization  | Power BI                     | Dashboard reporting          |
| Storage Format | Parquet                      | Optimized analytics storage  |
| Authentication | Managed Identity             | Secure access                |

# Project Structure
 ~~~text
 AdventureWorks-Enterprise-Data-Pipeline

│
├── datasets
│
│   ├── AdventureWorks_Customers.csv
│   ├── AdventureWorks_Products.csv
│   ├── AdventureWorks_Sales_2015.csv
│   ├── AdventureWorks_Sales_2016.csv
│   ├── AdventureWorks_Sales_2017.csv
│
│
├── Azure Pipeline Objects
│
│   ├── Linked Services
│   ├── Datasets
│   └── Parameters
│
│
├── notebooks
│
│   └── silver_layer.ipynb
│
│
└── PowerBI Dashboard
~~~
# Bronze Layer
The Bronze layer stores raw ingested datasets without major modifications.

Example:
~~~text
bronze/

AdventureWorks_Customers.csv

AdventureWorks_Products.csv

AdventureWorks_Sales.csv
~~~
## Purpose:

Maintain original source data
Enable reprocessing
Preserve historical information
# Silver Layer Processing
The Silver layer notebook performs transformations.

## Authentication

### Azure Data Lake access is configured using:
~~~text
Service Principal
OAuth authentication
Azure storage credentials
~~~
# Data Transformations
## Calendar Transformation
Added:
~~~text
Month

Year
~~~
Example:
~~~text
df_cal.withColumn(
"Month",
month(col("Date"))
)
~~~
Output:
~~~text
silver/AdventureWorks_Calendar
~~~
# Customer Transformation
## Created:
FullName
## Logic:
~~~text
concat_ws(
' ',
Prefix,
FirstName,
LastName
)
~~~
Output:
~~~text
silver/AdventureWorks_Customers
~~~
# Product Transformation
## Performed:
~~~text
SKU cleaning
Product name extraction
~~~
### Example:

Before:
~~~text
BK-M18B-44
~~~
After:
~~~text
BK
~~~
# Sales Transformation
## Applied:

Timestamp Conversion
~~~text
to_timestamp("StockDate")
~~~
## Order Number Standardization
~~~text
regexp_replace(
OrderNumber,
'S',
'T'
)
~~~
## Revenue Calculation
~~~text
OrderLineItem * OrderQuantity
~~~
Created:
~~~text
Multiply
~~~
# Silver Output Format
All transformed datasets are stored as:
~~~text
Apache Parquet
~~~
## Benefits:

Faster queries
Column based storage
Better compression
Analytics optimized
# Database / Data Model
https://github.com/PriyaRamteke/AdventureWorks-Enterprise-Data-Pipeline-Analytics-Platform/blob/main/images/Database%20%20Data%20Model.png
# How To Run
## Requirements

Install:
~~~text
Azure Subscription
Azure Data Factory
Azure Data Lake Gen2
Databricks Workspace
Power BI Desktop
~~~
# Notebook Execution
## Open:
~~~text
silver_layer.ipynb
~~~
## Execute:
~~~text
Configure Azure authentication
Read Bronze datasets
Apply transformations
Write Silver datasets
~~~
# Analytics Dashboard
## Power BI provides insights:

### Examples:
~~~text
Order trends
Customer growth
Product analysis
Quantity distribution
~~~
### Dashboard:
~~~text
Power BI

        |
        |
Silver Data

        |
        |
Azure Data Lake
~~~
# Engineering Practices
## Scalability

### Implemented:
~~~text
Cloud storage architecture
Spark distributed processing
Parameter driven ingestion
Performance Optimization
~~~ 
### Used:
~~~text
Parquet storage
Spark transformations
Data lake partitioning approach
Security
~~~
## Implemented:
~~~text
Managed Identity
OAuth authentication
Azure security model
Challenges & Solutions
~~~
| Challenge             | Solution                |
| --------------------- | ----------------------- |
| Multiple datasets     | Dynamic ingestion       |
| Raw inconsistent data | PySpark transformations |
| Large file processing | Spark engine            |
| Analytics performance | Parquet format          |
| Secure storage access | Azure authentication    |
# Future Enhancements

## Possible improvements:
~~~text
Add Gold analytics layer
Implement Delta Lake
Add data quality framework
Add pipeline monitoring
Add CI/CD deployment
Add incremental loading
Add automated testing
~~~
# Author
## Priya Ramteke

### Azure Data Engineering Portfolio Project
GitHub: https://github.com/PriyaRamteke

LinkedIn: https://www.linkedin.com/in/priyaborkar10/

