# State Machine

## Introduction

A state machine models the lifecycle of a GitLab Project by defining the valid operational states and the transitions between them.

Every state transition should occur only after the appropriate business rules, authorization checks, and validation logic have been satisfied.

From an application security perspective, state machines help identify:

- Invalid state transitions
- Missing authorization checks
- Workflow bypasses
- Race conditions
- Hidden substates
- TOCTOU vulnerabilities

---

# Project Lifecycle

```text
                Create Project
                     │
                     ▼
                +-----------+
                |  Active   |
                +-----------+
                 │    │
     Archive      │    │ Delete
                 ▼    ▼
          +-------------+
          | Archived    |
          +-------------+
                 │
          Unarchive
                 │
                 ▼
             +---------+
             | Active  |
             +---------+

Delete
   │
   ▼
+----------------------+
| Pending Deletion     |
+----------------------+
        │
   Restore │ Delete Permanently
        │
        ▼
     Active

             ▼
        +-----------+
        | Deleted   |
        +-----------+
```

---

# State Definitions

## State 1 — Active

Description

The Project is operational and available for normal use.

Typical Operations

- Push code
- Create branches
- Create issues
- Create merge requests
- Run CI/CD pipelines
- Manage members
- Update settings

---

## State 2 — Archived

Description

The Project is preserved for reference and becomes read-only for most operations.

Typical Characteristics

- Repository becomes read-only.
- Issues become read-only.
- Merge Requests become read-only.
- Scheduled pipelines stop running.
- Historical information is preserved.

Allowed Transition

Archived → Active (Unarchive)

---

## State 3 — Pending Deletion

Description

The Project has been scheduled for deletion but has not yet been permanently removed.

Typical Characteristics

- Awaiting permanent deletion.
- Can be restored before final removal.
- Administrative actions are limited.

Allowed Transitions

Pending Deletion → Active

Pending Deletion → Deleted

---

## State 4 — Deleted

Description

The Project has been permanently removed.

Characteristics

- Resources are no longer available.
- No further state transitions are possible.

---

# Valid State Transitions

| Current State | Allowed Transition |
|---------------|-------------------|
| Active | Archived |
| Active | Pending Deletion |
| Archived | Active |
| Pending Deletion | Active |
| Pending Deletion | Deleted |

---

# Invalid State Transitions

Examples

- Deleted → Active
- Deleted → Archived
- Archived → Deleted (without the required deletion workflow)
- Pending Deletion → Archived

Each invalid transition should be rejected by the application.

---

# Security Perspective

Every state transition should enforce:

- Authentication
- Authorization
- Resource existence
- Current state validation
- Audit logging
- Business rule validation

If the application allows an invalid transition, it may indicate an application logic flaw.

---

# Researcher's Notes

## Observation 1

State transitions modify shared project state and should be evaluated for race conditions.

## Observation 2

The application must verify the current state before executing a transition. Otherwise, users may bypass workflow restrictions.

## Observation 3

Archived Projects remain accessible but become read-only for most operations. This creates opportunities to verify that write operations are consistently blocked across all project features.

---

# Key Takeaways

- A GitLab Project progresses through a defined lifecycle.
- Only specific state transitions are valid.
- Every transition requires validation and authorization.
- Invalid transitions may reveal application logic vulnerabilities.
