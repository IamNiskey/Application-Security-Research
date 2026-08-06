# Test Case Derivation

## Introduction

Security testing should be a logical consequence of understanding an application's architecture rather than a collection of memorized vulnerability checks.

This methodology derives every security test from architectural artifacts created during research. Each test should trace back to one or more business objectives, business rules, invariants, state transitions, trust boundaries, or attack surfaces.

The result is a repeatable, explainable, and comprehensive testing methodology.

---

# Test Case Derivation Pipeline

```text
Business Objectives
        │
        ▼
Business Rules
        │
        ▼
Invariants
        │
        ▼
State Machine
        │
        ▼
Trust Boundaries
        │
        ▼
Attack Surface
        │
        ▼
Security Test Cases
        │
        ▼
Evidence Collection
```

---

# Step 1 — Derive Tests from Business Rules

Business rules define how the application should behave.

Ask:

- Can this rule be bypassed?
- Can this rule be executed out of order?
- Is this rule enforced everywhere?
- Is this rule enforced consistently?

Example

Business Rule

Only Project Maintainers may archive a Project.

Derived Tests

- Archive as a Developer.
- Archive through the API.
- Archive using a stale session.
- Archive through concurrent requests.

Deliverable

Business rule test catalogue.

---

# Step 2 — Derive Tests from Invariants

Invariants describe properties that must always remain true.

Ask:

- Can this invariant be violated?
- Can two workflows break this invariant?
- Can concurrent execution create an invalid state?

Example

Invariant

Every Project belongs to exactly one Namespace.

Derived Tests

- Transfer while deleting.
- Transfer concurrently.
- Modify namespace references.
- Replay transfer requests.

Deliverable

Invariant validation tests.

---

# Step 3 — Derive Tests from State Models

Every transition represents a security testing opportunity.

Ask:

- Can an invalid transition occur?
- Can a transition be skipped?
- Can two transitions execute simultaneously?
- Can a transition be replayed?

Example

Archived → Active

Derived Tests

- Restore without authorization.
- Restore twice.
- Restore while deleting.
- Restore using expired credentials.

Deliverable

State transition test suite.

---

# Step 4 — Derive Tests from Trust Boundaries

Every trust decision should be challenged.

Ask:

- Can identity be spoofed?
- Can authorization be inherited incorrectly?
- Can ownership be confused?
- Can trust become stale?

Examples

- User → Project
- API → Database
- Application → External Service

Deliverable

Trust boundary validation tests.

---

# Step 5 — Derive Tests from Attack Surfaces

Every business capability should generate security tests.

Example

Capability

Invite Member

Derived Tests

- Invite without permission.
- Invite concurrently.
- Invite existing users repeatedly.
- Invite using manipulated identifiers.
- Replay invitation requests.

Deliverable

Capability-based test catalogue.

---

# Step 6 — Derive Interaction Tests

Many vulnerabilities emerge when multiple workflows interact.

Examples

Membership + Visibility

Archive + Repository Push

Transfer + CI/CD

Delete + Background Job

Permission Change + Active Session

Questions

- Do both workflows modify shared state?
- Can they execute concurrently?
- Does one invalidate assumptions made by the other?

Deliverable

Workflow interaction tests.

---

# Step 7 — Derive Negative Tests

Every valid workflow has one or more invalid variations.

Examples

Valid

User creates Project.

Negative

Unauthenticated user creates Project.

Valid

Owner transfers Project.

Negative

Guest transfers Project.

Negative testing verifies that incorrect behavior is consistently rejected.

Deliverable

Negative test catalogue.

---

# Step 8 — Prioritize Testing

Not every test has equal value.

Suggested priority:

High

- Authorization
- Shared state
- Ownership
- State transitions
- Privilege changes

Medium

- Validation
- Business workflow consistency
- Resource lifecycle

Lower

- Cosmetic validation
- Non-security settings
- Read-only operations

Deliverable

Prioritized testing plan.

---

# Traceability Matrix

Every security test should be traceable.

| Test Case | Derived From |
|-----------|--------------|
| Authorization Test | Business Rule |
| Integrity Test | Invariant |
| Transition Test | State Machine |
| Boundary Test | Trust Boundary |
| Workflow Test | Attack Surface |
| Interaction Test | Shared State |
| Negative Test | Business Workflow |

---

# Security Perspective

Well-designed security tests answer questions such as:

- Can business rules be bypassed?
- Can invariants be violated?
- Can invalid state transitions occur?
- Can trust assumptions fail?
- Can ownership change unexpectedly?
- Can concurrent workflows create inconsistent state?
- Can one workflow interfere with another?

Each answer increases confidence in the application's security posture.

---

# Researcher's Notes

## Observation 1

Every architectural artifact should produce one or more security tests.

## Observation 2

The highest-value tests usually involve authorization, state transitions, ownership changes, and shared state.

## Observation 3

Interaction testing often reveals vulnerabilities that isolated feature testing cannot detect.

---

# Test Case Checklist

Before beginning security testing, verify that tests exist for:

- Business rules.
- Invariants.
- State transitions.
- Trust boundaries.
- Attack surfaces.
- Workflow interactions.
- Shared state.
- Negative scenarios.

---

# Key Takeaways

- Security tests should be derived, not invented.
- Every test should trace back to an architectural assumption.
- Interaction testing is as important as feature testing.
- A traceable methodology produces repeatable, explainable, and comprehensive security assessments.
