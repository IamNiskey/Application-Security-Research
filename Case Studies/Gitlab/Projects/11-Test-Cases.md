# Security Test Cases

## Introduction

This document defines security test cases for the GitLab Project feature. Each test case is derived from the architectural analysis performed throughout this case study rather than from a generic vulnerability checklist.

The objective is to verify that GitLab consistently enforces its business rules, preserves its invariants, validates state transitions, and protects trust boundaries.

---

# Authorization

## TC-001 Project Creation Authorization

Objective

Verify that only authorized users can create Projects.

Related Business Rule

BR-001

Test Ideas

- Attempt Project creation as an unauthenticated user.
- Attempt Project creation using insufficient privileges.
- Verify API and UI enforce identical authorization.

Expected Result

Unauthorized requests are rejected.

---

## TC-002 Project Settings Authorization

Objective

Verify only authorized users can modify Project settings.

Related Rules

BR-008

BR-014

Test Ideas

- Modify settings as Guest.
- Modify settings as Reporter.
- Modify settings through the API.
- Attempt direct endpoint access.

Expected Result

Only authorized roles may modify settings.

---

## TC-003 Membership Management

Objective

Verify membership changes require proper authorization.

Related Rules

BR-008

INV-006

Test Ideas

- Add members without permission.
- Remove privileged users.
- Change member roles.
- Test inherited memberships.
- Test shared group memberships.

Expected Result

Unauthorized membership changes are rejected.

---

# Resource Isolation

## TC-004 Cross-Project Repository Access

Objective

Verify repositories remain isolated.

Related Invariant

INV-008

Test Ideas

- Replace Project identifiers.
- Attempt cross-project cloning.
- Access repository objects directly.

Expected Result

Repository isolation is preserved.

---

## TC-005 Cross-Project Resource Access

Resources

- Issues
- Merge Requests
- Packages
- Releases
- Pipelines

Objective

Verify child resources cannot escape their Project boundary.

Related Invariants

INV-009

INV-010

INV-014

Expected Result

Resources remain bound to their owning Project.

---

# State Machine

## TC-006 Archive State Enforcement

Objective

Verify archived Projects become read-only where expected.

Related State

Archived

Test Ideas

- Push commits.
- Create issues.
- Modify settings.
- Trigger pipelines.
- Upload packages.

Expected Result

Write operations are rejected according to the archived state.

---

## TC-007 Invalid State Transitions

Objective

Verify invalid lifecycle transitions cannot occur.

Examples

- Deleted → Active
- Deleted → Archived
- Pending Deletion → Archived

Expected Result

Only valid transitions are accepted.

---

# Namespace Integrity

## TC-008 Namespace Validation

Objective

Verify Projects remain associated with a valid Namespace.

Related Invariants

INV-001

INV-002

Test Ideas

- Attempt unauthorized transfer.
- Modify namespace identifiers.
- Replay transfer requests.
- Test concurrent namespace operations.

Expected Result

Namespace integrity is preserved.

---

# Visibility

## TC-009 Visibility Enforcement

Objective

Verify Project visibility controls are consistently enforced.

Test Ideas

- Switch visibility levels.
- Test direct URLs.
- Test API responses.
- Test cached content.
- Test search indexing behavior.

Expected Result

Visibility restrictions are consistently applied.

---

# API Consistency

## TC-010 UI vs API Authorization

Objective

Verify identical authorization decisions across interfaces.

Test Ideas

- Perform identical operations through the UI and REST API.
- Compare responses.
- Verify permission consistency.

Expected Result

Authorization behavior is identical across interfaces. :contentReference[oaicite:0]{index=0}

---

# Trust Boundaries

## TC-011 Project Resource Ownership

Objective

Verify Project resources cannot be accessed outside their security boundary.

Test Ideas

- Replace object identifiers.
- Replay requests against another Project.
- Test nested resources.
- Test resource references.

Expected Result

Ownership validation prevents cross-Project access.

---

## TC-012 External Integrations

Objective

Verify external systems cannot perform unauthorized actions.

Test Ideas

- Replay webhook requests.
- Remove authentication.
- Modify signatures.
- Reuse old requests.

Expected Result

Only trusted integrations are accepted.

---

# Race Conditions

## TC-013 Membership Race

Objective

Determine whether authorization changes race with membership updates.

Test Ideas

- Remove a member while privileged requests are executing.
- Change roles during concurrent requests.
- Execute multiple membership updates simultaneously.

Expected Result

Authorization decisions remain consistent.

---

## TC-014 Visibility Race

Objective

Verify visibility changes are atomic.

Test Ideas

- Toggle Project visibility while requesting protected resources.
- Execute concurrent read requests.
- Observe cache consistency.

Expected Result

No unauthorized access occurs during state changes.

---

## TC-015 Project Lifecycle Race

Objective

Verify lifecycle transitions cannot be exploited through concurrent execution.

Test Ideas

- Archive while pushing commits.
- Delete while modifying settings.
- Restore while removing members.
- Archive during pipeline execution.

Expected Result

State transitions remain consistent under concurrent operations.

---

# Security Perspective

Each test case should evaluate:

- Authentication
- Authorization
- Business Rule enforcement
- Invariant preservation
- State transition validation
- Trust boundary protection
- Shared state consistency

Successful testing demonstrates that GitLab consistently enforces the architectural assumptions identified throughout this case study.

---

# Researcher's Notes

## Observation 1

Every test case traces back to one or more business rules or invariants rather than arbitrary endpoints.

## Observation 2

High-impact vulnerabilities frequently arise where multiple workflows operate on shared Project state.

## Observation 3

The most valuable tests are those that validate the consistency of authorization, state transitions, and resource ownership across all interfaces.

---

# Key Takeaways

- Security testing should validate architecture, not just endpoints.
- Every test case should map to a business rule or invariant.
- Shared state and workflow interactions deserve the highest testing priority.
- A structured methodology produces repeatable and comprehensive security assessments.
