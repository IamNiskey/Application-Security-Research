# Research Process

## Introduction

Application security research should begin by understanding how an application is designed to function before attempting to identify vulnerabilities.

This methodology treats vulnerability discovery as the result of systematic architectural analysis rather than random testing. Every stage builds upon knowledge gathered during the previous stage, creating a repeatable and evidence-driven research process.

---

# Research Workflow

```text
Target Selection
        │
        ▼
Information Collection
        │
        ▼
System Decomposition
        │
        ▼
Architecture Discovery
        │
        ▼
Actor Identification
        │
        ▼
Feature Enumeration
        │
        ▼
Workflow Modeling
        │
        ▼
Business Rule Extraction
        │
        ▼
Invariant Identification
        │
        ▼
State Machine Modeling
        │
        ▼
Trust Boundary Analysis
        │
        ▼
Attack Surface Modeling
        │
        ▼
Security Test Case Derivation
        │
        ▼
Security Testing
        │
        ▼
Reporting
```

---

# Phase 1 — Target Selection

## Objective

Choose an application or feature that will be analyzed.

Selection Criteria

- Clearly defined functionality.
- Publicly accessible documentation.
- Multiple user roles.
- Complex workflows.
- High-value business operations.
- Active development.

Deliverables

- Target identified.
- Research scope defined.
- Initial assumptions documented.

---

# Phase 2 — Information Collection

## Objective

Collect information from authoritative sources before interacting with the application.

Sources

- Official documentation
- API documentation
- Product guides
- Release notes
- Public presentations
- Engineering blogs
- RFCs and standards

Deliverables

- Documentation inventory.
- Terminology glossary.
- Feature inventory.

---

# Phase 3 — System Decomposition

## Objective

Break the application into manageable components.

Examples

- Authentication
- Organizations
- Projects
- Billing
- Notifications
- Search
- Administration

Deliverables

- System map.
- Component inventory.
- Research priorities.

---

# Phase 4 — Architecture Discovery

## Objective

Understand how the selected component is structured.

Questions

- What objects exist?
- How are they related?
- What responsibilities does each object have?
- Which objects own other resources?

Deliverables

- Object model.
- Relationship diagrams.
- Architecture overview.

---

# Phase 5 — Behavioral Analysis

## Objective

Understand how the application behaves.

Activities

- Identify actors.
- Enumerate features.
- Model workflows.
- Extract business rules.
- Identify invariants.
- Build state machines.

Deliverables

- Workflow diagrams.
- Business rules.
- Invariants.
- State models.

---

# Phase 6 — Security Modeling

## Objective

Translate architectural understanding into security analysis.

Activities

- Identify trust boundaries.
- Map attack surfaces.
- Analyze authorization.
- Identify shared state.
- Locate decision points.

Deliverables

- Trust boundary diagrams.
- Attack surface inventory.
- Security assumptions.

---

# Phase 7 — Test Case Derivation

## Objective

Design security tests directly from the architecture.

Every test should answer one of the following questions:

- Can a business rule be violated?
- Can an invariant be broken?
- Can a state transition be bypassed?
- Can trust be abused?
- Can authorization be circumvented?
- Can shared state become inconsistent?

Deliverables

- Structured test cases.
- Testing priorities.
- Risk assessment.

---

# Phase 8 — Security Testing

## Objective

Validate architectural assumptions through controlled testing.

Testing Areas

- Authentication
- Authorization
- Business Logic
- Race Conditions
- State Transitions
- Input Validation
- API Consistency
- Workflow Integrity

Deliverables

- Verified findings.
- Reproduced vulnerabilities.
- Supporting evidence.

---

# Phase 9 — Reporting

## Objective

Document the research in a reusable format.

Documentation Should Include

- System overview.
- Research methodology.
- Findings.
- Evidence.
- Root cause analysis.
- Recommendations.

Deliverables

- Case study.
- Technical report.
- Reusable knowledge.

---

# Guiding Principles

- Understand before testing.
- Test architecture, not just endpoints.
- Validate assumptions with evidence.
- Trace every test back to a business objective.
- Document every conclusion.
- Prefer repeatable methodology over intuition.

---

# Researcher's Notes

## Observation 1

Understanding the application's design dramatically reduces unnecessary testing by focusing effort on meaningful workflows.

## Observation 2

Every phase produces artifacts that become inputs for the next phase, ensuring the research remains structured and reproducible.

## Observation 3

Vulnerability discovery is the outcome of understanding the system—not the starting point of the research process.

---

# Key Takeaways

- Application security research is a structured process rather than a collection of isolated tests.
- Each phase builds on evidence gathered in previous phases.
- Architectural understanding leads to higher-quality security testing.
- A repeatable methodology produces consistent and reusable research.
