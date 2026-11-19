# Feature: Maintain Employees
**Feature ID:** ME
**Branch pattern:** `feature/ME-maintain-employee`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Employee
**As a** Company Manager
**I want to** input the id, name, title, email, and status of a new Employee
**So that** this Employee's id, name, title, email, and status gets added to the company
**Priority:** P1
**Independent test:** add a new employee and see it appear on the company's employee list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Employee
**As a** Company Manager
**I want to** select an Employee for removal
**So that** the company no longer tracks this employee's id, name, title, email, and status
**Priority:** P1
**Independent test:** remove an employee and see it no longer appear on the company's employee list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Employee
**As a** Company Manager
**I want to** input new id, name, title, email, and status for an existing employee
**So that** this Employee's id, name, title, email, and status in the company is updated
**Priority:** P1
**Independent test:** change an existing employee's information and see it changed on the company's employee list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit an employee's id, name, title, email, and status
- **FR-002**: System MUST store the employee's id, name, title, email, and status in a company

---
## Key Entities
- **User**: Company Manager; maintains employees
- **Employee**: Worker at the company
- **Company**: stores the id, name, title, email, and status of employees
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Employee
#### Scenario: Manager adds a new Employee
* **Given** I am prompted to enter id, name, title, email, and status for a new employee
* **When** I enter id, name, title, email, and status for the new employee
* **Then** The employee gets added to the provided company

### US-N.2 - Remove Employee
#### Scenario: Manager removes an Employee
* **Given** I am prompted to select an employee for removal
* **When** I select the employee I wish to remove
* **Then** That employee is removed from the company and the database

### US-N.3 - Edit Employee
#### Scenario: Manager changes an Employee's id, name, title, email, and status
* **Given** I am prompted to select an employee and enter new id, name, title, email, and status
* **When** I select an employee in the company's employee list
* **And** enter new id, name, title, email, and status for the employee
* **Then** The employee's new id, name, title, email, and status is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see employee information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, name, title, email, and status of an employee if the employee exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create employees |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/employee/read` | Yes | Read an employee's information |
| `POST` | `/employee/edit` | Yes | Change an employee's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "name": "John Doe",
  "title": "example",
  "email": "jdoe@example.com",
  "status": "chilling"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays employee id, name, title, email, and status

### [View: Edit Page] — route name `edit`
*   Fields: id, name, title, email, and status
*   Primary action: **Edit Employee**.
*   Buttons to save or cancel editing of employee
*   Verify pressing of save or cancel button

---

## Definition of Done

*   [ ] Backend and frontend implemented per this spec (**FR-00N** satisfied)
*   [ ] **Success Criteria (SC-00N)** met
*   [ ] `features/reference/data-model.md` updated (if schema changed)
*   [ ] `features/reference/api.md` updated (if API changed)
*   [ ] `features/reference/behavior.md` updated (if product rules changed)

---

## Out of Scope

*   User Authorization
* Adding, editing, or deleting any data not listed