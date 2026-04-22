# Logging Standard

## 1. Overview

This document defines logging standards to ensure observability, traceability, and effective debugging across the system.

Logging should help answer:

* What happened?
* When did it happen?
* Who was involved?
* Why did it fail?

---

## 2. Logging Principles

* Log for **debugging and monitoring**, not for noise
* Prefer **structured logging** over plain text
* Ensure logs are **searchable and consistent**
* Avoid excessive logging (log only what matters)
* Never log sensitive data

---

## 3. Log Levels

### 3.1 Standard Levels

| Level | Usage                                     |
| ----- | ----------------------------------------- |
| ERROR | System errors, exceptions, failures       |
| WARN  | Unexpected situations, recoverable issues |
| INFO  | Key business events                       |
| DEBUG | Detailed internal state (dev only)        |
| TRACE | Very fine-grained logs (rarely used)      |

---

### 3.2 Usage Guidelines

* Use `INFO` for important business actions
  Example: order created, payment completed

* Use `ERROR` for failures
  Always include exception stack trace

* Use `WARN` for suspicious but non-breaking issues

* Use `DEBUG` only for development or troubleshooting

---

## 4. Log Format (Structured Logging)

### 4.1 Required Fields

Every log should include:

* timestamp
* level
* serviceName
* requestId (or traceId)
* userId (if applicable)
* message

---

### 4.2 Example (JSON format)

```json
{
  "timestamp": "2026-04-22T10:00:00Z",
  "level": "INFO",
  "service": "order-service",
  "requestId": "abc123",
  "userId": "u1001",
  "message": "Order created successfully",
  "orderId": "o9001"
}
```

---

## 5. Request Tracing

* Every request must have a unique `requestId` or `traceId`
* Pass this ID across:

    * Controller
    * Service
    * External calls

---

### Example

```java
log.info("Create order start, requestId={}, userId={}", requestId, userId);
```

---

## 6. What to Log

### 6.1 Must Log

* Incoming requests (key APIs)
* Outgoing external calls
* Business critical actions
* Exceptions and errors

---

### 6.2 Optional

* Debug details (only in DEBUG level)
* Intermediate calculations (if necessary)

---

### 6.3 Must NOT Log

* Passwords
* Tokens / API keys
* Personal sensitive data (PII)
* Full request/response bodies (if sensitive)

---

## 7. Error Logging

* Always log:

    * error message
    * stack trace
    * key parameters

---

### Example

```java
log.error("Create order failed, userId={}, requestId={}", userId, requestId, e);
```

---

## 8. Logging Best Practices

* Use parameterized logging (avoid string concatenation)

❌ Bad:

```java
log.info("User id: " + userId);
```

✅ Good:

```java
log.info("User id: {}", userId);
```

---

* Keep log messages clear and concise
* Avoid duplicate logs for the same event
* Do not log inside tight loops unless necessary

---

## 9. Performance Considerations

* Logging should not significantly impact performance
* Avoid heavy object serialization in logs
* Use async logging if needed

---

## 10. Integration with Monitoring

Logs should be compatible with:

* ELK (Elasticsearch + Logstash + Kibana)
* Grafana + Loki
* Cloud logging platforms

---

## 11. Code Review Checklist

Before merging:

* Proper log level is used
* No sensitive data logged
* requestId / traceId included
* No excessive or duplicate logs
* Error logs include context

---

## 12. One-Line Summary

Logs should tell the story of the system without exposing secrets.
