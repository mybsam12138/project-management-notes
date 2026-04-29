# Code Review Guidelines

## 1. Purpose

This document defines the standards for code review to ensure code quality, maintainability, security, and consistency across the project.

---

## 2. Review Principles

* Review code, not the person
* Be constructive and respectful
* Focus on critical issues first (correctness, security)
* Keep reviews small and frequent
* Aim for knowledge sharing

---

## 3. Scope of Review

Reviewers must evaluate:

* Functionality correctness
* Code quality and readability
* Performance considerations
* Security risks
* Test coverage
* Adherence to standards

---

## 4. Review Checklist

### 4.1 Functionality

* Does the code meet the requirements?
* Are edge cases handled?
* Are error scenarios covered?

---

### 4.2 Code Quality

* Clear naming (variables, methods, classes)
* Functions are small and focused
* No duplicated logic
* Proper separation of concerns (Controller / Service / Repository)

---

### 4.3 Readability

* Easy to understand without excessive comments
* Consistent coding style
* Avoid unnecessary complexity

---

### 4.4 Performance

* Avoid unnecessary loops or queries
* Check for N+1 queries
* Use appropriate data structures

---

### 4.5 Security

* No hardcoded secrets
* Input validation present
* No SQL injection risks
* Proper authorization checks

---

### 4.6 Error Handling

* Exceptions handled properly
* No sensitive data exposed in responses
* Logging is appropriate

---

### 4.7 Testing

* Unit tests included for new logic
* Tests cover critical paths
* Tests are deterministic (no random failures)

---

## 5. Common Issues to Check

* NullPointerException risks
* Incorrect boundary handling
* Magic numbers
* Dead code
* Unused variables/imports

---

## 6. API Review

* Consistent naming (RESTful)
* Proper HTTP methods (GET/POST/PUT/DELETE)
* Proper status codes
* Input/output validation

---

## 7. Database Review

* Proper indexing
* No unnecessary queries
* Transactions handled correctly
* No raw SQL injection risk

---

## 8. Logging

* Important actions are logged
* No sensitive data in logs
* Use appropriate log levels (INFO/WARN/ERROR)

---

## 9. Review Process

### 9.1 Before Submitting PR

* Code compiles successfully
* Tests pass
* Self-review completed

---

### 9.2 During Review

* Reviewer provides actionable comments
* Use examples where necessary
* Avoid blocking for minor style issues

---

### 9.3 After Review

* Author addresses comments
* Reviewer verifies fixes
* Approve and merge

---

## 10. PR Size Guidelines

* Keep PR small (< 500 lines recommended)
* Large changes should be split

---

## 11. Commenting Guidelines

### Good Comment Example

```text
This method may cause N+1 query issue when processing large datasets.
Consider batching or using JOIN.
```

### Bad Comment Example

```text
This code is bad.
```

---

## 12. Do's and Don'ts

### Do

* Ask questions
* Suggest improvements
* Highlight risks

### Don't

* Be personal or emotional
* Nitpick trivial issues excessively
* Approve without understanding

---

## 13. Definition of Done (Code Review)

A PR is complete when:

* All comments are addressed
* At least one approval is obtained
* Tests pass
* No critical issues remain

---

## 14. Tools

* GitHub / GitLab PR
* Static analysis tools (SonarQube)
* Dependency scanning tools

---

## 15. Summary

Code review is a critical process to ensure quality, share knowledge, and reduce defects.

👉 Focus on impact, not perfection.
