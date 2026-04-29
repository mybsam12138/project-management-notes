# Requirement Workflow (End-to-End)

## 1. Overview

This document describes a practical end-to-end workflow that transforms raw user needs into delivered and controlled software features with full traceability.

---

## 2. Full Workflow

Elicitation → Analysis & Structuring → Validation → Breakdown → Estimation & Planning → Design → Development → Testing → Delivery → Change Control

---

## 3. Phase Details

## 3.1 Elicitation

### Purpose
Understand the real business need.

### Activities
- Gather requirements from stakeholders
- Ask clarifying questions
- Identify goals, constraints, and context

### Output
- Raw requirement description
- Stakeholder input
- Initial scope

---

## 3.2 Analysis & Structuring

### Purpose
Convert raw input into clear, structured requirements.

### Activities
- Remove ambiguity
- Define functional and non-functional requirements
- Identify dependencies and edge cases
- Define scope boundaries

### Output
- Requirement ID (e.g., REQ-101)
- Structured requirement description
- Acceptance criteria

---

## 3.3 Validation

### Purpose
Ensure correctness of requirements.

### Key Question
Are we building the right thing?

### Activities
- Stakeholder review
- Scenario walkthrough
- Confirm acceptance criteria

### Output
- Approved requirement baseline

---

## 3.4 Breakdown

### Purpose
Split requirements into implementable tasks.

### Activities
- Create task list
- Separate frontend/backend/DB work
- Define task ownership

### Output
- Task IDs (e.g., TASK-101-1)
- Work breakdown structure

---

## 3.5 Estimation & Planning

### Purpose
Estimate effort and plan delivery.

### Activities
- Estimate effort (time/story points)
- Identify risks and dependencies
- Assign priorities and schedule

### Output
- Delivery plan
- Timeline and resource allocation

---

## 3.6 Design

### Purpose
Define how the requirement will be implemented.

### Includes
- Functional design (flows, rules)
- API design (endpoints, request/response)
- Data design (tables, schema)
- System design (modules, services)

### Output
- Design documents
- API specification
- Database schema

### Traceability
- All design artifacts reference requirement ID

---

## 3.7 Development

### Purpose
Implement the solution.

### Activities
- Create branch (linked to requirement/task ID)
- Write code (business logic, API, DB)
- Perform self-review
- Conduct code review
- Execute unit tests

### Traceability
- Branch name includes requirement ID
- Commit message includes requirement/task ID
- Pull request references requirement

### Output
- Working code

---

## 3.8 Testing

### Purpose
Verify correctness and quality.

### Activities
- Create test cases based on requirements
- Execute unit, integration, and system tests
- Perform regression testing

### Traceability
- Test cases linked to requirement ID
- Example: TC-REQ-101-01

### Output
- Test reports
- Defect list

---

## 3.9 Delivery

### Purpose
Release features to users.

### Activities
- Merge code
- Deploy to environment
- Run smoke tests
- Update documentation
- Publish release notes

### Traceability
- Release notes include requirement IDs

### Output
- Deployed feature
- Release record

---

## 3.10 Change Control

### Purpose
Manage requirement changes.

### Activities
- Submit change request
- Perform impact analysis
- Approve or reject change
- Update requirement version
- Implement approved changes

### Output
- Controlled change record
- Updated requirement version

---

## 4. Big-Step Workflow

### Step 1: Discover & Define
- Elicitation
- Analysis & Structuring
- Validation

### Step 2: Plan & Decompose
- Breakdown
- Estimation & Planning

### Step 3: Design Solution
- System, API, and data design

### Step 4: Build & Verify
- Development
- Testing

### Step 5: Deliver & Control
- Delivery
- Change Control

---

## 5. Traceability Model

Business Need  
→ Requirement (REQ-101)  
→ Tasks (TASK-101-1)  
→ Design Docs / API / DB  
→ Code (branch, commit, PR)  
→ Test Cases (TC-REQ-101-01)  
→ Release Notes  

---

## 6. Summary

A strong requirement workflow ensures:
- Clear and structured requirements
- Accurate planning and estimation
- Well-designed solutions
- Traceable implementation
- Controlled and predictable delivery
