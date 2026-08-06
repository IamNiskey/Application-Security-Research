# Attack Surface Modeling

## Introduction

Attack surface modeling is the process of systematically identifying every business capability, interface, workflow, and architectural component through which an actor can influence the behavior of an application.

Rather than viewing the attack surface as a collection of URLs or API endpoints, this methodology treats it as the set of all reachable business capabilities, protected resources, trust boundaries, and state-changing operations.

The objective is to understand how the application can be interacted with before determining how it can be abused.

---

# Attack Surface Modeling Pipeline

```text
Business Domains
        │
        ▼
Business Capabilities
        │
        ▼
Business Objects
        │
        ▼
Actors
        │
        ▼
Interfaces
        │
        ▼
Workflows
        │
        ▼
Trust Boundaries
        │
        ▼
State Changes
        │
        ▼
Security Tests
```

---

# Step 1 — Identify Business Domains

Begin by identifying the major domains of the application.

Examples

- Authentication
- Organizations
- Projects
- Billing
- Messaging
- Administration

Deliverable

Business domain inventory.

---

# Step 2 — Identify Business Capabilities

Each domain exposes one or more capabilities.

Example

Projects

- Create
- Update
- Archive
- Transfer
- Delete
- Invite Members
- Change Visibility

Capabilities—not endpoints—form the primary attack surface.

Deliverable

Capability inventory.

---

# Step 3 — Identify Business Objects

Determine which objects each capability affects.

Example

Project

- Repository
- Members
- Issues
- Pipelines
- Variables

Questions

- What object changes?
- Who owns it?
- What depends on it?

Deliverable

Object inventory.

---

# Step 4 — Identify Interfaces

Determine how each capability is exposed.

Examples

- Web UI
- REST API
- GraphQL API
- Git Protocol
- Webhooks
- Background Jobs
- Scheduled Tasks

Every interface represents an independent attack surface.

Deliverable

Interface inventory.

---

# Step 5 — Identify Actors

Determine who can interact with each capability.

Examples

- Anonymous User
- Authenticated User
- Administrator
- Project Member
- External Integration
- Automated Process

Questions

- Who initiates the operation?
- Who approves it?
- Who receives the result?

Deliverable

Actor matrix.

---

# Step 6 — Identify State-Changing Operations

Not every operation changes system state.

Focus on operations that:

- Create objects
- Modify objects
- Delete objects
- Transfer ownership
- Change permissions
- Trigger background processing

These operations deserve additional security analysis.

Deliverable

State-change inventory.

---

# Step 7 — Identify Shared State

Determine whether multiple workflows modify the same object.

Example

Project Membership

- Invite User
- Remove User
- Change Role
- Accept Invitation

Because these workflows modify shared state, they are strong candidates for race conditions and business logic flaws.

Deliverable

Shared state map.

---

# Step 8 — Identify Trust Boundaries

Determine where each workflow crosses a trust boundary.

Examples

- User → Application
- Application → Database
- Project → Namespace
- Application → External Service

Every boundary crossing introduces new security assumptions.

Deliverable

Boundary map.

---

# Attack Surface Classification

Classify every attack surface according to its purpose.

## Identity

Examples

- Login
- Session
- OAuth
- API Tokens

---

## Resource Management

Examples

- Projects
- Repositories
- Organizations
- Files

---

## Administration

Examples

- Settings
- User Management
- Permissions
- Audit Logs

---

## Communication

Examples

- Notifications
- Email
- Webhooks
- Integrations

---

## Automation

Examples

- Background Jobs
- CI/CD
- Scheduled Tasks
- Imports
- Exports

---

## Data Exchange

Examples

- REST APIs
- GraphQL
- File Uploads
- Imports
- Exports

---

# Security Perspective

For every attack surface ask:

- What business capability is exposed?
- Which business object is affected?
- Which actors can access it?
- Which trust boundaries are crossed?
- Does it change system state?
- Does it modify shared state?
- Which business rules apply?
- Which invariants must remain true?

The answers to these questions define the security testing strategy.

---

# Researcher's Notes

## Observation 1

Business capabilities are more stable than endpoints and remain useful even when the implementation changes.

## Observation 2

Attack surfaces that modify shared state generally present higher security risk than read-only operations.

## Observation 3

Many critical vulnerabilities arise from interactions between attack surfaces rather than from individual features.

---

# Attack Surface Checklist

Before testing, verify:

- Business domains identified.
- Capabilities documented.
- Objects mapped.
- Interfaces enumerated.
- Actors identified.
- State-changing operations located.
- Shared state documented.
- Trust boundaries identified.

---

# Key Takeaways

- Model attack surfaces from architecture rather than URLs.
- Focus on business capabilities instead of implementation details.
- Prioritize state-changing operations and shared state.
- Every attack surface should be traceable to business objectives, trust boundaries, and architectural assumptions.
