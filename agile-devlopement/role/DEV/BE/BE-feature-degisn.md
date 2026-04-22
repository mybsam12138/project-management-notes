# Backend Feature Design Document

## 1. Feature Overview

**Feature Name:**
**Description:**
Briefly describe what this feature does and why it exists.

---

## 2. API Design

### 2.1 Endpoint

```
POST /api/v1/{resource}
```

### 2.2 Request

```json
{
  "field1": "string",
  "field2": 123
}
```

### 2.3 Response

```json
{
  "id": "XXX",
  "status": "SUCCESS"
}
```

### 2.4 Error Codes

| Code | Message        | Description        |
| ---- | -------------- | ------------------ |
| 400  | INVALID_PARAM  | Invalid input      |
| 404  | NOT_FOUND      | Resource not found |
| 500  | INTERNAL_ERROR | Server error       |

---

## 3. Business Logic Flow

```
1. Validate request
2. Check business rules
3. Process core logic
4. Save to database
5. Return response
```

---

## 4. Data / Database Impact

### 4.1 Tables

* table_name

### 4.2 Changes

* New field: xxx
* Index: xxx

---

## 5. Validation Rules

* field1 must not be null
* field2 > 0

---

## 6. Integration (if any)

* External API:
* MQ/Event:

---

## 7. Logging & Error Handling

* Log requestId / traceId
* Log key business steps
* Log errors with stack trace

---

## 8. Test Scope

* Unit Test: service logic
* Integration Test: API endpoint

---

## 9. Notes

* Any assumptions
* Known limitations
