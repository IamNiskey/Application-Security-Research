# State Modeling

## Introduction

State modeling is the process of identifying how a business object changes over time.

Every significant object within an application progresses through one or more states. Users, workflows, and system events cause transitions between these states.

Understanding these transitions allows security researchers to identify invalid state changes, race conditions, workflow bypasses, and violations of business logic.

---

# Why State Modeling?

Applications are not static.

Every business object changes over time.

Examples include:

- User Account
- Project
- Repository
- Payment
- Order
- Subscription
- Support Ticket

Each object follows a lifecycle that defines what operations are valid at any point in time.

---

# State Modeling Pipeline

```text
Business Object
        │
        ▼
Identify States
        │
        ▼
Identify Events
        │
        ▼
Identify Transitions
        │
        ▼
Identify Guards
        │
        ▼
Identify Actions
        │
        ▼
Validate State Machine
        │
        ▼
Derive Security Tests
```

---

# Step 1 — Identify the Business Object

Begin by selecting a single object.

Examples

- Project
- Invoice
- Group
- Order
- Repository

Questions

- What is the object?
- What is its responsibility?
- Which workflows modify it?

Deliverable

Business object definition.

---

# Step 2 — Identify States

A state represents the condition of the object at a particular moment.

Example

Project

```
Draft

↓

Active

↓

Archived

↓

Pending Deletion

↓

Deleted
```

Questions

- What states exist?
- Are any states temporary?
- Are any states terminal?

Deliverable

State inventory.

---

# Step 3 — Identify Events

Events trigger transitions.

Examples

- Create
- Approve
- Archive
- Restore
- Delete
- Cancel
- Expire

Questions

- What causes a state change?
- Can the event originate from a user?
- Can the system trigger it automatically?

Deliverable

Event catalogue.

---

# Step 4 — Identify Transition Guards

A transition guard is a condition that must be true before a transition is allowed.

Examples

- User is authenticated.
- User is authorized.
- Payment completed.
- Project exists.
- Resource not locked.
- Feature enabled.

Questions

- What conditions control this transition?
- Which validations occur first?

Deliverable

Transition guard inventory.

---

# Step 5 — Identify Actions

Actions occur before, during, or after a successful transition.

Examples

- Update database.
- Send notification.
- Create audit log.
- Start background job.
- Trigger webhook.
- Update permissions.

Questions

- What changes as a result of the transition?
- Which resources are modified?

Deliverable

Action inventory.

---

# Step 6 — Validate the State Machine

Review every transition.

Questions

- Can every state be reached?
- Can every state be exited?
- Are invalid transitions rejected?
- Are terminal states enforced?
- Are hidden transitions present?

Deliverable

Validated state machine.

---

# Hidden States

Applications often contain hidden or internal states that are not visible in the user interface.

Examples

- Processing
- Pending Approval
- Awaiting Background Job
- Synchronizing
- Queued

These states frequently introduce race conditions and inconsistent behavior because users are unaware of them.

---

# Shared State

Multiple workflows may modify the same state.

Example

Project Membership

- Invite Member
- Remove Member
- Change Role
- Accept Invitation

All four workflows modify the same underlying membership state.

Shared state is a common source of:

- Race conditions
- TOCTOU vulnerabilities
- Business logic flaws

---

# Security Perspective

State modeling helps answer important security questions.

- Can an invalid transition occur?
- Can a guard condition be bypassed?
- Can two transitions execute simultaneously?
- Can an object exist in conflicting states?
- Can hidden states be manipulated?

Answering these questions often reveals architectural weaknesses that are invisible during endpoint-focused testing.

---

# Researcher's Notes

## Observation 1

Every transition should have clearly defined guard conditions.

## Observation 2

Hidden states are often richer sources of vulnerabilities than visible states.

## Observation 3

Objects modified by multiple workflows deserve additional attention because concurrent transitions may violate business assumptions.

---

# State Modeling Checklist

Before testing, verify:

- All states identified.
- All events documented.
- All transitions mapped.
- All guards identified.
- All actions documented.
- Hidden states investigated.
- Shared states identified.
- Invalid transitions listed.

---

# Key Takeaways

- Every business object has a lifecycle.
- States, transitions, guards, and actions define system behavior.
- Hidden and shared states are valuable security targets.
- State models provide the foundation for workflow and race condition testing.
