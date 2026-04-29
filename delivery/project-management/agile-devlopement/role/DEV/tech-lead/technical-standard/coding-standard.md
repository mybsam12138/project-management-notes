# Coding Standard

## 1. Overview

This document defines the coding standards and best practices to ensure consistency, readability, and maintainability across the codebase.

---

## 2. General Principles

* Write clean, readable, and maintainable code
* Follow the DRY (Don't Repeat Yourself) principle
* Prefer simplicity over complexity (KISS)
* Avoid premature optimization
* Code should be self-explanatory whenever possible

---

## 3. Naming Conventions

### 3.1 General Rules

* Use meaningful and descriptive names
* Avoid abbreviations unless widely understood (e.g., `id`, `url`)
* Keep naming consistent across the project

### 3.2 Java

* Classes: `PascalCase`

    * Example: `UserService`, `OrderController`
* Methods / Variables: `camelCase`

    * Example: `getUserById`, `orderList`
* Constants: `UPPER_CASE`

    * Example: `MAX_RETRY_COUNT`

### 3.3 Frontend (Vue / JS)

* Components: `PascalCase`

    * Example: `UserTable.vue`
* Props / Variables: `camelCase`
* Event names: `kebab-case`

    * Example: `user-selected`

---

## 4. Code Structure

### 4.1 Layered Architecture

* Controller → Handle request/response
* Service → Business logic
* Repository → Data access

**Do not mix responsibilities across layers**

---

### 4.2 Function Design

* Keep functions under **50 lines**
* Each function should do **one thing only**
* Use early return to reduce nesting

### 4.3 Nesting Rules

* Maximum nesting depth: **3 levels**

❌ Bad:

```java
if (a) {
  if (b) {
    if (c) {
      if (d) {
        // too deep
      }
    }
  }
}
```

✅ Good:

```java
if (!a) return;
if (!b) return;
if (!c) return;

// clean logic here
```

---

## 5. Error Handling

* Do not swallow exceptions
* Always log meaningful error messages
* Use custom exceptions for business logic

Example:

```java
throw new BusinessException("USER_NOT_FOUND");
```

---

## 6. Code Style

### 6.1 Formatting

* Use consistent indentation (2 or 4 spaces)
* Max line length: 120 characters
* Add blank lines between logical sections

### 6.2 Comments

* Prefer self-explanatory code over comments
* Use comments only when necessary
* Avoid redundant comments

❌ Bad:

```java
// increment i
i++;
```

---

## 7. API Related Code

* Use consistent naming for endpoints
* Use plural nouns

Example:

```
GET /users
POST /orders
```

* Do not expose internal models directly
* Always use DTOs for API responses

---

## 8. Logging

* Use structured logging
* Include key identifiers (e.g., requestId, userId)

Example:

```java
log.info("Create order success, userId={}, orderId={}", userId, orderId);
```

---

## 9. Security Practices

* Never log sensitive data (passwords, tokens)
* Validate all inputs
* Use parameterized queries to prevent SQL injection

---

## 10. Code Review Checklist

Before submitting PR:

* Code is readable and clean
* No duplicated logic
* Proper error handling
* Naming is consistent
* No unused code
* Tests are included (if applicable)

---

## 11. One-Line Summary

Write code for humans first, machines second.
