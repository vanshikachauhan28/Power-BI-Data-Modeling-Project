# Project Notes

## 1. Project Background

This project was created as a hands-on learning exercise in Power BI data modeling.

The starting point was a complex dataset containing 23 interconnected and unorganized tables. The objective was to investigate the data, understand the underlying business processes, clean and transform the tables, and build a structured analytical data model.

The project was implemented by following the methodology demonstrated in the tutorial:

**Power BI Data Modeling Portfolio Project End-to-End (Nightmare Data Model)**
by Baraa Khatib Salkini.

The tutorial was used as a learning reference, while the project was implemented in Power BI to practice the concepts and workflow.

---

# 2. Objective

The main objective was to understand how a messy relational dataset can be transformed into a clean and reliable analytical model.

The project focused on:

- Understanding the business domain
- Investigating raw tables
- Identifying Facts and Dimensions
- Cleaning and transforming data
- Combining related tables
- Defining appropriate table grain
- Creating dimension and fact tables
- Building relationships
- Creating a Star/Galaxy Schema
- Creating a Date dimension
- Developing DAX measures
- Validating the model
- Implementing Row-Level Security

---

# 3. Phase 1 — Preparation & Investigation

The first stage focused on understanding the dataset before making any transformations.

### Key activities

- Reviewed all available tables
- Examined columns and data types
- Investigated how tables were related
- Identified duplicate and redundant information
- Studied the underlying business processes
- Distinguished between transactional and descriptive data
- Classified tables as potential Facts or Dimensions
- Organized the tables within Power Query

### Important learning

A major takeaway from this phase was that data modeling should begin with understanding the **business process and data**, rather than immediately creating relationships or dashboards.

---

# 4. Phase 2 — Building Dimension Tables

The next stage focused on creating clean and reusable dimension tables.

Related source tables were combined where appropriate to create a single source of descriptive information.

### Dimension tables created

- `dim_customer`
- `dim_product`
- `dim_geo`
- `dim_date`
- `dim_campaign`
- `dim_order_flag`

### Dim Customer

The customer dimension consolidates customer-related information such as:

- Customer ID
- Customer name
- Contact information
- City
- Account manager
- Credit limit
- Payment terms

The goal was to create one central source for customer attributes rather than keeping customer information spread across multiple tables.

### Dim Product

The product dimension contains attributes such as:

- Product key
- Product code
- Product name
- Brand
- Category
- Subcategory
- Supplier
- Price

This allows product-related analysis to be performed consistently across multiple fact tables.

### Dim Geography

Geographic information was separated into its own dimension to provide reusable geographic attributes such as:

- City
- Region
- Geographic key

### Dim Campaign

Campaign-related descriptive information was consolidated into a dedicated campaign dimension.

Attributes include:

- Campaign key
- Campaign name
- Channel
- Start date
- End date
- Budget

### Dim Order Flag

The order flag table functions as a small filtering/junk dimension containing attributes related to order classification.

---

# 5. Phase 3 — Building Fact Tables

The third phase focused on identifying business events and measurable transactions.

The major fact tables created were:

- `fact_sales`
- `fact_inventory`
- `fact_order_process`
- `fact_sales_target`
- `fact_campaign_spend`
- `fact_promotion_coverage`

---

## Fact Sales

The Sales fact table represents sales transactions.

Important fields include:

- Customer ID
- Product key
- Order date
- Line ID
- Quantity-related information
- Discount percentage
- Cost
- Line total
- Flag key

The `line_total` measure was particularly important during the transformation process because it could be used as a reference point to validate that the numbers remained consistent.

---

## Fact Inventory

The Inventory fact table stores inventory-related measurements such as:

- Month
- Product key
- Units

This allows inventory analysis by product and time.

---

## Fact Order Process

This fact table captures the order processing lifecycle.

Relevant dates include:

- Order date
- Invoice date
- Delivery date
- Payment date

It also contains the customer and order identifiers required to analyze the order process.

---

## Fact Sales Target

The Sales Target fact table contains target revenue information by period.

Key fields include:

- Period
- Target revenue

This can be connected with the Date dimension for target-vs-actual analysis.

---

## Fact Campaign Spend

The Campaign Spend fact table contains measurable campaign performance information such as:

- Campaign key
- Date
- Spend
- Impressions
- Clicks

This allows campaign-level performance and spending analysis.

---

## Fact Promotion Coverage

The Promotion Coverage fact table connects products with campaigns and represents promotional coverage.

Key fields include:

- Campaign key
- Product key

---

# 6. Understanding Table Grain

