
# Data / Database Design Document (Example)

## 1. Document Overview

### 1.1 Purpose
This document describes the data and database design for a backend system. It defines the core entities, relationships, table structures, constraints, indexing strategy, and design considerations needed to support application development, integration, and future maintenance.

### 1.2 Scope
This example uses a simple **Order Management System** domain to demonstrate how a database design document is typically written. The same structure can be applied to CRM, insurance, ERP, or other enterprise systems.

### 1.3 Audience
- Backend developers
- Frontend developers
- Tech leads
- QA engineers
- DBAs
- Architects

---

## 2. Design Goals

- Support clear and normalized core business data
- Ensure data consistency and integrity
- Provide good query performance for common business scenarios
- Keep the schema maintainable and extensible
- Support auditing and future reporting requirements

---

## 3. Business Context

The system supports the following business flow:

1. A customer places an order
2. An order contains one or more order items
3. The system records product snapshot data inside the order item
4. The order can go through status changes such as CREATED, PAID, SHIPPED, COMPLETED, CANCELLED
5. Payments can be recorded for the order

---

## 4. Entity List

Core entities in this design:

- customer
- product
- order
- order_item
- payment

Supporting concepts:

- order status
- audit fields
- soft delete flag

---

## 5. Entity Relationship Summary

### 5.1 Relationship Overview

- One customer can have many orders
- One order can have many order items
- One product can appear in many order items
- One order can have many payments

### 5.2 ER Summary (Text)

```text
customer 1 --- n orders
orders 1 --- n order_item
product 1 --- n order_item
orders 1 --- n payment
```

---

## 6. Naming Conventions

- Table names use lowercase with underscore, e.g. `order_item`
- Primary key column uses `id`
- Foreign key columns use `{entity}_id`, e.g. `customer_id`
- Datetime columns use `_at`, e.g. `created_at`, `updated_at`
- Boolean-like flags use `is_` prefix where appropriate
- Monetary amounts use `DECIMAL(18,2)`

---

## 7. Table Design

## 7.1 customer

### Purpose
Stores customer master data.

### Table Definition

| Column Name | Type | Nullable | Key | Default | Description |
|------------|------|----------|-----|---------|-------------|
| id | BIGINT | No | PK | - | Customer primary key |
| customer_code | VARCHAR(50) | No | UK | - | Business customer code |
| full_name | VARCHAR(100) | No | - | - | Customer full name |
| email | VARCHAR(100) | Yes | IDX | NULL | Customer email |
| phone | VARCHAR(30) | Yes | - | NULL | Customer phone |
| status | VARCHAR(20) | No | - | 'ACTIVE' | Customer status |
| created_at | DATETIME | No | - | CURRENT_TIMESTAMP | Creation time |
| updated_at | DATETIME | No | - | CURRENT_TIMESTAMP | Last update time |
| is_deleted | TINYINT(1) | No | - | 0 | Soft delete flag |

### Constraints
- PK: `id`
- UK: `customer_code`
- Recommended unique constraint on `email` if business requires one email per customer

---

## 7.2 product

### Purpose
Stores product master data.

### Table Definition

| Column Name | Type | Nullable | Key | Default | Description |
|------------|------|----------|-----|---------|-------------|
| id | BIGINT | No | PK | - | Product primary key |
| product_code | VARCHAR(50) | No | UK | - | Business product code |
| product_name | VARCHAR(200) | No | - | - | Product name |
| category | VARCHAR(50) | Yes | IDX | NULL | Product category |
| unit_price | DECIMAL(18,2) | No | - | 0.00 | Current standard unit price |
| status | VARCHAR(20) | No | - | 'ACTIVE' | Product status |
| created_at | DATETIME | No | - | CURRENT_TIMESTAMP | Creation time |
| updated_at | DATETIME | No | - | CURRENT_TIMESTAMP | Last update time |
| is_deleted | TINYINT(1) | No | - | 0 | Soft delete flag |

### Constraints
- PK: `id`
- UK: `product_code`

---

## 7.3 orders

### Purpose
Stores order header information.

### Table Definition

