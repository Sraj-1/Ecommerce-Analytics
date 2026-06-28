# Data Dictionary

---

# Table: customers

## Business Purpose

Stores information about customers who place orders on the Olist marketplace. It provides customer identifiers and geographic information used for customer segmentation, regional analysis, logistics, and marketing.

---

## Grain

One record represents one customer record associated with an order.

(Note: We will verify later whether customer_id or customer_unique_id represents the true business customer.)

---

## Primary Key

customer_id (To be validated)

---

## Foreign Keys

None in this table.

Referenced by:
orders.customer_id

---

## Columns

| Column | Description |
|----------|-------------|
| customer_id | Transaction-level customer identifier |
| customer_unique_id | Unique identifier for the actual customer across purchases |
| customer_zip_code_prefix | ZIP code prefix |
| customer_city | Customer city |
| customer_state | Customer state |

---

## Business Questions Supported

- How many customers do we have?
- Which states have the most customers?
- Which cities generate the most business?
- Revenue by geography (after joining with orders)
- Customer lifetime value (after joining with payments)
- Customer satisfaction by region (after joining with reviews)

---

## Potential Data Quality Checks

- Duplicate customer_id
- Missing customer_unique_id
- Missing city/state
- Invalid state codes
- ZIP code formatting