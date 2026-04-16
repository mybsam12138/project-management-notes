# Requirement → Feature → Task (Detailed Example with Explicit Relationships)

## Overview

This document provides a **detailed, Jira-ready example** of:
- Requirement (business level)
- Feature (business capability)
- Task (execution level with owner, estimate, and explicit feature relationship)

---

## 1. Relationship Model

```text
Requirement (REQ-101)
    ├── Feature (FEAT-101-1 Premium Calculation)
    │      ├── Task (TASK-BE-101-1 Define API contract)
    │      ├── Task (TASK-BE-101-2 Implement pricing lookup and calculation logic)
    │      ├── Task (TASK-BE-101-3 Implement validation and error handling)
    │      ├── Task (TASK-QA-101-1 Create test cases for premium calculation)
    │      └── Task (TASK-QA-101-2 Execute backend/business testing)
    │
    └── Feature (FEAT-101-2 Quotation Result Display)
           ├── Task (TASK-FE-101-1 Build input form for premium calculation)
           ├── Task (TASK-FE-101-2 Integrate with premium calculation API)
           └── Task (TASK-QA-101-3 Execute frontend/display testing)
```

### Rule
- Requirement = overall business goal
- Feature = business capability under that requirement
- Task = execution item under a specific feature
- A task should have:
  - **Parent Requirement**
  - **Parent Feature**
  - **Owner**
  - **Estimate**

---

## 2. Requirement (Business Level)

```text
Requirement ID: REQ-101
Title: Premium Calculation for Quotation

Business Goal:
Allow users (sales agents) to calculate insurance premium automatically during quotation to improve efficiency and accuracy.

Description:
The system shall calculate premium based on user input parameters (age and coverage amount) and return the result to the quotation page.

Scope:
Included:
- Premium calculation based on age and coverage
- Display result on quotation page
- Input validation and error handling

Excluded:
- Discount logic
- Rider pricing
- Renewal calculation

Functional Requirements:
1. System shall accept age and coverage amount.
2. System shall calculate premium using pricing configuration.
3. System shall return premium result to frontend.

Non-Functional Requirements:
- Response time < 2 seconds
- Must not impact existing quotation workflow

Acceptance Criteria:
1. Valid input returns correct premium
2. Missing input returns validation error
3. No pricing rule returns business error

Priority: High
```

---

## 3. Features (Business Capability Level)

### Feature 1

```text
Feature ID: FEAT-101-1
Parent Requirement: REQ-101
Title: Premium Calculation

Description:
Enable system to calculate premium during quotation process based on user input.

Input:
- Age
- Coverage amount

Output:
- Premium amount

Business Value:
- Improve quotation efficiency
- Reduce manual calculation errors
```

### Feature 2

```text
Feature ID: FEAT-101-2
Parent Requirement: REQ-101
Title: Quotation Result Display

Description:
Display calculated premium or error message on quotation page.

Business Value:
- Provide clear feedback to users
- Improve quotation usability
```

---

## 4. Tasks (Execution Level - Jira Ready)

## 4.1 Tasks under FEAT-101-1 Premium Calculation

### TASK-BE-101-1

```text
Task ID: TASK-BE-101-1
Parent Requirement: REQ-101
Parent Feature: FEAT-101-1
Title: [REQ-101][FEAT-101-1][BE] Define premium calculation API contract

Description:
Define request/response structure for premium calculation API.

Owner:
Backend Developer

Estimate:
1 day

Details:
- Endpoint: POST /api/premium/calculate
- Request:
  age: number
  coverageAmount: number
- Response:
  premiumAmount: number

Acceptance Criteria:
- API contract documented
- Frontend can integrate based on contract
```

### TASK-BE-101-2

```text
Task ID: TASK-BE-101-2
Parent Requirement: REQ-101
Parent Feature: FEAT-101-1
Title: [REQ-101][FEAT-101-1][BE] Implement pricing lookup and calculation logic

Description:
Implement backend logic to retrieve pricing factor and calculate premium.

Owner:
Backend Developer

Estimate:
2 days

Details:
- Query pricing_table
- Apply formula: premium = coverageAmount × factor

Acceptance Criteria:
- Correct premium returned for valid input
- Unit test coverage included
```

### TASK-BE-101-3

