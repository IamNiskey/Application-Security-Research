# Invariants

## Introduction

Invariants are properties of a system that must remain true regardless of the workflow being executed. Unlike business rules, which govern how users interact with the application, invariants define the fundamental truths that preserve the consistency and integrity of GitLab Projects.

Every workflow—whether creating a project, adding members, transferring ownership, changing visibility, or deleting a project—must preserve these invariants.

From an application security perspective, violations of invariants often indicate authorization flaws, business logic vulnerabilities, race conditions, or data integrity issues.

---

# Namespace Invariants

## INV-001

### Every Project belongs to exactly one Namespace.

Rationale

Namespaces establish ownership, organization, and administrative boundaries.

Violation Example

A Project simultaneously belongs to multiple namespaces.

Security Impact

Authorization ambiguity.

Broken ownership model.

Potential privilege escalation.

---

## INV-002

### Every Namespace maintains independent Project organization.

Rationale

Projects in different namespaces remain logically isolated.

Security Impact

Cross-namespace access should never occur without an explicit transfer or sharing mechanism.

---

# Identity Invariants

## INV-003

### Every Project has exactly one unique identifier.

Rationale

Projects must always be uniquely identifiable.

Security Impact

Incorrect resource resolution.

Broken references.

Authorization inconsistencies.

---

## INV-004

### Every Project has one canonical path within its Namespace.

Rationale

Project URLs depend on namespace and project path.

Security Impact

Duplicate paths may cause routing ambiguity.

---

# Ownership Invariants

## INV-005

### Every Project always has a responsible owner or controlling namespace.

Rationale

Administrative responsibility must never disappear.

Security Impact

Orphaned Projects create undefined authorization behavior.

---

# Membership Invariants

## INV-006

### Every effective Project permission must be derived from a valid authorization source.

Examples

- Direct membership
- Group membership
- Shared group membership
- Administrator privileges

Security Impact

Permissions should never exist without a legitimate origin.

---

## INV-007

### Authorization decisions must always reflect the user's effective permissions.

Rationale

Permission evaluation should be deterministic.

Security Impact

Incorrect evaluation may result in privilege escalation.

---

# Resource Invariants

## INV-008

### Every repository belongs to exactly one Project.

Rationale

Repositories are Project resources.

Security Impact

Repository isolation must always be preserved.

---

## INV-009

### Every Issue belongs to exactly one Project.

Rationale

Issues inherit Project ownership and permissions.

Security Impact

Cross-project issue access violates resource isolation.

---

## INV-010

### Every Merge Request belongs to a valid Project context.

Rationale

Merge Requests operate within Projects.

Security Impact

Broken project association creates authorization ambiguity.

---

# Visibility Invariants

## INV-011

### Project visibility must always remain internally consistent.

Examples

Public.

Internal.

Private.

Security Impact

Visibility inconsistencies may expose confidential resources.

---

# Lifecycle Invariants

## INV-012

### Every Project exists in exactly one lifecycle state.

Examples

- Active
- Archived
- Pending Deletion
- Deleted

Security Impact

Projects should never exist in conflicting operational states simultaneously.

---

## INV-013

### State transitions preserve Project integrity.

Rationale

Changing state must never corrupt project resources.

---

# Integrity Invariants

## INV-014

### Child resources inherit the Project security boundary.

Examples

Repository

Issues

Merge Requests

Packages

Pipelines

Variables

Wiki

Security Impact

Child resources should never become detached from Project authorization.

---

## INV-015

### Authorization is evaluated within the Project context.

Rationale

Project membership defines access to Project resources.

Security Impact

Authorization bypasses may violate Project isolation.

---

# Researcher's Notes

## Observation 1

Many GitLab workflows modify Project state but should never modify these invariants.

---

## Observation 2

Business rules can change over time.

Invariants should remain stable across product versions because they define the architecture rather than individual workflows.

---

## Observation 3

Most severe application logic flaws occur when an attacker causes the application to violate an invariant while still passing business rule validation.

---

# Key Takeaways

- Invariants define truths that must always remain valid.
- Business rules govern behavior; invariants preserve architecture.
- Every workflow must maintain these invariants.
- Violating an invariant often indicates a serious application logic flaw.
