# Business Rules

## Introduction

Business rules define the constraints and requirements that GitLab must enforce to ensure Projects operate correctly. These rules protect the integrity of the software development process, maintain proper authorization, preserve data consistency, and support collaboration between users.

From an application security perspective, every business rule represents an assumption that the application relies upon. If a rule can be bypassed or violated, the application may become vulnerable to authorization flaws, business logic vulnerabilities, race conditions, or inconsistent system states.

---

# Project Creation Rules

## BR-001

**Only authorized users may create a Project.**

Reason

Project creation changes persistent system state and consumes platform resources.

Security Impact

Creating Projects without authorization could allow resource abuse or unauthorized collaboration.

---

## BR-002

**Every Project must belong to exactly one Namespace.**

Reason

Namespaces establish ownership and organizational boundaries.

Security Impact

Projects without valid ownership would create authorization ambiguity.

---

## BR-003

**The Project must have a valid name.**

Reason

The Project name identifies the Project to users.

Security Impact

Invalid or conflicting names may create confusion or interfere with resource identification.

---

## BR-004

**The Project path (slug) must be unique within its Namespace.**

Reason

Projects are addressed through URLs derived from their path.

Security Impact

Duplicate paths could cause routing conflicts or incorrect resource resolution.

---

## BR-005

**The selected visibility level must comply with namespace and instance policies.**

Reason

Visibility determines who may discover and access the Project.

Security Impact

Incorrect visibility could expose confidential repositories or unintentionally restrict legitimate access.

---

# Ownership Rules

## BR-006

**Every Project must have an owner or controlling namespace.**

Reason

Administrative responsibility must always exist.

Security Impact

Orphaned Projects create uncertainty around authorization and management.

---

## BR-007

**Project ownership changes must be authorized.**

Reason

Ownership transfers affect administrative control.

Security Impact

Unauthorized transfers could result in privilege escalation or resource theft.

---

# Membership Rules

## BR-008

**Only authorized users may manage Project membership.**

Reason

Membership determines access to Project resources.

Security Impact

Improper membership management may grant unauthorized access.

---

## BR-009

**Each Project Member must have exactly one effective role for authorization decisions.**

Reason

GitLab evaluates permissions using role assignments and inherited access.

Security Impact

Incorrect role evaluation may result in excessive or insufficient privileges.

---

# Repository Rules

## BR-010

**Repository operations must occur within the context of the owning Project.**

Reason

Repositories are Project resources.

Security Impact

Cross-project repository access would violate Project isolation.

---

# Visibility Rules

## BR-011

**Users may only access Projects permitted by the configured visibility level and their authorization.**

Reason

Visibility controls information disclosure.

Security Impact

Visibility bypasses could expose confidential project information.

---

# Lifecycle Rules

## BR-012

**Archived Projects should restrict modification while preserving historical data.**

Reason

Archiving transitions a Project into a protected operational state.

Security Impact

Allowing modifications to archived Projects may violate expected workflow behavior.

---

## BR-013

**Project deletion must require appropriate authorization.**

Reason

Deletion permanently affects project resources.

Security Impact

Unauthorized deletion could result in data loss or denial of service.

---

# Cross-Cutting Rules

## BR-014

**Authorization must be evaluated before performing security-sensitive operations.**

Reason

Operations should only be executed by authorized actors.

---

## BR-015

**Every security-sensitive action should operate on the intended Project.**

Reason

Project identifiers must correctly reference the target resource.

---

## BR-016

**Project state transitions must follow the defined lifecycle.**

Reason

Projects should only move between valid operational states.

---

# Researcher's Notes

## Observation 1

Many business rules are enforced before a Project is created. This makes the Project Creation workflow one of the richest sources of validation logic.

---

## Observation 2

Authorization is not a single rule. It appears repeatedly across creation, membership, visibility, settings, transfers, archiving, and deletion.

---

## Observation 3

Several business rules depend on shared state for example, project ownership, membership, namespace configuration, and visibility settings. These shared states should be analyzed later for race conditions and consistency issues.

---

# Key Takeaways

- Business rules define how GitLab Projects are expected to behave.
- Security controls exist to enforce business rules.
- Violating a business rule may lead to authorization flaws, business logic vulnerabilities, or inconsistent application state.
- Business rules provide the foundation for deriving invariants and designing security test cases.
