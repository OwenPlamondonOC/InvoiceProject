# Feature: Maintain Project Times
**Feature ID:** MPT
**Branch pattern:** `feature/ME-maintain-project-time`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Project Time
**As a** Company Manager
**I want to** input the id, project id, date, hours, and project role assignment id of a new Project Time
**So that** this Project Time's id, project id, date, hours, and project role assignment id gets added to the project
**Priority:** P1
**Independent test:** add a new project time and see it appear on the project's project time list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Project Time
**As a** Company Manager
**I want to** select an Project Time for removal
**So that** the project no longer tracks this project time's id, project id, date, hours, and project role assignment id
**Priority:** P1
**Independent test:** remove an project time and see it no longer appear on the project's project time list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Project Time
**As a** Company Manager
**I want to** input new id, project id, date, hours, and project role assignment id for an existing project time
**So that** this Project Time's id, project id, date, hours, and project role assignment id in the project is updated
**Priority:** P1
**Independent test:** change an existing project time's information and see it changed on the project's project time list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit an project time's id, project id, date, hours, and project role assignment id
- **FR-002**: System MUST store the project time's id, project id, date, hours, and project role assignment id in a project

---
## Key Entities
- **User**: Company Manager; maintains project times
- **Project Time**: Keeps track of time for a project role assignment
- **Project**: stores the id, project id, date, hours, and project role assignment id of project times
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Project Time
#### Scenario: Manager adds a new Project Time
* **Given** I am prompted to enter id, project id, date, hours, and project role assignment id for a new project time
* **When** I enter id, project id, date, hours, and project role assignment id for the new project time
* **Then** The project time gets added to the provided project

### US-N.2 - Remove Project Time
#### Scenario: Manager removes an Project Time
* **Given** I am prompted to select an project time for removal
* **When** I select the project time I wish to remove
* **Then** That project time is removed from the project and the database

### US-N.3 - Edit Project Time
#### Scenario: Manager changes an Project Time's id, project id, date, hours, and project role assignment id
* **Given** I am prompted to select an project time and enter new id, project id, date, hours, and project role assignment id
* **When** I select an project time in the project's project time list
* **And** enter new id, project id, date, hours, and project role assignment id for the project time
* **Then** The project time's new id, project id, date, hours, and project role assignment id is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see project time information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, project id, date, hours, and project role assignment id of an project time if the project time exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create project times |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/project time/read` | Yes | Read an project time's information |
| `POST` | `/project time/edit` | Yes | Change an project time's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "project id": 1,
  "date": "01/01/2000",
  "hours": 3,
  "project role assignment id": 1
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays project time id, project id, date, hours, and project role assignment id

### [View: Edit Page] — route name `edit`
*   Fields: id, project id, date, hours, and project role assignment id
*   Primary action: **Edit Project Time**.
*   Buttons to save or cancel editing of project time
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