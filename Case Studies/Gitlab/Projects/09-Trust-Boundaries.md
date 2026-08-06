# Trust Boundaries

## Introduction

A trust boundary is a point where GitLab must decide whether an actor, request, resource, or external system can be trusted to perform a particular operation.

Whenever information crosses a trust boundary, the application should validate identity, permissions, resource ownership, and business rules before allowing the requested operation.

From an application security perspective, trust boundaries are where authorization failures, business logic flaws, and privilege escalation vulnerabilities commonly occur.

---

# Trust Boundary Overview

```text
          User
            │
            ▼
 Authentication
            │
            ▼
 Authorization
            │
            ▼
 GitLab Project
            │
    ┌───────┼────────┐
    │       │        │
Repository Members CI/CD
    │
    ▼
External Integrations
```

Every transition between these components represents a trust boundary that requires validation.

---

# TB-001 User → GitLab

Description

A user submits a request to GitLab.

Trust Decision

- Is the user authenticated?
- Is the session valid?
- Is the request genuine?

Security Controls

- Authentication
- Session validation
- CSRF protection (where applicable)

---

# TB-002 User → Project

Description

A user attempts to access a Project.

Trust Decision

- Does the Project exist?
- Is the Project visible?
- Is the user authorized?

Security Controls

- Visibility enforcement
- Membership evaluation
- Role validation

---

# TB-003 User → Project Resource

Examples

- Repository
- Issues
- Merge Requests
- Wiki
- Packages

Trust Decision

- Does this resource belong to the requested Project?
- Is the actor permitted to access it?

Security Controls

- Resource ownership validation
- Project authorization
- Permission checks

---

# TB-004 Project → Namespace

Description

Projects exist within a Namespace.

Trust Decision

- Does the Namespace own this Project?
- Is the Project operating within the correct Namespace?

Security Controls

- Namespace ownership validation
- Project relationship verification

---

# TB-005 Project → CI/CD

Description

A Project initiates CI/CD execution.

Trust Decision

- Is the pipeline authorized?
- Is the runner trusted?
- Can this pipeline access protected resources?

Security Controls

- Pipeline authorization
- Runner validation
- Protected branch rules

---

# TB-006 Project → External Integrations

Examples

- Webhooks
- Jira
- Slack
- Kubernetes

Trust Decision

- Is the integration trusted?
- Can data be exchanged?
- Is the request authentic?

Security Controls

- Authentication
- Secret validation
- Webhook verification

---

# TB-007 Project → Background Jobs

Description

GitLab executes asynchronous tasks on behalf of a Project.

Examples

- Import
- Export
- Notifications
- Cleanup
- Scheduled processing

Trust Decision

- Was the job initiated by an authorized workflow?
- Does the job still have permission to operate?

Security Controls

- Authorization context
- Job validation
- Audit logging

---

# Trust Boundary Summary

| Boundary | Trust Decision |
|----------|----------------|
| User → GitLab | Authenticate identity |
| User → Project | Verify authorization |
| User → Resource | Verify ownership and permissions |
| Project → Namespace | Verify ownership relationship |
| Project → CI/CD | Verify execution permissions |
| Project → External Services | Verify trusted integration |
| Project → Background Jobs | Verify delegated authority |

---

# Security Perspective

Every trust boundary should answer four questions:

1. Who is making the request?
2. What resource is being accessed?
3. Is the action authorized?
4. Has the integrity of the request been preserved?

Failure to enforce these checks consistently can lead to authorization bypasses, privilege escalation, business logic flaws, and data exposure.

---

# Researcher's Notes

## Observation 1

Most Project workflows cross multiple trust boundaries rather than only one.

## Observation 2

Authorization should be evaluated whenever a request crosses into a new Project or resource boundary.

## Observation 3

External integrations and automated systems should be treated as separate actors with independent trust assumptions.

---

# Key Takeaways

- Trust boundaries define where GitLab evaluates trust.
- Every boundary should perform authentication, authorization, and validation.
- Crossing a trust boundary without appropriate checks may compromise Project security.
- Mapping trust boundaries helps identify where security testing should focus.
