# Power-BI-Data-Modeling-Project
End-to-end Power BI data modeling project focused on transforming messy relational data into a clean, scalable Star/Galaxy Schema for reliable business analysis.

## Project Overview

This project is a hands-on Power BI data modeling implementation focused on transforming a complex dataset of **23 messy and interconnected tables** into a clean, structured, and analysis-ready **Star/Galaxy Schema**.

The project covers the complete data modeling workflow — from investigating raw data and identifying business processes to transforming tables, building Fact and Dimension tables, creating relationships, developing DAX measures, validating the model, and implementing Row-Level Security.

The project was developed as a **learning implementation based on a Power BI data modeling tutorial by Baraa Khatib Salkini**, with the concepts and workflow practically implemented in Power BI.

---

## Project Objective

The primary objective of this project was to understand how a complex relational dataset can be transformed into a reliable analytical data model.

The project focuses on:

- Understanding the underlying business processes
- Investigating and organizing raw tables
- Identifying Fact and Dimension tables
- Cleaning and transforming data using Power Query
- Combining related source tables
- Defining the appropriate grain of Fact tables
- Creating a Star/Galaxy Schema
- Establishing one-to-many relationships
- Creating a dedicated Date dimension
- Developing DAX measures
- Validating data throughout the transformation process
- Implementing Row-Level Security (RLS)

---

## Tools & Technologies

- **Power BI**
- **Power Query**
- **DAX**
- Data Modeling
- Star Schema
- Galaxy Schema
- Data Transformation
- Row-Level Security (RLS)

---

# Project Workflow

## Phase 1 — Data Preparation & Investigation

The project started with a dataset containing 23 interconnected tables with information spread across different business processes.

The first stage focused on understanding the data before building the model.

### Key activities

- Examined available tables and columns
- Reviewed data types and existing relationships
- Investigated the underlying business processes
- Identified redundant and related information
- Distinguished transactional data from descriptive data
- Classified tables as potential Facts or Dimensions
- Organized the source tables logically in Power Query

### Key Learning

Before building relationships, it is important to understand **what the data represents and how the business process works**.

---

# Phase 2 — Building Dimension Tables

Related source tables were cleaned and consolidated into reusable Dimension tables.

The final model contains the following major dimensions:

### `dim_customer`

Contains customer-related attributes such as:

- Customer ID
- Customer name
- Contact information
- City
- Account manager
- Credit limit
- Payment terms

### `dim_product`

Contains product-related information including:

- Product key
- Product code
- Product name
- Brand
- Category
- Subcategory
- Supplier
- Price

### `dim_geo`

Contains geographic information such as:

- Geographic key
- City
- Region

### `dim_date`

A dedicated Date dimension containing:

- Date
- Month
- Year

This dimension provides a consistent basis for time-based analysis across different Fact tables.

### `dim_campaign`

Contains campaign-related information including:

- Campaign key
- Campaign name
- Channel
- Start date
- End date
- Budget

### `dim_order_flag`

A small filtering/junk dimension containing order classification information.

---

# Phase 3 — Building Fact Tables

The next stage focused on structuring measurable business events into Fact tables.

The final model contains:

- `fact_sales`
- `fact_inventory`
- `fact_order_process`
- `fact_sales_target`
- `fact_campaign_spend`
- `fact_promotion_coverage`

---

## `fact_sales`

Contains sales transaction information including:

- Customer ID
- Product key
- Order date
- Line ID
- Discount percentage
- Cost
- Line total
- Flag key

The **line total** was also used as an important validation metric throughout the transformation process.

---

## `fact_inventory`

Contains inventory information by product and month.

Key fields include:

- Month
- Product key
- Units

---

## `fact_order_process`

Captures different stages of the order processing cycle.

Important fields include:

- Order ID
- Customer ID
- Order date
- Invoice date
- Delivery date
- Payment date
- Order-to-pay duration

---

## `fact_sales_target`

Contains sales targets by period.

Key fields include:

- Period
- Target revenue

---

## `fact_campaign_spend`

Contains measurable campaign performance information such as:

- Campaign key
- Date
- Spend
- Impressions
- Clicks

---

## `fact_promotion_coverage`

Connects products with campaigns to represent promotional coverage.

Key fields include:

- Campaign key
- Product key

---

# Understanding Fact Table Grain

One of the key concepts practiced in this project was defining the **grain** of each Fact table.
Grain describes what exactly one row represents.

For example:

| Fact Table | Grain |
|---|---|
| Fact Sales | Individual sales line/item |
| Fact Inventory | Product-level inventory observation by month |
| Fact Campaign Spend | Campaign performance/spending observation by date |
| Fact Promotion Coverage | Product-campaign relationship |

Clearly defining grain helps prevent duplicate records, incorrect aggregations, and unreliable measures.

---

# Data Modeling

The final model follows a **Star/Galaxy Schema** approach.
Instead of connecting tables randomly, Fact tables are connected to appropriate shared Dimensions.

### Modeling principles applied

- Fact tables contain measurable business events
- Dimension tables provide descriptive context
- Shared Dimensions are reused across multiple Fact tables
- One-to-many relationships are used where appropriate
- Surrogate keys are used for relationships
- Transactional and descriptive data are separated
- Consistent naming conventions are maintained

This creates a structured analytical layer that can support multiple business processes.

---

# Date Dimension

A dedicated Date table was created instead of relying exclusively on date fields within individual Fact tables.

The Date dimension contains:

- Date
- Month
- Year

This enables consistent time-based analysis across Sales, Order Processing, Campaigns, and other business processes.

---

# DAX Measures

A dedicated `_measures` table was created to organize DAX calculations.

Some of the measures include:

- Total Orders
- Total Customers
- Total Active Customers
- Average Order-to-Pay Time

Keeping measures in a separate table makes the model easier to navigate and maintain.

---

# Data Validation

Data validation was an important part of the modeling process.
Rather than assuming that transformations were correct, key business numbers were checked throughout the process.
The **Line Total** from the Sales data was used as a core reference metric to ensure that transformations and merges did not unintentionally change the underlying numbers.

The validation process followed the principle:

**Raw Data → Transformation → Final Model → Validate**

This reinforced the importance of protecting the integrity of the original business data while transforming it.

---

# Row-Level Security

Row-Level Security (RLS) was implemented to demonstrate how access to the data model can be restricted based on user attributes.

The model uses **regional information** to demonstrate how different users can be provided access to relevant portions of the dataset.

This adds a practical security layer to the analytical model.

---

# Final Data Model

The final model contains the following major components:

### Dimensions

| Dimension | Purpose |
|---|---|
| `dim_customer` | Customer attributes |
| `dim_product` | Product and category information |
| `dim_geo` | Geographic information |
| `dim_date` | Time-based analysis |
| `dim_campaign` | Campaign attributes |
| `dim_order_flag` | Order classification/filtering |

### Facts

| Fact | Purpose |
|---|---|
| `fact_sales` | Sales transactions |
| `fact_inventory` | Inventory information |
| `fact_order_process` | Order processing lifecycle |
| `fact_sales_target` | Sales targets |
| `fact_campaign_spend` | Campaign performance and spending |
| `fact_promotion_coverage` | Product promotion coverage |

---

## 📚 Project Credit

This project was created as a hands-on learning implementation based on:

**Power BI Data Modeling Portfolio Project End-to-End (Nightmare Data Model)**  
by **Baraa Khatib Salkini**

The tutorial was used as a learning reference to understand and practice Power BI data modeling concepts including data transformation, Fact and Dimension modeling, Star/Galaxy Schema design, relationships, validation, DAX measures, Date dimensions, and Row-Level Security.
