# Security Standards

## 1. Purpose

This document defines security standards to protect system data, prevent unauthorized access, and ensure compliance with best practices.

---

## 2. Security Principles

* Follow **Least Privilege Principle**
* Defense in Depth (multiple layers of protection)
* Secure by Default
* Never trust user input
* Encrypt sensitive data
* Log and monitor security events

---

## 3. Authentication

### Standards

* Use secure authentication mechanisms (OAuth2 / JWT / Session)
* Enforce strong password policies:

    * Minimum length ≥ 8
    * Include letters, numbers, special characters
* Passwords must be hashed (e.g., bcrypt)

---

### Example

```java
passwordEncoder.encode(rawPassword);
```

---

## 4. Authorization

### Standards

* Use **RBAC (Role-Based Access Control)**
* Validate permissions at:

    * API level
    * Service layer
* Never rely only on frontend checks

---

## 5. Input Validation

### Standards

* Validate all external inputs:

    * API request parameters
    * Query parameters
    * File uploads

* Use:

    * Whitelisting (preferred)
    * Length validation
    * Format validation

---

## 6. SQL Injection Prevention

### Standards

* Always use prepared statements / ORM
* Never concatenate SQL directly

### ❌ Avoid

```java
String sql = "SELECT * FROM users WHERE name = '" + name + "'";
```

### ✅ Use

```java
PreparedStatement ps = connection.prepareStatement(
  "SELECT * FROM users WHERE name = ?"
);
```

---

## 7. XSS (Cross-Site Scripting) Prevention

### Standards

* Escape output in frontend
* Sanitize user-generated content
* Use secure frameworks

---

## 8. CSRF Protection

### Standards

* Enable CSRF protection for state-changing requests
* Use CSRF tokens

---

## 9. Sensitive Data Protection

### Standards

* Encrypt sensitive data:

    * Passwords (hash)
    * Tokens
    * Personal data

* Do NOT store:

    * Plaintext passwords
    * Secrets in database without encryption

---

## 10. Secret Management

### Standards

* Do NOT hardcode:

    * API keys
    * DB passwords

* Use:

    * Environment variables
    * Secret managers

---

## 11. API Security

### Standards

* Use HTTPS only
* Validate all requests
* Implement rate limiting
* Return minimal error information

---

## 12. Logging & Monitoring

### Standards

* Log:

    * Login attempts
    * Failed access
    * Critical operations

* Do NOT log:

    * Passwords
    * Sensitive personal data

---

## 13. File Upload Security

### Standards

* Validate file type
* Limit file size
* Store outside application directory
* Scan for malicious content if possible

---

## 14. Dependency Security

### Standards

* Regularly update dependencies
* Scan for vulnerabilities

---

## 15. Session Management

### Standards

* Use secure cookies
* Set:

    * HttpOnly
    * Secure flag
* Implement session timeout

---

## 16. Error Handling

### Standards

* Do NOT expose:

    * Stack traces
    * Internal system details

* Return generic error messages

---

## 17. Network Security

### Standards

* Use firewall rules
* Restrict access to internal services
* Separate environments (DEV / TEST / PROD)

---

## 18. Data Access Control

### Standards

* Enforce access control at DB and service level
* Avoid direct DB access from frontend

---

## 19. Backup & Recovery

### Standards

* Encrypt backups
* Restrict access
* Test recovery regularly

---

## 20. Security Testing

### Standards

* Perform:

    * Vulnerability scanning
    * Penetration testing
* Include security in CI/CD pipeline

---

## 21. Definition of Done (Security)

A feature is complete when:

* Input validation implemented
* Authorization checks in place
* Sensitive data protected
* No known vulnerabilities introduced
* Security review completed

---

## 22. Anti-Patterns to Avoid

* Hardcoded secrets
* Trusting frontend validation
* Direct SQL concatenation
* Exposing internal errors
* Over-permissioned users

---

## 23. Summary

Security is not a feature, it is a foundation.

👉 Build secure systems by default, not as an afterthought.