| Column Name | Type | Nullable | Key | Default | Description |
|------------|------|----------|-----|---------|-------------|
| id | BIGINT | No | PK | - | Order primary key |
| order_no | VARCHAR(50) | No | UK | - | Business order number |
| customer_id | BIGINT | No | FK | - | Reference to customer |
| order_status | VARCHAR(20) | No | IDX | 'CREATED' | Order status |
| order_date | DATETIME | No | IDX | CURRENT_TIMESTAMP | Time order was created |
| total_amount | DECIMAL(18,2) | No | - | 0.00 | Total order amount |
| currency | VARCHAR(10) | No | - | 'USD' | Currency code |
| remarks | VARCHAR(500) | Yes | - | NULL | Remarks |
| created_at | DATETIME | No | - | CURRENT_TIMESTAMP | Creation time |
| updated_at | DATETIME | No | - | CURRENT_TIMESTAMP | Last update time |
| is_deleted | TINYINT(1) | No | - | 0 | Soft delete flag |

### Constraints
- PK: `id`
- UK: `order_no`
- FK: `customer_id` references `customer(id)`

---

## 7.4 order_item

### Purpose
Stores line items under an order.

### Table Definition

| Column Name | Type | Nullable | Key | Default | Description |
|------------|------|----------|-----|---------|-------------|
| id | BIGINT | No | PK | - | Order item primary key |
| order_id | BIGINT | No | FK | IDX | - | Reference to order |
| product_id | BIGINT | No | FK | IDX | - | Reference to product |
| product_code | VARCHAR(50) | No | - | - | Snapshot of product code |
| product_name | VARCHAR(200) | No | - | - | Snapshot of product name |
| unit_price | DECIMAL(18,2) | No | - | 0.00 | Snapshot unit price |
| quantity | INT | No | - | 1 | Purchased quantity |
| line_amount | DECIMAL(18,2) | No | - | 0.00 | Line total amount |
| created_at | DATETIME | No | - | CURRENT_TIMESTAMP | Creation time |
| updated_at | DATETIME | No | - | CURRENT_TIMESTAMP | Last update time |
| is_deleted | TINYINT(1) | No | - | 0 | Soft delete flag |

### Constraints
- PK: `id`
- FK: `order_id` references `orders(id)`
- FK: `product_id` references `product(id)`

### Design Note
Snapshot fields such as `product_code`, `product_name`, and `unit_price` are stored in `order_item` to preserve historical order data even if product master data changes later.

---

## 7.5 payment

### Purpose
Stores payment records for an order.

### Table Definition

| Column Name | Type | Nullable | Key | Default | Description |
|------------|------|----------|-----|---------|-------------|
| id | BIGINT | No | PK | - | Payment primary key |
| payment_no | VARCHAR(50) | No | UK | - | Payment number |
| order_id | BIGINT | No | FK | IDX | - | Reference to order |
| payment_method | VARCHAR(30) | No | - | - | Payment method |
| payment_status | VARCHAR(20) | No | IDX | 'PENDING' | Payment status |
| paid_amount | DECIMAL(18,2) | No | - | 0.00 | Amount paid |
| paid_at | DATETIME | Yes | - | NULL | Payment completion time |
| transaction_ref | VARCHAR(100) | Yes | - | NULL | External transaction reference |
| created_at | DATETIME | No | - | CURRENT_TIMESTAMP | Creation time |
| updated_at | DATETIME | No | - | CURRENT_TIMESTAMP | Last update time |
| is_deleted | TINYINT(1) | No | - | 0 | Soft delete flag |

### Constraints
- PK: `id`
- UK: `payment_no`
- FK: `order_id` references `orders(id)`

---

## 8. Suggested DDL Example

