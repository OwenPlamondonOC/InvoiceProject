# Feature: Maintain Project Role Assignments
**Feature ID:** MPRA
**Branch pattern:** `feature/MPRA-maintain-project-role-assignment`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Project Role Assignment
**As a** Company Manager
**I want to** input the id, project role id, and employee id of a new Project Role Assignment
**So that** this Project Role Assignment's id, project role id, and employee id gets added to the employee
**Priority:** P1
**Independent test:** add a new project role assignment and see it appear on the employee's project role assignment list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Project Role Assignment
**As a** Company Manager
**I want to** select a Project Role Assignment for removal
**So that** the employee no longer tracks this project role assignment's id, project role id, and employee id
**Priority:** P1
**Independent test:** remove a project role assignment and see it no longer appear on the employee's project role assignment list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Project Role Assignment
**As a** Company Manager
**I want to** input new id, project role id, and employee id for an existing project role assignment
**So that** this Project Role Assignment's id, project role id, and employee id in the employee is updated
**Priority:** P1
**Independent test:** change an existing project role assignment's information and see it changed on the employee's project role assignment list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit a project role assignment's id, project role id, and employee id
- **FR-002**: System MUST store the project role assignment's id, project role id, and employee id in a employee

---
## Key Entities
- **User**: Company Manager; maintains project role assignments
- **Project Role Assignment**: Assigns a role to an employee for an assignment
- **Employee**: stores the id, project role id, and employee id of project role assignments
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Project Role Assignment
#### Scenario: Manager adds a new Project Role Assignment
* **Given** I am prompted to enter id, project role id, and employee id for a new project role assignment
* **When** I enter id, project role id, and employee id for the new project role assignment
* **Then** The project role assignment gets added to the provided employee

### US-N.2 - Remove Project Role Assignment
#### Scenario: Manager removes a Project Role Assignment
* **Given** I am prompted to select a project role assignment for removal
* **When** I select the project role assignment I wish to remove
* **Then** That project role assignment is removed from the employee and the database

### US-N.3 - Edit Project Role Assignment
#### Scenario: Manager changes a Project Role Assignment's id, project role id, and employee id
* **Given** I am prompted to select a project role assignment and enter new id, project role id, and employee id
* **When** I select a project role assignment in the employee's project role assignment list
* **And** enter new id, project role id, and employee id for the project role assignment
* **Then** The project role assignment's new id, project role id, and employee id is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see project role assignment information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, project role id, and employee id of a project role assignment if the project role assignment exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create project role assignments |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/project role assignment/read` | Yes | Read a project role assignment's information |
| `POST` | `/project role assignment/edit` | Yes | Change a project role assignment's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "project role id": 1,
  "employee id": 1
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays project role assignment id, project role id, and employee id

### [View: Edit Page] — route name `edit`
*   Fields: id, project role id, and employee id
*   Primary action: **Edit Project Role Assignment**.
*   Buttons to save or cancel editing of project role assignment
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