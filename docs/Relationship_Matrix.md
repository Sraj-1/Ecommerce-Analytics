# Relationship Matrix

## Purpose

This document defines the relationships between the tables in the Olist E-Commerce dataset.

Understanding these relationships is essential before designing the PostgreSQL database schema, writing SQL queries, or building analytical dashboards.

---

## Relationship Matrix

| Parent Table | Child Table                       | Relationship       | Primary Key              | Foreign Key                 | Business Meaning                                        |
| ------------ | --------------------------------- | ------------------ | ------------------------ | --------------------------- | ------------------------------------------------------- |
| customers    | orders                            | 1 : Many           | customer_id              | customer_id                 | One customer can place multiple orders.                 |
| orders       | order_items                       | 1 : Many           | order_id                 | order_id                    | One order may contain multiple products.                |
| products     | order_items                       | 1 : Many           | product_id               | product_id                  | A product can appear in many order items.               |
| sellers      | order_items                       | 1 : Many           | seller_id                | seller_id                   | A seller can sell many products across multiple orders. |
| orders       | order_payments                    | 1 : Many           | order_id                 | order_id                    | An order may have multiple payment records.             |
| orders       | order_reviews                     | 1 : 1 (Mostly)     | order_id                 | order_id                    | Most completed orders receive a single review.          |
| products     | product_category_name_translation | Many : 1           | product_category_name    | product_category_name       | Maps Portuguese category names to English translations. |
| customers    | geolocation                       | Many : 1 (Logical) | customer_zip_code_prefix | geolocation_zip_code_prefix | Used to enrich customer location data.                  |
| sellers      | geolocation                       | Many : 1 (Logical) | seller_zip_code_prefix   | geolocation_zip_code_prefix | Used to enrich seller location data.                    |

---

## Relationship Summary

### Core Transaction Flow

Customers → Orders → Order Items

This forms the backbone of the marketplace transaction process.

---

### Product Dimension

Products are linked through the Order Items table.

This enables analysis of:

* Product performance
* Category sales
* Revenue
* Inventory trends

---

### Seller Dimension

Each Order Item references a seller.

This enables:

* Seller performance analysis
* Revenue by seller
* Delivery performance
* Geographic seller analysis

---

### Payment Dimension

Orders may contain multiple payment records.

This supports:

* Installment analysis
* Payment method analysis
* Revenue validation

---

### Review Dimension

Customer reviews are associated with completed orders.

This enables:

* Customer satisfaction analysis
* Delivery impact on ratings
* Review score trends

---

### Geographic Dimension

Customer and Seller ZIP codes connect logically to the Geolocation table.

These relationships support:

* Regional analysis
* Delivery distance estimation
* Geographic visualizations

---

## Notes

* All physical relationships will be enforced using Primary Keys and Foreign Keys where appropriate.
* Geolocation relationships are logical rather than enforced because ZIP code prefixes are not unique.
* Relationship cardinality has been validated against the business process documented during the Business & Data Understanding phase.
