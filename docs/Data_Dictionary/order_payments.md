Table: order_payments
Business Purpose

The order_payments table records the payment details for each customer order. It captures how customers paid for their purchases, including the payment method, installment plan, payment sequence, and total payment amount.

This table enables financial analysis, payment behavior analysis, revenue reporting, and customer payment preference analysis. It is the primary source for understanding how money flows into the business.

Business Process

The business process represented by this table is:

Customer Places Order
          │
          ▼
Customer Selects Payment Method
          │
          ▼
Payment Processed
          │
          ▼
Payment Confirmed
          │
          ▼
Order Approved

A customer may complete payment using one or more payment methods. Each payment transaction is recorded as a separate row.

Grain

One row represents one payment transaction associated with one order.

An order can have multiple payment transactions, making this table more granular than the orders table.

Primary Key

Composite Primary Key (Candidate)

order_id
payment_sequential

The combination uniquely identifies each payment transaction for an order.

Foreign Keys
Foreign Key	References	Purpose
order_id	orders.order_id	Associates the payment with a customer order.
Table Relationships
Orders
   │
   │ order_id
   ▼
Order Payments

The order_payments table extends the orders table by adding financial transaction details.

Column Descriptions
Column	Description
order_id	Unique identifier of the order associated with the payment.
payment_sequential	Sequence number of the payment transaction within the order.
payment_type	Payment method used (e.g., credit card, boleto, voucher, debit card).
payment_installments	Number of installments selected by the customer.
payment_value	Total amount paid in the payment transaction.
Business Questions Supported

This table supports analysis such as:

Which payment methods are most commonly used?
What percentage of customers pay by credit card?
How many customers choose installment payments?
What is the average payment value?
Which payment methods generate the highest revenue?
Do installment payments influence order value?
Are there orders with multiple payment transactions?
What is the total payment value collected?
KPIs Enabled

When joined with other tables, this table enables calculation of:

Total Revenue
Revenue by Payment Method
Average Payment Value
Average Installments per Order
Credit Card Usage Rate
Installment Usage Rate
Payment Method Distribution
Revenue by Installment Count
Orders with Multiple Payments
Average Order Payment Value
Data Quality Checks

Before importing the data into PostgreSQL, perform the following validations.

Primary Key Validation
Verify that (order_id, payment_sequential) combinations are unique.
Check for missing key values.
Foreign Key Validation
Verify that every order_id exists in the orders table.
Missing Values
Check for missing payment types.
Check for missing installment counts.
Check for missing payment values.
Numeric Validation
Verify that payment_value is greater than zero.
Verify that payment_installments is greater than or equal to one.
Identify unusually high payment values for investigation.
Payment Method Validation
Verify that payment types contain only valid values.
Check for inconsistent payment method naming.
Duplicate Records
Verify that duplicate payment transactions do not exist.
Business Importance

The order_payments table is the primary financial transaction table in the Olist data model. It provides the information required to analyze customer payment behavior, payment preferences, and revenue generation.

Although the order_items table contains product prices, this table records how customers actually paid for their purchases. It is essential for financial reporting, payment analysis, and executive revenue dashboards.

This table is fundamental for:

Revenue analysis
Financial reporting
Payment behavior analysis
Installment analysis
Executive dashboards
Customer payment preference analysis
Notes & Assumptions
One order may have multiple payment transactions.
Multiple payment methods can be used for a single order.
payment_sequential determines the order of payment transactions.
payment_value represents the amount paid in a specific payment transaction.
Revenue calculations should be validated by comparing payment totals with sales totals from the order_items table.
Installment information reflects the customer's chosen payment plan and can be used to analyze purchasing behavior.