One of the important concepts reinforced through this project was **grain**.

The grain defines what one row in a fact table represents.

For example:

### Fact Sales

One row represents a sales line/item transaction.

### Fact Inventory

One row represents an inventory observation for a particular product and month.

### Fact Campaign Spend

One row represents campaign performance/spending information for a particular campaign and date.

Defining the grain before building relationships helps prevent incorrect aggregations and duplicate calculations.

---

# 7. Data Modeling

After constructing the Fact and Dimension tables, relationships were established between them.

The final model follows a **Star/Galaxy Schema** structure.

### Modeling principles applied

- Dimensions sit around fact tables
- Fact tables contain measurable business events
- Dimensions provide descriptive context
- One-to-many relationships are used where appropriate
- Shared dimensions can connect multiple fact tables
- Surrogate keys are used where appropriate
- Fact tables are kept separate when they represent different business processes

The resulting structure allows multiple business processes to be analyzed using common dimensions.

---

# 8. Date Dimension

A dedicated Date dimension was created instead of relying directly on date columns within individual fact tables.

The Date dimension contains attributes such as:

- Date
- Month
- Year

This provides a consistent basis for time-based analysis across different fact tables.

---

# 9. Measures

A dedicated measures table was created to keep DAX calculations organized.

Examples of measures include:

- Total Orders
- Total Customers
- Total Active Customers
- Average Order-to-Pay Time

Keeping measures separate from the underlying tables makes the model easier to navigate and maintain.

---

# 10. Data Validation

Data validation was an important part of the modeling process.

Rather than assuming that transformations were correct, key business metrics were checked throughout the process.

The `line_total` from the sales data was used as an important validation metric.

The objective was to ensure that:

**Raw Data → Transformation → Final Model**

did not result in unintended changes to important business numbers.

This reinforced the importance of validating a data model after major transformations.

---

# 11. Row-Level Security

Row-Level Security (RLS) was implemented to demonstrate how access to the model can be restricted based on user attributes.

The security structure uses regional information to control which data different users can access.

This introduced an additional real-world consideration beyond simply creating relationships and measures.

---

# 12. Naming Conventions

Consistent naming conventions were used throughout the model.

Examples include:

### Dimensions

`dim_customer`

`dim_product`

`dim_geo`

`dim_date`

### Facts

`fact_sales`

`fact_inventory`

`fact_order_process`

### Keys

Fields such as:

`customer_id`

`product_key`

`campaign_key`

Using consistent names makes the model easier to understand and maintain.

---

# 13. Final Data Model

The final model consists of multiple fact and dimension tables connected through shared keys.

### Dimensions

- Customer
- Product
- Geography
- Date
- Campaign
- Order Flag

### Facts

- Sales
- Inventory
- Order Process
- Sales Target
- Campaign Spend
- Promotion Coverage

This creates a structured analytical layer that can support reporting across different business processes.

---

# 14. Key Learnings

### 1. Data modeling comes before visualization

A Power BI report is only as reliable as the model underneath it.

### 2. Understand the business process first

Before deciding whether a table is a Fact or Dimension, it is important to understand what the data represents.

### 3. Define grain carefully

Knowing what one row represents is essential for building correct fact tables and avoiding incorrect aggregations.

### 4. Dimensions should be reusable

A well-designed dimension can provide context to multiple fact tables.

### 5. Validate important numbers

Transformations should be checked against known business metrics to make sure the data has not been unintentionally altered.

### 6. Naming conventions matter

Consistent naming makes complex models easier to navigate and maintain.

### 7. Security is part of data modeling

A production-ready model may also need to consider who should be able to access different portions of the data.

---

# 15. Skills Practiced

Through this project, I practiced:

- Power BI
- Power Query
- DAX
- Data Cleaning
- Data Transformation
- Data Modeling
- Star Schema
- Galaxy Schema
- Fact and Dimension Modeling
- Relationship Management
- Surrogate Keys
- Date Dimensions
- Data Validation
- Row-Level Security
- Analytical Data Modeling

---

# 16. Final Takeaway

The biggest lesson from this project was that building a Power BI solution is not just about creating charts and dashboards.

The more important foundation is:

**Understand the data → Define the grain → Build dimensions → Build facts → Create relationships → Validate → Add measures → Secure the model**

A clean data model makes downstream reporting and analysis more reliable, easier to maintain, and easier to scale.
**Understand the data → Define the grain → Build dimensions → Build facts → Create relationships → Validate → Add measures → Secure the model**

A clean data model makes downstream reporting and analysis more reliable, easier to maintain, and easier to scale.
