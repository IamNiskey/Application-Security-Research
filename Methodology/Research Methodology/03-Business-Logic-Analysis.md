# Business Logic Analysis

## Introduction

Business logic analysis is the process of understanding why an application behaves the way it does before attempting to identify security vulnerabilities.

Rather than focusing on implementation details such as endpoints or parameters, business logic analysis examines the application's objectives, workflows, assumptions, and constraints.

The goal is to understand what the application is trying to achieve so that security testing can verify whether those objectives are consistently enforced.

---

# Business Logic Pipeline

```text
Business Objective
        │
        ▼
Business Process
        │
        ▼
Actors
        │
        ▼
Features
        │
        ▼
Workflow
        │
        ▼
Decision Points
        │
        ▼
Business Rules
        │
        ▼
Invariants
        │
        ▼
Security Tests
```

Every stage provides context for the next.

---

# Step 1 — Identify the Business Objective

Ask:

- Why does this feature exist?
- What business problem does it solve?
- Who benefits from it?
- What outcome should it achieve?

Example

Feature

Project Creation

Business Objective

Enable users to create isolated workspaces for software development.

Deliverable

A clear statement describing the feature's purpose.

---

# Step 2 — Identify the Actors

Determine every entity that participates in the workflow.

Examples

- Anonymous User
- Authenticated User
- Administrator
- Project Member
- External Service
- Background Job

Questions

- Who starts the workflow?
- Who approves it?
- Who can modify it?
- Who observes it?

Deliverable

Actor inventory.

---

# Step 3 — Identify Features

Break the business objective into individual capabilities.

Example

Project

├── Repository

├── Members

├── Issues

├── Merge Requests

├── Pipelines

└── Settings

Each feature should have a clearly defined responsibility.

---

# Step 4 — Model the Workflow

Describe the sequence of actions required to complete the business objective.

Example

```text
Request

↓

Validation

↓

Authorization

↓

Business Processing

↓

State Update

↓

Audit Logging

↓

Response
```

Questions

- What happens first?
- What decisions are made?
- Which state changes?
- What happens if validation fails?

Deliverable

Workflow diagram.

---

# Step 5 — Identify Decision Points

Decision points are locations where the application evaluates one or more conditions before continuing.

Examples

- Is the user authenticated?
- Does the Project exist?
- Is the user authorized?
- Is the Project archived?
- Is the resource locked?

Every decision point should answer a clear business question.

Deliverable

Decision point inventory.

---

# Step 6 — Extract Business Rules

Business rules define how the workflow must behave.

Examples

- Only authorized users may modify Project settings.
- Every Project must belong to exactly one Namespace.
- Archived Projects should reject write operations.

Questions

- What must always be true?
- What actions are prohibited?
- What conditions must be satisfied?

Deliverable

Business rule catalogue.

---

# Step 7 — Identify Invariants

Invariants describe properties that remain true regardless of the workflow.

Examples

- Every Project belongs to one Namespace.
- Every repository belongs to one Project.
- Every authorization decision has a valid permission source.

Questions

- What architectural truths must never change?
- Which assumptions does every workflow depend on?

Deliverable

Invariant catalogue.

---

# Step 8 — Derive Security Tests

Every test should validate one architectural assumption.

Examples

Business Rule

↓

Authorization Test

Invariant

↓

Integrity Test

Decision Point

↓

Validation Test

Workflow

↓

Business Logic Test

State Transition

↓

State Machine Test

Deliverable

Traceable security test cases.

---

# Analysis Checklist

Before testing a feature, answer the following:

- What business objective does it satisfy?
- Who interacts with it?
- What capabilities does it expose?
- What workflows exist?
- Where are the decision points?
- What business rules are enforced?
- Which invariants must never change?
- What state transitions occur?
- What trust boundaries are crossed?
- What assumptions should be tested?

---

# Researcher's Notes

## Observation 1

Business logic vulnerabilities usually arise from incorrect assumptions rather than incorrect input validation.

## Observation 2

Understanding why a workflow exists is often more valuable than understanding how it is implemented.

## Observation 3

Every architectural assumption should be traceable to one or more security tests.

---

# Key Takeaways

- Business logic analysis begins with understanding business objectives.
- Every workflow should be decomposed into actors, decisions, rules, and invariants.
- Architectural assumptions provide the foundation for meaningful security testing.
- Security tests should validate business behavior rather than only technical implementation.