```text
Task ID: TASK-BE-101-3
Parent Requirement: REQ-101
Parent Feature: FEAT-101-1
Title: [REQ-101][FEAT-101-1][BE] Implement validation and error handling

Description:
Validate input parameters and return proper error messages.

Owner:
Backend Developer

Estimate:
1 day

Acceptance Criteria:
- Missing age returns error
- Invalid coverage returns error
```

### TASK-QA-101-1

```text
Task ID: TASK-QA-101-1
Parent Requirement: REQ-101
Parent Feature: FEAT-101-1
Title: [REQ-101][FEAT-101-1][QA] Create test cases for premium calculation

Description:
Prepare test cases based on acceptance criteria for premium calculation logic and validation.

Owner:
QA Engineer

Estimate:
1 day

Acceptance Criteria:
- Covers valid and invalid calculation scenarios
- Covers no pricing rule scenario
```

### TASK-QA-101-2

```text
Task ID: TASK-QA-101-2
Parent Requirement: REQ-101
Parent Feature: FEAT-101-1
Title: [REQ-101][FEAT-101-1][QA] Execute premium calculation testing

Description:
Execute backend and business-flow related test cases for premium calculation.

Owner:
QA Engineer

Estimate:
1–2 days

Acceptance Criteria:
- All premium calculation scenarios tested
- Defects reported clearly
```

---

## 4.2 Tasks under FEAT-101-2 Quotation Result Display

### TASK-FE-101-1

```text
Task ID: TASK-FE-101-1
Parent Requirement: REQ-101
Parent Feature: FEAT-101-2
Title: [REQ-101][FEAT-101-2][FE] Build input form for premium calculation

Description:
Add age and coverage input fields on quotation page.

Owner:
Frontend Developer

Estimate:
1 day

Acceptance Criteria:
- Input fields displayed correctly
- Values can be entered
```

### TASK-FE-101-2

```text
Task ID: TASK-FE-101-2
Parent Requirement: REQ-101
Parent Feature: FEAT-101-2
Title: [REQ-101][FEAT-101-2][FE] Integrate with premium calculation API and display result

Description:
Call backend API and display premium result or error message.

Owner:
Frontend Developer

Estimate:
1–2 days

Acceptance Criteria:
- API triggered on button click
- Premium result displayed
- Error messages displayed properly
```

### TASK-QA-101-3

```text
Task ID: TASK-QA-101-3
Parent Requirement: REQ-101
Parent Feature: FEAT-101-2
Title: [REQ-101][FEAT-101-2][QA] Execute quotation result display testing

Description:
Verify frontend display of premium result and error handling on quotation page.

Owner:
QA Engineer

Estimate:
1 day

Acceptance Criteria:
- Premium displayed correctly
- Validation errors displayed correctly
- Business errors displayed correctly
```

---

## 5. Feature-to-Task Mapping Table

| Feature ID | Feature Title | Task IDs |
|-----------|---------------|----------|
| FEAT-101-1 | Premium Calculation | TASK-BE-101-1, TASK-BE-101-2, TASK-BE-101-3, TASK-QA-101-1, TASK-QA-101-2 |
| FEAT-101-2 | Quotation Result Display | TASK-FE-101-1, TASK-FE-101-2, TASK-QA-101-3 |

---

## 6. Jira Structure

```text
Epic (Requirement):
REQ-101 Premium Calculation for Quotation

Stories (Features):
FEAT-101-1 Premium Calculation
FEAT-101-2 Quotation Result Display

Subtasks / Tasks:
TASK-BE-101-1 ...
TASK-BE-101-2 ...
TASK-FE-101-1 ...
TASK-QA-101-1 ...
```

### Practical Jira Rule
- Each task should be created **under a feature/story**
- Each feature/story should be created **under a requirement/epic**
- The task title or custom field should still reference the requirement ID for traceability

---

## 7. Key Takeaways

- Requirement = business goal
- Feature = business capability
- Task = execution unit under a specific feature
- A task should not float directly under a requirement without feature context unless the change is very small
- In Jira, the **primary parent of a task is the feature**, while the **requirement is kept as higher-level traceability**

---

## 8. One-line Summary

A complete breakdown should make task-to-feature and feature-to-requirement relationships explicit, so every execution item has both clear implementation context and business traceability.