```sql
CREATE TABLE customer (
    id BIGINT PRIMARY KEY,
    customer_code VARCHAR(50) NOT NULL,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NULL,
    phone VARCHAR(30) NULL,
    status VARCHAR(20) NOT NULL DEFAULT 'ACTIVE',
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    is_deleted TINYINT(1) NOT NULL DEFAULT 0,
    CONSTRAINT uk_customer_code UNIQUE (customer_code)
);

CREATE TABLE product (
    id BIGINT PRIMARY KEY,
    product_code VARCHAR(50) NOT NULL,
    product_name VARCHAR(200) NOT NULL,
    category VARCHAR(50) NULL,
    unit_price DECIMAL(18,2) NOT NULL DEFAULT 0.00,
    status VARCHAR(20) NOT NULL DEFAULT 'ACTIVE',
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    is_deleted TINYINT(1) NOT NULL DEFAULT 0,
    CONSTRAINT uk_product_code UNIQUE (product_code)
);

CREATE TABLE orders (
    id BIGINT PRIMARY KEY,
    order_no VARCHAR(50) NOT NULL,
    customer_id BIGINT NOT NULL,
    order_status VARCHAR(20) NOT NULL DEFAULT 'CREATED',
    order_date DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(18,2) NOT NULL DEFAULT 0.00,
    currency VARCHAR(10) NOT NULL DEFAULT 'USD',
    remarks VARCHAR(500) NULL,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    is_deleted TINYINT(1) NOT NULL DEFAULT 0,
    CONSTRAINT uk_order_no UNIQUE (order_no),
    CONSTRAINT fk_orders_customer FOREIGN KEY (customer_id) REFERENCES customer(id)
);

CREATE TABLE order_item (
    id BIGINT PRIMARY KEY,
    order_id BIGINT NOT NULL,
    product_id BIGINT NOT NULL,
    product_code VARCHAR(50) NOT NULL,
    product_name VARCHAR(200) NOT NULL,
    unit_price DECIMAL(18,2) NOT NULL DEFAULT 0.00,
    quantity INT NOT NULL DEFAULT 1,
    line_amount DECIMAL(18,2) NOT NULL DEFAULT 0.00,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    is_deleted TINYINT(1) NOT NULL DEFAULT 0,
    CONSTRAINT fk_order_item_order FOREIGN KEY (order_id) REFERENCES orders(id),
    CONSTRAINT fk_order_item_product FOREIGN KEY (product_id) REFERENCES product(id)
);

CREATE TABLE payment (
    id BIGINT PRIMARY KEY,
    payment_no VARCHAR(50) NOT NULL,
    order_id BIGINT NOT NULL,
    payment_method VARCHAR(30) NOT NULL,
    payment_status VARCHAR(20) NOT NULL DEFAULT 'PENDING',
    paid_amount DECIMAL(18,2) NOT NULL DEFAULT 0.00,
    paid_at DATETIME NULL,
    transaction_ref VARCHAR(100) NULL,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    is_deleted TINYINT(1) NOT NULL DEFAULT 0,
    CONSTRAINT uk_payment_no UNIQUE (payment_no),
    CONSTRAINT fk_payment_order FOREIGN KEY (order_id) REFERENCES orders(id)
);
```

---

## 9. Index Design

### 9.1 Index Principles
Indexes should be created based on real query patterns, not just by habit.

### 9.2 Recommended Indexes

#### customer
- Unique index on `customer_code`
- Index on `email` if customer lookup by email is common

#### product
- Unique index on `product_code`
- Index on `category` if product list filtering by category is common

#### orders
- Unique index on `order_no`
- Index on `customer_id`
- Composite index on `(customer_id, order_date)`
- Index on `order_status`
- Index on `order_date`

#### order_item
- Index on `order_id`
- Index on `product_id`

#### payment
- Unique index on `payment_no`
- Index on `order_id`
- Index on `payment_status`

### 9.3 Example Index DDL

```sql
CREATE INDEX idx_customer_email ON customer(email);
CREATE INDEX idx_product_category ON product(category);
CREATE INDEX idx_orders_customer_id ON orders(customer_id);
CREATE INDEX idx_orders_customer_date ON orders(customer_id, order_date);
CREATE INDEX idx_orders_status ON orders(order_status);
CREATE INDEX idx_order_item_order_id ON order_item(order_id);
CREATE INDEX idx_order_item_product_id ON order_item(product_id);
CREATE INDEX idx_payment_order_id ON payment(order_id);
CREATE INDEX idx_payment_status ON payment(payment_status);
```

---

## 10. Data Integrity Rules

