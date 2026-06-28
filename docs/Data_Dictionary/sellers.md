Table: sellers
Business Purpose

The sellers table stores information about all sellers registered on the Olist marketplace. It contains each seller's unique identifier and geographic location, including ZIP code prefix, city, and state.

This table enables seller-level analysis, regional performance reporting, logistics optimization, and marketplace performance evaluation. By linking sellers with products and orders, analysts can measure sales performance, delivery efficiency, and customer satisfaction for individual sellers.

Business Process

The business process represented by this table is:

Seller Registers on Marketplace
          │
          ▼
Seller Information Stored
          │
          ▼
Seller Lists Products
          │
          ▼
Customer Purchases Product
          │
          ▼
Seller Fulfills Order

The sellers table stores master data about sellers before any sales transactions occur.

Grain

One row represents one unique seller.

Each record describes a single seller identified by a unique seller_id.

Primary Key

Primary Key

seller_id

Each seller should have a unique identifier.

Foreign Keys

This table does not contain foreign keys.

It is referenced by:

Referenced By	Relationship
order_items.seller_id	Links sellers to products sold in customer orders.
Table Relationships
Sellers
    │
    │ seller_id
    ▼
Order Items
    │
    ▼
Orders
    │
    ▼
Customers

The sellers table enriches transaction data by identifying which seller fulfilled each purchased product.

Column Descriptions
Column	Description
seller_id	Unique identifier for each seller.
seller_zip_code_prefix	ZIP code prefix of the seller's location.
seller_city	City where the seller is located.
seller_state	Brazilian state where the seller operates.
Business Questions Supported

This table supports analysis such as:

Which sellers generate the highest revenue?
Which states have the most active sellers?
Which cities contribute the most sellers?
Which sellers fulfill the highest number of orders?
Which geographic regions have the strongest marketplace presence?
Which sellers have the highest customer satisfaction? (after joining with reviews)
Which sellers experience the highest shipping costs? (after joining with order_items)
How are sellers distributed across Brazil?
KPIs Enabled

When joined with transactional tables, this table enables calculation of:

Total Sellers
Active Sellers
Revenue by Seller
Revenue by State
Revenue by City
Orders per Seller
Average Revenue per Seller
Seller Market Share
Seller Distribution by State
Seller Distribution by City
Data Quality Checks

Before importing the data into PostgreSQL, perform the following validations.

Primary Key Validation
Verify that seller_id is unique.
Check for missing seller_id values.
Missing Values
Check for missing ZIP code prefixes.
Check for missing city names.
Check for missing state values.
Geographic Validation
Verify that state codes follow valid Brazilian state abbreviations.
Check for inconsistent city names.
Validate ZIP code formatting.
Duplicate Records
Verify that duplicate seller_id records do not exist.
Business Importance

The sellers table is the primary seller dimension table in the Olist data model. It provides the descriptive information needed to evaluate seller performance, geographic distribution, and marketplace coverage.

Although this table does not contain sales or revenue data directly, it becomes highly valuable when joined with order_items, allowing analysts to measure seller performance, regional trends, and operational efficiency.

This table is essential for:

Seller performance analysis
Geographic reporting
Marketplace expansion analysis
Executive dashboards
Logistics optimization
Regional sales analysis
Notes & Assumptions
One seller can sell many products.
One seller can fulfill many order items.
Different sellers may contribute products to different customer orders.
Geographic information is used for regional analysis and logistics reporting.
Revenue calculations should use the price column from order_items; this table provides descriptive seller information.
Seller location data can be combined with customer and geolocation data to analyze shipping distances and regional marketplace performance.