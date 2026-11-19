# Feature: Maintain <Entity>s
**Feature ID:** ME
**Branch pattern:** `feature/ME-maintain-<entity>`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add <Entity>
**As a** Company Manager
**I want to** input the <information> of a new <Entity>
**So that** this <Entity>'s <information> gets added to the <parent>
**Priority:** P1
**Independent test:** add a new <entity> and see it appear on the <parent>'s <entity> list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove <Entity>
**As a** Company Manager
**I want to** select an <Entity> for removal
**So that** the <parent> no longer tracks this <entity>'s <information>
**Priority:** P1
**Independent test:** remove an <entity> and see it no longer appear on the <parent>'s <entity> list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit <Entity>
**As a** Company Manager
**I want to** input new <information> for an existing <entity>
**So that** this <Entity>'s <information> in the <parent> is updated
**Priority:** P1
**Independent test:** change an existing <entity>'s information and see it changed on the <parent>'s <entity> list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit an <entity>'s <information>
- **FR-002**: System MUST store the <entity>'s <information> in a <parent>

---
## Key Entities
- **User**: Company Manager; maintains <entity>s
- **<Entity>**: 
- **<Parent>**: stores the <information> of <entity>s
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add <Entity>
#### Scenario: Manager adds a new <Entity>
* **Given** I am prompted to enter <information> for a new <entity>
* **When** I enter <information> for the new <entity>
* **Then** The <entity> gets added to the provided <parent>

### US-N.2 - Remove <Entity>
#### Scenario: Manager removes an <Entity>
* **Given** I am prompted to select an <entity> for removal
* **When** I select the <entity> I wish to remove
* **Then** That <entity> is removed from the <parent> and the database

### US-N.3 - Edit <Entity>
#### Scenario: Manager changes an <Entity>'s <information>
* **Given** I am prompted to select an <entity> and enter new <information>
* **When** I select an <entity> in the <parent>'s <entity> list
* **And** enter new <information> for the <entity>
* **Then** The <entity>'s new <information> is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see <entity> information  |
| **Write scope** | Only logged in Company Managers can edit or remove <information> of an <entity> if the <entity> exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create <entity>s |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/<entity>/read` | Yes | Read an <entity>'s information |
| `POST` | `/<entity>/edit` | Yes | Change an <entity>'s information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "name": "John Doe",
  "title": "example",
  "emal": "jdoe@example.com",
  "status": "chilling"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays <entity> <information>

### [View: Edit Page] — route name `edit`
*   Fields: <information>
*   Primary action: **Edit <Entity>**.
*   Buttons to save or cancel editing of <entity>
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