- Each order must belong to one valid customer
- Each order must contain at least one order item at business level
- `line_amount = unit_price * quantity`
- `total_amount` should equal the sum of active order items
- Payment amount should not exceed the order payable amount unless business explicitly allows overpayment
- Business status transitions should be validated in application logic

---

## 11. Normalization and Denormalization

### 11.1 Normalized Parts
- Customer and product are stored as independent master tables
- Foreign keys are used to define relationships

### 11.2 Denormalized Parts
- Product snapshot fields are stored in `order_item`

### 11.3 Reason
This is a deliberate denormalization to preserve historical business meaning and simplify order detail display.

---

## 12. Audit and Soft Delete Strategy

### 12.1 Audit Fields
Each table includes:
- `created_at`
- `updated_at`

Optional future audit fields:
- `created_by`
- `updated_by`

### 12.2 Soft Delete
Each table includes:
- `is_deleted`

### 12.3 Reason
Soft delete supports:
- logical recovery
- audit review
- safer data handling in enterprise systems

---

## 13. Common Query Scenarios

### 13.1 Query Order List by Customer
Business need:
- Show all orders for a customer
- Support filtering by status and date range

Example:
```sql
SELECT id, order_no, order_status, order_date, total_amount
FROM orders
WHERE customer_id = ?
  AND is_deleted = 0
ORDER BY order_date DESC;
```

### 13.2 Query Order Detail
Business need:
- Show order header, items, and payment information

Typical approach:
- Query `orders`
- Query `order_item`
- Query `payment`

### 13.3 Query Product Sales Summary
Business need:
- Aggregate sold quantity and amount by product

Example:
```sql
SELECT
    oi.product_id,
    oi.product_code,
    oi.product_name,
    SUM(oi.quantity) AS total_quantity,
    SUM(oi.line_amount) AS total_sales
FROM order_item oi
JOIN orders o ON oi.order_id = o.id
WHERE o.is_deleted = 0
  AND oi.is_deleted = 0
GROUP BY oi.product_id, oi.product_code, oi.product_name;
```

---

## 14. Performance Considerations

- Avoid over-indexing because indexes increase write cost
- Large text columns should not be indexed blindly
- Frequent list queries should support pagination
- Reporting queries may require separate reporting tables or data warehouse design in the future
- High-volume systems may need partitioning for orders and payments

---

## 15. Security Considerations

- Sensitive fields should be masked when exposed through APIs
- Database access should follow least privilege principle
- SQL injection must be prevented through parameterized queries / ORM / mapper frameworks
- Audit-sensitive tables may require operation logs at application layer

---

## 16. Backup and Recovery Considerations

- Full backup schedule should be defined by operations/DBA
- Incremental/binlog recovery strategy should be available
- Critical business tables should support point-in-time recovery where possible

---

## 17. Future Extension Considerations

Potential future extensions:
- order status history table
- shipment table
- refund table
- customer address table
- product inventory table
- created_by / updated_by fields
- tenant_id for multi-tenant design

---

## 18. Risks and Trade-offs

| Topic | Choice | Benefit | Trade-off |
|-------|--------|---------|-----------|
| Soft delete | Use `is_deleted` | Safer data handling | Queries must always filter deleted data |
| Snapshot in order_item | Keep historical product data | Accurate historical records | Data duplication |
| Use relational design | Strong consistency | Clear structure and constraints | Some reporting queries may become more complex |

---

## 19. Open Questions

- Should email be globally unique for customer?
- Should order cancellation preserve payment records or require refund records?
- Is partial payment allowed?
- Is multi-currency settlement needed in future?
- Does the system need tenant isolation?

---

## 20. Summary

This database design uses a relational model centered around customer, product, order, order item, and payment. It balances normalization and practical denormalization, includes basic audit and soft delete support, and provides a foundation suitable for transactional business systems.

---

## Appendix A: Recommended Document Structure for Real Projects

In real projects, a data/database design document usually includes:

1. Overview
2. Business context
3. Entity list
4. ER model
5. Table definitions
6. Constraints and integrity rules
7. Index design
8. Query scenarios
9. Performance considerations
10. Security considerations
11. Backup/recovery
12. Risks and trade-offs
13. Open questions
14. Change history
