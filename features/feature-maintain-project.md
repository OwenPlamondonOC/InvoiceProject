# Feature: Maintain Projects
**Feature ID:** MP
**Branch pattern:** `feature/ME-maintain-project`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Project
**As a** Company Manager
**I want to** input the id, name, customer id, start date, estimated end date, budget, customer contact, and status of a new Project
**So that** this Project's id, name, customer id, start date, estimated end date, budget, customer contact, and status gets added to the customer
**Priority:** P1
**Independent test:** add a new project and see it appear on the customer's project list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Project
**As a** Company Manager
**I want to** select a Project for removal
**So that** the customer no longer tracks this project's id, name, customer id, start date, estimated end date, budget, customer contact, and status
**Priority:** P1
**Independent test:** remove a project and see it no longer appear on the customer's project list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Project
**As a** Company Manager
**I want to** input new id, name, customer id, start date, estimated end date, budget, customer contact, and status for an existing project
**So that** this Project's id, name, customer id, start date, estimated end date, budget, customer contact, and status in the customer is updated
**Priority:** P1
**Independent test:** change an existing project's information and see it changed on the customer's project list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit a project's id, name, customer id, start date, estimated end date, budget, customer contact, and status
- **FR-002**: System MUST store the project's id, name, customer id, start date, estimated end date, budget, customer contact, and status in a customer

---
## Key Entities
- **User**: Company Manager; maintains projects
- **Customer**: stores the id, name, customer id, start date, estimated end date, budget, customer contact, and status of projects
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Project
#### Scenario: Manager adds a new Project
* **Given** I am prompted to enter id, name, customer id, start date, estimated end date, budget, customer contact, and status for a new project
* **When** I enter id, name, customer id, start date, estimated end date, budget, customer contact, and status for the new project
* **Then** The project gets added to the provided customer

### US-N.2 - Remove Project
#### Scenario: Manager removes a Project
* **Given** I am prompted to select a project for removal
* **When** I select the project I wish to remove
* **Then** That project is removed from the customer and the database

### US-N.3 - Edit Project
#### Scenario: Manager changes a Project's id, name, customer id, start date, estimated end date, budget, customer contact, and status
* **Given** I am prompted to select a project and enter new id, name, customer id, start date, estimated end date, budget, customer contact, and status
* **When** I select a project in the customer's project list
* **And** enter new id, name, customer id, start date, estimated end date, budget, customer contact, and status for the project
* **Then** The project's new id, name, customer id, start date, estimated end date, budget, customer contact, and status is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see project information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, name, customer id, start date, estimated end date, budget, customer contact, and status of a project if the project exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create projects |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/project/read` | Yes | Read a project's information |
| `POST` | `/project/edit` | Yes | Change a project's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "name": "Project",
  "customer id": 1,
  "start date": "1/1/2000",
  "estimated end date": "12/31/2000",
  "budget": "$1",
  "customer contact": "customer@example.com",
  "status": "pending"

}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays project id, name, customer id, start date, estimated end date, budget, customer contact, and status

### [View: Edit Page] — route name `edit`
*   Fields: id, name, customer id, start date, estimated end date, budget, customer contact, and status
*   Primary action: **Edit Project**.
*   Buttons to save or cancel editing of project
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