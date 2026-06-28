# Table: product_category_name_translation

## Business Purpose

The `product_category_name_translation` table is a reference (lookup) table that translates product category names from Portuguese to English.

Its primary purpose is to improve the readability and usability of reports, dashboards, and business analyses for users who do not understand Portuguese.

This table enriches the `products` table by providing standardized English category names for reporting and visualization.

---

## Business Process

The business process represented by this table is:

```text
Product Registered
        │
        ▼
Category Stored in Portuguese
        │
        ▼
Translation Lookup
        │
        ▼
English Category Used in Reports
```

Unlike transactional tables, this table supports reporting and data presentation rather than recording business events.

---

## Grain

**One row represents one product category translation.**

Each record maps a single Portuguese product category to its English equivalent.

---

## Primary Key

**Primary Key**

* `product_category_name`

Each Portuguese category name should appear only once in the translation table.

---

## Foreign Keys

This table does not contain foreign keys.

It is referenced by:

| Referenced By                    | Relationship                                         |
| -------------------------------- | ---------------------------------------------------- |
| `products.product_category_name` | Maps Portuguese product categories to English names. |

---

## Table Relationships

```text
Products
     │
product_category_name
     │
     ▼
Product Category Translation
     │
     ▼
English Category Name
```

The translation table enriches product data by replacing Portuguese category names with English equivalents for analysis and reporting.

---

## Column Descriptions

| Column                          | Description                                       |
| ------------------------------- | ------------------------------------------------- |
| `product_category_name`         | Product category name in Portuguese.              |
| `product_category_name_english` | English translation of the product category name. |

---

## Business Questions Supported

This table supports analysis such as:

* How can product categories be displayed in English?
* Which English product categories generate the highest revenue?
* Which translated categories have the highest sales volume?
* How can dashboards be made understandable for international stakeholders?
* How can category names be standardized across reports?

---

## KPIs Enabled

Although this table does not generate KPIs directly, it supports the presentation of KPIs such as:

* Revenue by Product Category
* Orders by Product Category
* Products Sold by Category
* Average Review Score by Category
* Freight Cost by Category
* Category Market Share
* Category Sales Trends

---

## Data Quality Checks

Before importing the data into PostgreSQL, perform the following validations.

### Primary Key Validation

* Verify that `product_category_name` is unique.
* Check for missing Portuguese category names.

### Translation Validation

* Check for missing English translations.
* Identify duplicate English translations if necessary.
* Verify consistent spelling and formatting.

### Duplicate Records

* Verify that duplicate category mappings do not exist.

---

## Business Importance

The `product_category_name_translation` table is a supporting reference table that improves data usability rather than storing operational or transactional information.

It allows analysts to produce reports, dashboards, and executive presentations using English category names, making insights easier to understand for international business users and stakeholders.

This table is particularly valuable for:

* Executive dashboards
* Business reports
* Power BI visualizations
* International presentations
* Portfolio projects
* Standardized reporting

---

## Notes & Assumptions

* Each Portuguese category has one English translation.
* Translation values are assumed to be standardized and consistent.
* This table should be joined with the `products` table using `product_category_name`.
* If a product category has no matching translation, reports should clearly indicate the missing translation or provide a fallback.
* This table is used for reporting and presentation purposes only and does not affect transactional calculations.
