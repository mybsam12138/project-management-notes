# Database Design Standards

## 1. Purpose

This document defines the standards for database design to ensure data consistency, performance, scalability, and maintainability.

---

## 2. General Principles

* Design for **clarity and simplicity first**, then optimize
* Follow **normalization** (3NF) unless justified otherwise
* Avoid redundant data unless required for performance
* Ensure data integrity at the database level
* Prefer explicit over implicit relationships

---

## 3. Naming Conventions

### 3.1 Table Naming

* Use **snake_case**
* Use **plural nouns**

```
users
orders
policy_records
```

---

### 3.2 Column Naming

* Use **snake_case**
* Be descriptive and consistent

```
user_id
created_at
updated_at
is_deleted
```

---

### 3.3 Primary Key

* Use `id` as primary key name
* Prefer **BIGINT / UUID**

---

### 3.4 Foreign Key

* Naming format:

```
<referenced_table>_id
```

Example:

```
user_id
order_id
```

---

## 4. Data Types Standards

### 4.1 Numeric Types

* Monetary values:

```
DECIMAL(18,2)
```

* IDs:

```
BIGINT
```

---

### 4.2 String Types

* Use `VARCHAR(n)` instead of `TEXT` when length is known
* Avoid overly large columns

---

### 4.3 Date/Time

* Use:

```
TIMESTAMP / DATETIME
```

* Standard columns:

```
created_at
updated_at
```

---

### 4.4 Boolean

* Use:

```
BOOLEAN or TINYINT(1)
```

Example:

```
is_active
is_deleted
```

---

## 5. Primary Key Strategy

* Every table must have a primary key
* Preferred:

    * Auto-increment BIGINT
    * Or distributed ID (e.g., Snowflake)

---

## 6. Index Design

### 6.1 General Rules

* Create indexes for:

    * Frequently queried columns
    * Join conditions
    * WHERE conditions

---

### 6.2 Composite Index

* Follow **leftmost prefix rule**

Example:

```
INDEX (user_id, status, created_at)
```

---

### 6.3 Avoid Over-Indexing

* Too many indexes slow down writes

---

## 7. Data Integrity Rules

* Use constraints:

    * NOT NULL
    * UNIQUE
    * FOREIGN KEY (optional depending on system)

---

### Example:

```
email VARCHAR(255) NOT NULL UNIQUE
```

---

## 8. Normalization

* Follow up to **Third Normal Form (3NF)**

Avoid:

* Duplicate data
* Repeating groups

---

## 9. Denormalization (When Needed)

Use when:

* High read performance required
* Complex joins become bottleneck

Must:

* Clearly document reason
* Ensure consistency strategy

---

## 10. Soft Delete Strategy

* Use:

```
is_deleted BOOLEAN DEFAULT FALSE
```

* Avoid physical deletion unless necessary

---

## 11. Audit Fields

Every table should include:

```
created_at
created_by
updated_at
updated_by
```

---

## 12. Transaction Design

* Keep transactions **short**
* Avoid long-running locks
* Ensure atomicity for critical operations

---

## 13. Partitioning & Sharding

Use when:

* Large data volume
* High concurrency

Strategies:

* Range partition (by date)
* Hash partition

---

## 14. Performance Considerations

* Avoid:

    * SELECT *
    * Full table scans

* Prefer:

    * Explicit column selection
    * Pagination

---

## 15. Security

* Avoid storing sensitive data in plain text
* Use encryption where necessary
* Mask sensitive fields

---

## 16. Migration & Version Control

* Use tools:

    * Flyway / Liquibase

* Every change must be:

    * Versioned
    * Reversible

---

## 17. Backup & Recovery

* Regular backups required
* Support point-in-time recovery where possible

---

## 18. Documentation

Each table should document:

* Purpose
* Relationships
* Key fields

---

## 19. Anti-Patterns to Avoid

* No primary key
* Overuse of TEXT fields
* Storing JSON blindly in columns
* Business logic inside database (unless justified)
* Over-normalization

---

## 20. Example Table

```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    is_active BOOLEAN DEFAULT TRUE,
    is_deleted BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP NOT NULL,
    updated_at TIMESTAMP NOT NULL
);
```

---

## 21. Definition of Done (DB Design)

A database design is complete when:

* Naming conventions are followed
* Indexes are properly defined
* Constraints are applied
* Audit fields exist
* Performance considerations reviewed
* Migration script prepared

---

## 22. Summary

A good database design should be:

* Clear
* Consistent
* Scalable
* Maintainable

👉 Design for the future, but avoid over-engineering.
