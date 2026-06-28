# Table: order_reviews

## Business Purpose

The `order_reviews` table stores customer feedback for completed orders. It captures review ratings, optional review titles, review comments, and review timestamps submitted after the customer receives an order.

This table enables customer satisfaction analysis, service quality monitoring, seller performance evaluation, and customer experience measurement. It provides qualitative and quantitative feedback that helps identify operational issues affecting customer satisfaction.

---

## Business Process

The business process represented by this table is:

```text
Customer Places Order
          │
          ▼
Order Delivered
          │
          ▼
Customer Receives Product
          │
          ▼
Customer Leaves Review
          │
          ▼
Review Stored
```

Reviews are submitted after customers complete their shopping experience, making this table an important source of customer feedback.

---

## Grain

**One row represents one customer review for one order.**

Each record corresponds to a single review identified by a unique `review_id`.

---

## Primary Key

**Primary Key**

* `review_id`

Each review should have a unique identifier.

---

## Foreign Keys

| Foreign Key | References        | Purpose                                      |
| ----------- | ----------------- | -------------------------------------------- |
| `order_id`  | `orders.order_id` | Associates the review with a customer order. |

---

## Table Relationships

```text
Customers
     │
     ▼
Orders
     │
     ▼
Order Reviews
```

The `order_reviews` table connects customer satisfaction data with order information, allowing analysts to evaluate how operational performance influences customer experience.

---

## Column Descriptions

| Column                    | Description                                                           |
| ------------------------- | --------------------------------------------------------------------- |
| `review_id`               | Unique identifier for each review.                                    |
| `order_id`                | Unique identifier of the reviewed order.                              |
| `review_score`            | Customer rating for the order, typically on a scale of 1 to 5.        |
| `review_comment_title`    | Optional title provided by the customer.                              |
| `review_comment_message`  | Optional detailed review message.                                     |
| `review_creation_date`    | Date the customer created the review.                                 |
| `review_answer_timestamp` | Timestamp when the review was submitted and recorded by the platform. |

---

## Business Questions Supported

This table supports analysis such as:

* What is the average customer rating?
* What percentage of reviews are positive?
* Which sellers receive the highest ratings?
* Which product categories receive poor reviews?
* Does late delivery reduce customer satisfaction?
* Do expensive products receive better ratings?
* Which states have the happiest customers?
* How does delivery performance affect review scores?
* What are the most common customer complaints? (using review comments)

---

## KPIs Enabled

When joined with other tables, this table enables calculation of:

* Average Review Score
* Customer Satisfaction Score
* Positive Review Rate
* Negative Review Rate
* Review Distribution (1–5 Stars)
* Average Rating by Seller
* Average Rating by Product Category
* Average Rating by State
* Review Response Volume
* Customer Satisfaction Trends

---

## Data Quality Checks

Before importing the data into PostgreSQL, perform the following validations.

### Primary Key Validation

* Verify that `review_id` is unique.
* Check for missing `review_id` values.

### Foreign Key Validation

* Verify that every `order_id` exists in the `orders` table.

### Missing Values

* Check for missing review scores.
* Check for missing review creation dates.
* Identify missing review titles and comments (optional fields).

### Rating Validation

* Verify that `review_score` contains only valid values (1–5).
* Identify invalid or unexpected rating values.

### Date Validation

* Ensure review creation dates occur after the corresponding order purchase date.
* Check for unrealistic review timestamps.

### Duplicate Records

* Verify that duplicate review records do not exist.

---

## Business Importance

The `order_reviews` table is the primary customer feedback table in the Olist data model. It provides direct insight into customer satisfaction and the overall shopping experience.

By joining this table with orders, products, sellers, and payments, analysts can identify the operational factors that influence customer ratings, such as delivery delays, seller performance, and product quality.

This table is essential for:

* Customer experience analysis
* Seller performance evaluation
* Product quality monitoring
* Executive dashboards
* Service improvement initiatives
* Customer satisfaction reporting

---

## Notes & Assumptions

* Each review is associated with one order.
* Review comments are optional; customers may submit only a rating.
* Review scores are assumed to use a 1–5 rating scale.
* Customer satisfaction analysis should combine review data with delivery and payment information for a complete understanding of the customer experience.
* Text comments can later be used for sentiment analysis or text mining to identify recurring customer issues.
