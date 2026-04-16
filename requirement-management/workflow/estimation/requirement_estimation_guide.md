# Requirement Estimation Guide (5-Person Team)

## Team Setup

- 1 Frontend Developer
- 2 Backend Developers
- 1 Tech Lead
- 1 QA Engineer

---

## 1. Estimation Goal

Estimate:
- Effort (time)
- Complexity
- Risk

Ensure:
- Predictable delivery
- Balanced workload
- Clear expectations

---

## 2. Requirement Classification

### 2.1 By Size

| Size | Description | Effort |
|------|------------|--------|
| Small | Simple change, minor logic | 1–3 days |
| Medium | Standard feature | 3–7 days |
| Large | Complex feature / multiple components | 7–15 days |
| X-Large | Cross-module / high complexity | 15+ days |

---

### 2.2 By Type

- CRUD (simple data operations)
- Business Logic (e.g., premium calculation)
- Integration (external systems)
- UI/UX changes
- Infrastructure / performance

---

## 3. Estimation Process

### Step 1: Requirement Breakdown
- Split into tasks (FE / BE / QA)
- Identify dependencies

---

### Step 2: Complexity Assessment

Consider:
- Logic complexity
- Data model changes
- Integration needs
- Edge cases
- Testing scope

---

### Step 3: Effort Estimation

Each role estimates their part:

Example:

| Task | Role | Effort |
|------|------|--------|
| API development | Backend | 2 days |
| UI page | Frontend | 2 days |
| Testing | QA | 1 day |

Total ≈ 3–5 days → Medium

---

### Step 4: Risk Adjustment

Add buffer for:
- Unclear requirements
- New technology
- External dependency

Typical buffer:
- +10% to +30%

---

## 4. Capacity Planning (6 Months)

### Available Time

- ~100 effective working days per person

### Dev Capacity

- 3 developers × 100 days = 300 dev-days

---

## 5. Estimated Delivery Capacity

### Scenario (Mixed Complexity)

| Type | Count | Avg Effort | Total |
|------|------|-----------|------|
| Small | 20 | 2 days | 40 |
| Medium | 20 | 5 days | 100 |
| Large | 10 | 10 days | 100 |

Total ≈ 240 dev-days

👉 Leaves buffer for:
- Meetings
- Rework
- Bugs

---

## 6. Best Practices

- Always break requirements before estimating
- Estimate by team discussion (not individual guess)
- Use historical data if available
- Re-estimate if requirement changes
- Track actual vs estimated effort

---

## 7. Anti-Patterns

- Estimating without breakdown
- Ignoring QA effort
- Ignoring integration complexity
- Over-optimistic estimation
- Treating all requirements equally

---

## 8. One-line Summary

Requirement estimation is the process of breaking down work, assessing complexity, and assigning realistic effort based on team capacity and risk.

---

## 9. Quick Reference

- Small: 1–3 days
- Medium: 3–7 days
- Large: 7–15 days
- Team capacity (6 months): ~300 dev-days
- Typical delivery: 40–80 requirements
