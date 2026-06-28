# Data Quality Notes

## Purpose

This document identifies potential data quality risks within the Olist E-Commerce dataset before importing the data into PostgreSQL.

The goal is not to clean the data yet, but to understand potential issues that could affect business analysis and define validation checks for future phases.

---

# Objectives

* Identify potential data quality risks.
* Document expected validation rules.
* Record assumptions.
* Prepare for Data Cleaning (Phase 7).

---

# Table-Level Data Quality Risks

## customers

### Potential Issues

* Duplicate customer_id values.
* Missing city or state values.
* Invalid ZIP code prefixes.

### Planned Validation

* Verify Primary Key uniqueness.
* Check for missing geographic information.
* Validate ZIP code format.

---

## orders

### Potential Issues

* Missing delivery dates.
* Missing approval timestamps.
* Invalid order statuses.
* Purchase dates occurring after delivery dates.

### Planned Validation

* Verify Primary Key uniqueness.
* Validate chronological order of timestamps.
* Identify cancelled and unavailable orders.
* Detect unusually long delivery durations.

---

## order_items

### Potential Issues

* Duplicate order-product combinations.
* Missing seller_id.
* Invalid freight values.
* Zero or negative quantities (if present).

### Planned Validation

* Verify composite uniqueness.
* Validate foreign key references.
* Check freight cost distribution.
* Detect duplicate records.

---

## products

### Potential Issues

* Missing product category names.
* Missing dimensions.
* Missing weight information.

### Planned Validation

* Measure category completeness.
* Validate physical measurements.
* Detect invalid dimension values.

---

## sellers

### Potential Issues

* Duplicate seller IDs.
* Missing city or state information.

### Planned Validation

* Verify Primary Key uniqueness.
* Validate location fields.
* Check ZIP code consistency.

---

## order_payments

### Potential Issues

* Multiple payment records per order.
* Outlier payment values.
* Missing payment types.
* Invalid installment counts.

### Planned Validation

* Validate payment totals.
* Review payment method distribution.
* Detect unusually high payment amounts.

---

## order_reviews

### Potential Issues

* Missing review comments.
* Missing review dates.
* Review scores outside expected range.

### Planned Validation

* Verify review score range (1–5).
* Measure percentage of missing comments.
* Validate review timestamps.

---

## geolocation

### Potential Issues

* Duplicate ZIP code prefixes.
* Missing latitude or longitude.
* Inconsistent city spelling.

### Planned Validation

* Measure duplicate rate.
* Validate coordinate ranges.
* Standardize city names during cleaning if required.

---

## product_category_name_translation

### Potential Issues

* Missing translations.
* Duplicate category mappings.

### Planned Validation

* Verify one-to-one mappings.
* Ensure every product category has a valid English translation.

---

# Cross-Table Validation

The following integrity checks will be performed after data import:

* Every order must reference an existing customer.
* Every order item must reference an existing order.
* Every order item must reference an existing product.
* Every order item must reference an existing seller.
* Every payment must reference an existing order.
* Every review must reference an existing order.

---

# Expected Outliers

Potential outliers include:

* Extremely high payment values.
* Long delivery durations.
* Very large freight charges.
* Products with unusually large dimensions.

These values will be investigated before deciding whether they represent data errors or legitimate business events.

---

# Assumptions

* Missing delivery dates generally indicate undelivered or cancelled orders.
* Missing review comments do not imply missing review scores.
* Duplicate ZIP code prefixes in the Geolocation table are expected because multiple geographic coordinates may exist for the same ZIP code prefix.
* Multiple payment records for a single order are valid business scenarios.

---

# Future Actions (Phase 7)

During the Data Cleaning phase, we will:

* Validate Primary Keys.
* Validate Foreign Keys.
* Handle missing values.
* Remove duplicates where appropriate.
* Standardize categorical values.
* Investigate outliers.
* Document all cleaning decisions to ensure reproducibility.
