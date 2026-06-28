# Table: orders

## Business Purpose

The `orders` table is the central transactional table in the Olist e-commerce dataset. It records every order placed by customers and tracks the complete order lifecycle from purchase to delivery. This table connects customers with payments, products, sellers, and reviews, making it the foundation for most business analysis.

The table enables the business to monitor operational efficiency, customer experience, order fulfillment, and overall business performance.

---

## Grain

**One row represents one unique order placed by one customer.**

Each record corresponds to a single order identified by a unique `order_id`. All other columns describe different stages of that order's lifecycle.

---

## Primary Key

**Primary Key:** `order_id`

Each order should have a unique `order_id`, which uniquely identifies every order in the dataset.

---

## Foreign Key

| Foreign Key   | References              | Purpose                                       |
| ------------- | ----------------------- | --------------------------------------------- |
| `customer_id` | `customers.customer_id` | Identifies the customer who placed the order. |

---

## Column Descriptions

| Column                          | Description                                                              |
| ------------------------------- | ------------------------------------------------------------------------ |
| `order_id`                      | Unique identifier for each order.                                        |
| `customer_id`                   | Identifier of the customer who placed the order.                         |
| `order_status`                  | Current status of the order (e.g., delivered, shipped, canceled).        |
| `order_purchase_timestamp`      | Date and time when the customer placed the order.                        |
| `order_approved_at`             | Date and time when payment for the order was approved.                   |
| `order_delivered_carrier_date`  | Date and time when the seller handed the order to the logistics carrier. |
| `order_delivered_customer_date` | Date and time when the customer received the order.                      |
| `order_estimated_delivery_date` | Estimated delivery date promised to the customer.                        |

---

## Business Questions Supported

This table helps answer questions such as:

* How many orders were placed?
* How many orders were delivered?
* How many orders were cancelled?
* What are the monthly and yearly order trends?
* What is the average delivery time?
* How many orders were delivered late?
* Which periods have the highest order volume?
* How efficient is the order fulfillment process?
* What percentage of orders are completed successfully?
* How does delivery performance affect customer satisfaction? (after joining with reviews)

---

## KPIs Enabled

The `orders` table supports calculation of the following KPIs:

* Total Orders
* Delivered Orders
* Cancelled Orders
* Order Completion Rate
* Order Cancellation Rate
* Average Delivery Time
* Average Processing Time
* Average Shipping Time
* Late Delivery Rate
* On-Time Delivery Rate
* Monthly Order Growth
* Daily Order Volume
* Order Fulfillment Cycle Time

---

## Data Quality Checks

Before importing the data into PostgreSQL, the following validations should be performed:

### Primary Key Validation

* Verify that `order_id` is unique.
* Check for missing `order_id` values.

### Foreign Key Validation

* Verify that every `customer_id` exists in the `customers` table.

### Missing Values

* Identify missing timestamps.
* Check for missing order status values.

### Date Validations

* Ensure `order_purchase_timestamp` occurs before `order_approved_at`.
* Ensure `order_approved_at` occurs before `order_delivered_carrier_date`.
* Ensure `order_delivered_carrier_date` occurs before `order_delivered_customer_date`.
* Validate that estimated delivery dates are reasonable.

### Status Validation

* Check that `order_status` contains only valid status values.
* Identify inconsistent or unexpected statuses.

### Duplicate Records

* Verify that duplicate `order_id` records do not exist.

---

## Business Importance

The `orders` table is the core fact table of the Olist data model. It links customers, payments, products, sellers, and reviews, enabling comprehensive business analysis across sales, logistics, operations, finance, and customer experience. Nearly every business dashboard and analytical report in this project will rely on this table either directly or through joins with related tables.
