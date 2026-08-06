# Trust Boundary Analysis

## Introduction

Trust boundary analysis is the process of identifying every location where an application must decide whether an actor, request, resource, or external system should be trusted.

Whenever data or control crosses a trust boundary, the application must validate identity, authorization, ownership, integrity, and business constraints before allowing the requested operation.

Many high-impact security vulnerabilities occur because an application incorrectly trusts an actor, object, or service.

---

# Trust Boundary Analysis Pipeline

```text
Business Workflow
        │
        ▼
Identify Actors
        │
        ▼
Identify Trust Zones
        │
        ▼
Identify Boundary Crossings
        │
        ▼
Identify Trust Decisions
        │
        ▼
Identify Security Controls
        │
        ▼
Derive Security Tests
```

---

# Step 1 — Identify Trust Zones

A trust zone is a collection of components that share the same level of trust.

Example

```
Internet

↓

Browser

↓

Application

↓

Database

↓

Third-Party Services
```

Questions

- Which components trust one another?
- Which components require independent validation?
- Where does trust change?

Deliverable

Trust zone diagram.

---

# Step 2 — Identify Actors

Determine every entity capable of crossing a trust boundary.

Examples

- Anonymous User
- Authenticated User
- Administrator
- Background Job
- CI/CD Runner
- External Integration
- API Client

Questions

- Who initiates the request?
- Who receives it?
- Who makes the trust decision?

Deliverable

Actor inventory.

---

# Step 3 — Identify Boundary Crossings

A boundary crossing occurs whenever information moves between trust zones.

Examples

- Browser → Web Application
- User → API
- API → Database
- Project → Namespace
- Application → External API
- CI/CD → Repository

Each crossing should be documented independently.

Deliverable

Boundary crossing inventory.

---

# Step 4 — Identify Trust Decisions

Every boundary crossing should answer one or more trust questions.

Examples

Identity

- Who is making the request?

Authorization

- Is the actor allowed to perform this action?

Ownership

- Does the resource belong to this actor?

Integrity

- Has the request been modified?

Business Context

- Does this operation satisfy the workflow requirements?

Deliverable

Trust decision catalogue.

---

# Step 5 — Identify Security Controls

Determine which controls enforce each trust decision.

Examples

Authentication

Authorization

Session Validation

CSRF Protection

Input Validation

Ownership Validation

Audit Logging

Integrity Verification

Rate Limiting

Deliverable

Control mapping.

---

# Types of Trust Boundaries

## Identity Boundary

Verifies who is making the request.

Examples

- Login
- Session
- API Token
- OAuth

---

## Authorization Boundary

Determines what an actor is allowed to do.

Examples

- Role checks
- Permission checks
- Resource access

---

## Ownership Boundary

Determines whether an actor owns or controls a resource.

Examples

- Project ownership
- Organization ownership
- Repository ownership

---

## Data Boundary

Protects sensitive information crossing system components.

Examples

- User input
- File uploads
- API payloads
- Database queries

---

## Service Boundary

Separates internal systems from external services.

Examples

- Payment providers
- Identity providers
- Notification services
- Cloud storage

---

## Process Boundary

Separates synchronous and asynchronous execution.

Examples

- Background jobs
- Queues
- Scheduled tasks
- Workers

---

# Trust Boundary Checklist

For every boundary ask:

- Who is requesting the operation?
- What resource is affected?
- What assumptions are being made?
- What security controls enforce those assumptions?
- Can trust be inherited?
- Can trust be replayed?
- Can trust become stale?
- Is the boundary crossed more than once?

---

# Security Perspective

Common vulnerability classes associated with trust boundaries include:

- Broken Authorization
- IDOR
- Privilege Escalation
- Business Logic Flaws
- Race Conditions
- TOCTOU
- Cross-Tenant Access
- Data Exposure

Boundary analysis helps identify where these vulnerabilities are most likely to occur.

---

# Researcher's Notes

## Observation 1

Trust should never be assumed simply because a request has already crossed one boundary.

## Observation 2

Many workflows cross multiple trust boundaries, requiring independent validation at each stage.

## Observation 3

Shared trust decisions are often reused across different workflows, making them attractive targets for security testing.

---

# Key Takeaways

- Trust boundaries identify where applications must re-evaluate trust.
- Every boundary crossing requires explicit validation.
- Different types of boundaries protect different architectural concerns.
- Systematically documenting trust boundaries leads to more focused authorization and business logic testing.
