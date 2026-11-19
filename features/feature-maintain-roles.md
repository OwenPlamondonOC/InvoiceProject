# Feature: Maintain Roles
**Feature ID:** MRO
**Branch pattern:** `feature/ME-maintain-role`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Role
**As a** Company Manager
**I want to** input the id, name, and standard rate of a new Role
**So that** this Role's id, name, and standard rate gets added to the company
**Priority:** P1
**Independent test:** add a new role and see it appear on the company's role list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Role
**As a** Company Manager
**I want to** select a Role for removal
**So that** the company no longer tracks this role's id, name, and standard rate
**Priority:** P1
**Independent test:** remove a role and see it no longer appear on the company's role list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Role
**As a** Company Manager
**I want to** input new id, name, and standard rate for an existing role
**So that** this Role's id, name, and standard rate in the company is updated
**Priority:** P1
**Independent test:** change an existing role's information and see it changed on the company's role list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit a role's id, name, and standard rate
- **FR-002**: System MUST store the role's id, name, and standard rate in a company

---
## Key Entities
- **User**: Company Manager; maintains roles
- **Role**: Position an employee can take
- **Company**: stores the id, name, and standard rate of roles
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Role
#### Scenario: Manager adds a new Role
* **Given** I am prompted to enter id, name, and standard rate for a new role
* **When** I enter id, name, and standard rate for the new role
* **Then** The role gets added to the provided company

### US-N.2 - Remove Role
#### Scenario: Manager removes a Role
* **Given** I am prompted to select a role for removal
* **When** I select the role I wish to remove
* **Then** That role is removed from the company and the database

### US-N.3 - Edit Role
#### Scenario: Manager changes a Role's id, name, and standard rate
* **Given** I am prompted to select a role and enter new id, name, and standard rate
* **When** I select a role in the company's role list
* **And** enter new id, name, and standard rate for the role
* **Then** The role's new id, name, and standard rate is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see role information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, name, and standard rate of a role if the role exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create roles |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/role/read` | Yes | Read a role's information |
| `POST` | `/role/edit` | Yes | Change a role's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "name": "programmer",
  "rate": "$1/hr"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays role id, name, and standard rate

### [View: Edit Page] — route name `edit`
*   Fields: id, name, and standard rate
*   Primary action: **Edit Role**.
*   Buttons to save or cancel editing of role
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