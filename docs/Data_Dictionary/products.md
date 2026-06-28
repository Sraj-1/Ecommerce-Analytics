# Table: products

## Business Purpose

The `products` table stores the master information for every product available on the Olist marketplace. It contains descriptive attributes such as product category, dimensions, weight, number of photos, and textual information used to identify and describe products.

This table provides the product metadata required for sales analysis, category performance analysis, logistics planning, and product portfolio management. While transactional tables record what customers purchased, this table describes the characteristics of those products.

---

## Business Process

The business process represented by this table is:

```text
Seller Registers Product
          │
          ▼
Product Information Captured
          │
          ▼
Product Published on Marketplace
          │
          ▼
Customer Purchases Product
          │
          ▼
Order Item Created
```

The `products` table stores product information before any customer purchase occurs. It serves as a master data table that supports all downstream sales and logistics processes.

---

## Grain

**One row represents one unique product.**

Each record describes a single product identified by a unique `product_id`.

---

## Primary Key

**Primary Key**

* `product_id`

Each product should have a unique identifier within the dataset.

---

## Foreign Keys

This table does not contain foreign keys.

It is referenced by the following table:

| Referenced By            | Relationship                             |
| ------------------------ | ---------------------------------------- |
| `order_items.product_id` | Connects products to sales transactions. |

---

## Table Relationships

```text
Products
     │
     │ product_id
     ▼
Order Items
     │
     ▼
Orders
     │
     ▼
Customers
```

The `products` table enriches transactional sales data by providing descriptive product attributes.

---

## Column Descriptions

| Column                       | Description                                      |
| ---------------------------- | ------------------------------------------------ |
| `product_id`                 | Unique identifier for each product.              |
| `product_category_name`      | Product category in Portuguese.                  |
| `product_name_lenght`        | Number of characters in the product name.        |
| `product_description_lenght` | Number of characters in the product description. |
| `product_photos_qty`         | Number of product images available.              |
| `product_weight_g`           | Product weight in grams.                         |
| `product_length_cm`          | Product length in centimeters.                   |
| `product_height_cm`          | Product height in centimeters.                   |
| `product_width_cm`           | Product width in centimeters.                    |

---

## Business Questions Supported

This table supports analysis such as:

* Which product categories generate the highest revenue?
* Which categories have the highest sales volume?
* Which products are the heaviest?
* Do heavier products have higher freight costs?
* Which products have the highest average selling price?
* Do products with more images receive better customer ratings?
* Does product description length influence sales?
* Which product categories contribute most to overall business performance?
* Which categories experience the highest delivery costs?

---

## KPIs Enabled

When joined with transactional tables, this table enables calculation of:

* Revenue by Product
* Revenue by Category
* Products Sold
* Product Sales Volume
* Category Sales Share
* Average Product Weight
* Average Product Dimensions
* Average Product Price
* Freight Cost by Category
* Product Popularity
* Category Performance

---

## Data Quality Checks

Before importing the data into PostgreSQL, perform the following validations.

### Primary Key Validation

* Verify that `product_id` is unique.
* Check for missing `product_id` values.

### Missing Values

* Check for missing category names.
* Check for missing dimensions.
* Check for missing product weight.
* Check for missing photo counts.
* Check for missing name or description lengths.

### Numeric Validation

* Verify that weight is greater than zero.
* Verify that dimensions are greater than zero.
* Verify that photo quantity is not negative.
* Identify unusually large or unrealistic dimensions.

### Category Validation

* Identify products without a category.
* Check for inconsistent category names.
* Verify category values before joining with the translation table.

### Duplicate Records

* Verify that duplicate `product_id` records do not exist.

---

## Business Importance

The `products` table is the primary product dimension table within the Olist data model. It provides the descriptive information required to transform transactional sales records into meaningful business insights.

This table is essential for:

* Product performance analysis
* Category performance reporting
* Logistics optimization
* Freight cost analysis
* Product portfolio evaluation
* Executive dashboards
* Marketing analysis

Without this table, analysts could calculate total sales but would not know **which products or categories generated those sales**.

---

## Notes & Assumptions

* One product can appear in many different orders.
* Product attributes are assumed to remain consistent throughout the analysis period.
* Product dimensions are stored in centimeters.
* Product weight is stored in grams.
* `product_category_name` is stored in Portuguese and will later be translated using the `product_category_name_translation` table.
* Revenue calculations should be performed using the `price` column from the `order_items` table rather than this table.
* Product dimensions and weight can be combined with freight costs to analyze shipping efficiency and logistics performance.
