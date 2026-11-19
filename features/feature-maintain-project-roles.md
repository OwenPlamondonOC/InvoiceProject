# Feature: Maintain Project Roles
**Feature ID:** ME
**Branch pattern:** `feature/ME-maintain-project-role`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Project Role
**As a** Company Manager
**I want to** input the id, project id, role id, and rate of a new Project Role
**So that** this Project Role's id, project id, role id, and rate gets added to the project
**Priority:** P1
**Independent test:** add a new project role and see it appear on the project's project role list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Project Role
**As a** Company Manager
**I want to** select a Project Role for removal
**So that** the project no longer tracks this project role's id, project id, role id, and rate
**Priority:** P1
**Independent test:** remove a project role and see it no longer appear on the project's project role list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Project Role
**As a** Company Manager
**I want to** input new id, project id, role id, and rate for an existing project role
**So that** this Project Role's id, project id, role id, and rate in the project is updated
**Priority:** P1
**Independent test:** change an existing project role's information and see it changed on the project's project role list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit a project role's id, project id, role id, and rate
- **FR-002**: System MUST store the project role's id, project id, role id, and rate in a project

---
## Key Entities
- **User**: Company Manager; maintains project roles
- **Project Role**: An employee's role for a specific project
- **Project**: stores the id, project id, role id, and rate of project roles
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Project Role
#### Scenario: Manager adds a new Project Role
* **Given** I am prompted to enter id, project id, role id, and rate for a new project role
* **When** I enter id, project id, role id, and rate for the new project role
* **Then** The project role gets added to the provided project

### US-N.2 - Remove Project Role
#### Scenario: Manager removes a Project Role
* **Given** I am prompted to select a project role for removal
* **When** I select the project role I wish to remove
* **Then** That project role is removed from the project and the database

### US-N.3 - Edit Project Role
#### Scenario: Manager changes a Project Role's id, project id, role id, and rate
* **Given** I am prompted to select a project role and enter new id, project id, role id, and rate
* **When** I select a project role in the project's project role list
* **And** enter new id, project id, role id, and rate for the project role
* **Then** The project role's new id, project id, role id, and rate is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see project role information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, project id, role id, and rate of a project role if the project role exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create project roles |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/project role/read` | Yes | Read a project role's information |
| `POST` | `/project role/edit` | Yes | Change a project role's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "project id": 1,
  "role id": 1,
  "rate": "$1/hr"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays project role id, project id, role id, and rate

### [View: Edit Page] — route name `edit`
*   Fields: id, project id, role id, and rate
*   Primary action: **Edit Project Role**.
*   Buttons to save or cancel editing of project role
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