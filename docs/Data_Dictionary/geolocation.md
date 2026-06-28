# Table: geolocation

## Business Purpose

The `geolocation` table is a geographic reference table that maps Brazilian ZIP code prefixes to their corresponding latitude, longitude, city, and state.

Unlike transactional tables, this table does not record business events. Instead, it provides geographic information that enriches customer and seller data, enabling spatial analysis, regional reporting, and logistics optimization.

It serves as a lookup table that allows analysts to convert ZIP code prefixes into meaningful geographic locations.

---

## Business Process

The business process represented by this table is:

```text
Customer or Seller Provides ZIP Code
          │
          ▼
ZIP Code Prefix Identified
          │
          ▼
Geographic Information Retrieved
          │
          ▼
Location Used for Analysis
```

This table supports business operations by providing location information rather than recording transactions.

---

## Grain

**One row represents one geographic record associated with a ZIP code prefix.**

Multiple records may exist for the same ZIP code prefix because different geographic coordinates can fall within the same postal region.

---

## Primary Key

**No reliable primary key exists in this table.**

The column `geolocation_zip_code_prefix` is **not unique**, meaning the same ZIP code prefix may appear multiple times.

A surrogate key could be introduced during database design if required.

---

## Foreign Keys

This table does not contain foreign keys.

It is logically related to:

| Related Table | Related Column             | Purpose                  |
| ------------- | -------------------------- | ------------------------ |
| `customers`   | `customer_zip_code_prefix` | Maps customer locations. |
| `sellers`     | `seller_zip_code_prefix`   | Maps seller locations.   |

These relationships are logical rather than enforced through database constraints in the raw dataset.

---

## Table Relationships

```text
Customers
      │
customer_zip_code_prefix
      │
      ▼
Geolocation
      ▲
      │
seller_zip_code_prefix
      │
Sellers
```

The `geolocation` table enriches customer and seller records with geographic coordinates and regional information.

---

## Column Descriptions

| Column                        | Description                                                     |
| ----------------------------- | --------------------------------------------------------------- |
| `geolocation_zip_code_prefix` | Brazilian ZIP code prefix used to identify a geographic region. |
| `geolocation_lat`             | Latitude coordinate of the ZIP code region.                     |
| `geolocation_lng`             | Longitude coordinate of the ZIP code region.                    |
| `geolocation_city`            | City associated with the ZIP code prefix.                       |
| `geolocation_state`           | Brazilian state associated with the ZIP code prefix.            |

---

## Business Questions Supported

This table supports analysis such as:

* Where are customers located?
* Where are sellers located?
* Which states generate the highest revenue?
* Which cities have the highest order volume?
* What is the geographic distribution of customers?
* What is the geographic distribution of sellers?
* Which regions experience the highest shipping costs?
* How far are sellers from customers? (after deriving distances)
* Which regions experience longer delivery times?

---

## KPIs Enabled

When joined with customer, seller, and order data, this table enables calculation of:

* Customers by State
* Customers by City
* Sellers by State
* Sellers by City
* Revenue by State
* Revenue by City
* Orders by Region
* Geographic Sales Distribution
* Average Delivery Time by Region
* Shipping Distance Analysis (derived)

---

## Data Quality Checks

Before importing the data into PostgreSQL, perform the following validations.

### ZIP Code Validation

* Check for missing ZIP code prefixes.
* Verify ZIP code formatting.
* Identify duplicate ZIP code prefixes.

### Coordinate Validation

* Check for missing latitude values.
* Check for missing longitude values.
* Verify latitude values fall within valid geographic ranges.
* Verify longitude values fall within valid geographic ranges.

### Geographic Validation

* Check for missing city names.
* Check for missing state abbreviations.
* Verify valid Brazilian state codes.
* Identify inconsistent city spellings.

### Duplicate Records

* Investigate duplicate ZIP code prefixes to determine whether they represent valid multiple coordinate entries.

---

## Business Importance

The `geolocation` table is the geographic dimension of the Olist data model. It enables regional analysis by linking customer and seller ZIP code prefixes to geographic coordinates.

Although it does not directly contain sales or operational data, it provides the location context necessary for logistics analysis, regional performance reporting, delivery optimization, and geographic visualizations.

This table is essential for:

* Regional sales analysis
* Logistics optimization
* Geographic dashboards
* Customer distribution analysis
* Seller distribution analysis
* Delivery performance by region

---

## Notes & Assumptions

* A ZIP code prefix may appear multiple times in the dataset.
* Geographic coordinates represent locations within a ZIP code region rather than precise customer or seller addresses.
* Customer and seller tables reference ZIP code prefixes rather than latitude and longitude directly.
* Geographic information will primarily be used for visualization and regional performance analysis.
* During database design, duplicate ZIP code prefixes may require special handling depending on reporting requirements.
