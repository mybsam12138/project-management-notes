# Sprint Backlog Example

## Sprint Information
- **Sprint Name:** Sprint 12 - Product Management Module
- **Duration:** 2026-04-21 ~ 2026-05-05
- **Sprint Goal:**  
  Deliver core Product Management features including:
    - Create Product
    - Product List (with pagination)
    - Delete Product

---

## Sprint Backlog (Task Breakdown)

### User Story: US-101 - Create Product
_As an operator, I want to create a new product_

| Task ID | Task Description | Owner | Estimate (hours) | Status |
|--------|----------------|-------|------------------|--------|
| T-101-1 | Design Product table schema (DB) | Backend A | 4h | Todo |
| T-101-2 | Implement Create Product API (Spring Boot) | Backend A | 6h | Todo |
| T-101-3 | Add request validation (required fields) | Backend A | 2h | Todo |
| T-101-4 | Write unit tests | Backend A | 3h | Todo |
| T-101-5 | Build frontend form (Vue3) | Frontend | 6h | Todo |
| T-101-6 | Form validation + API integration | Frontend | 3h | Todo |

---

### User Story: US-102 - Product List
_As a user, I want to view product list with pagination_

| Task ID | Task Description | Owner | Estimate | Status |
|--------|----------------|-------|----------|--------|
| T-102-1 | Implement list API (pagination) | Backend B | 5h | Todo |
| T-102-2 | Optimize SQL (index + pagination) | Backend B | 3h | Todo |
| T-102-3 | Build table UI (Element Plus) | Frontend | 6h | Todo |
| T-102-4 | Integrate pagination component | Frontend | 2h | Todo |

---

### User Story: US-103 - Delete Product
_As an operator, I want to delete a product_

| Task ID | Task Description | Owner | Estimate | Status |
|--------|----------------|-------|----------|--------|
| T-103-1 | Implement delete API (logical delete) | Backend A | 3h | Todo |
| T-103-2 | Add RBAC permission check | Backend A | 2h | Todo |
| T-103-3 | Add delete button + confirmation modal | Frontend | 3h | Todo |

---

## Impediments (Blockers)

| ID | Issue | Impact | Owner | Status |
|----|------|--------|--------|--------|
| IMP-1 | No DB permission in test environment | Cannot test create API | DevOps | In Progress |
| IMP-2 | Product field definition not finalized | API cannot be completed | PO | Pending |

---

## Daily Tracking (Example)

| Day | Completed | Remaining | Risk |
|-----|----------|----------|------|
| Day 1 | DB schema done | API not started | None |
| Day 2 | Create API done | Frontend not integrated | API not tested |

---

## Key Principles

### 1. Story → Task Breakdown
Each user story must be broken down into:
- Backend tasks
- Frontend tasks
- Testing tasks

---

### 2. Tasks Must Be Actionable
❌ Bad:
- "Complete product module"

✅ Good:
- "Implement create product API"

---

### 3. Clear Ownership
Each task must have a single owner.

---

### 4. Estimation Is Required
Without estimates:
- Sprint planning becomes unreliable
- Workload cannot be controlled

---

## Summary

A Sprint Backlog is:

> A structured, executable, and trackable task list derived from prioritized user stories.