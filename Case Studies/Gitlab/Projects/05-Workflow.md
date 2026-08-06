# Workflow

## Introduction

A GitLab Project progresses through a series of business workflows from creation to deletion.

Rather than viewing a Project as a static object, this research models it as a collection of workflows, each containing validation steps, authorization decisions, state transitions, and business rules.

Understanding these workflows is essential because every security-sensitive action performed against a Project occurs within one of these workflows.

---

# Project Lifecycle

```text
Project Request

↓

Validation

↓

Project Creation

↓

Configuration

↓

Active Project

↓

Maintenance

↓

Archive

↓

Deletion
```

The Project lifecycle represents the highest-level workflow for a GitLab Project.

Each stage contains multiple sub-workflows that will be analyzed independently.

---

# Primary Workflows

## 1. Project Creation

Purpose

Create a new GitLab Project.

Typical Flow

```text
User Initiates Project Creation

↓

Validate Authentication

↓

Validate Namespace

↓

Validate Project Name

↓

Validate Project Path (Slug)

↓

Validate Visibility

↓

Apply Initial Configuration

↓

Initialize Repository (Optional)

↓

Persist Project

↓

Generate Audit Events

↓

Project Created
```

---

## 2. Project Configuration

Purpose

Configure project behavior after creation.

Typical Activities

- Update project settings
- Configure integrations
- Configure CI/CD
- Configure repository options
- Configure security settings

---

## 3. Project Maintenance

Purpose

Support day-to-day project operations.

Typical Activities

- Add members
- Remove members
- Push code
- Create issues
- Create merge requests
- Execute pipelines
- Manage releases

---

## 4. Project Archival

Purpose

Move a project into a read-only operational state.

Typical Activities

- Archive project
- Restrict modifications
- Preserve historical data

---

## 5. Project Deletion

Purpose

Permanently remove a project.

Typical Activities

- Verify authorization
- Verify deletion requirements
- Delete project resources
- Record audit information

---

# Workflow Hierarchy

```text
GitLab Project

├── Create Project

├── Configure Project

├── Manage Members

├── Manage Repository

├── Manage Issues

├── Manage Merge Requests

├── Manage CI/CD

├── Archive Project

└── Delete Project
```

Each workflow introduces its own business rules, authorization checks, and state transitions.

---

# Security Perspective

Every workflow contains one or more security-sensitive operations.

Examples include:

- Authentication checks
- Authorization decisions
- Input validation
- Resource ownership verification
- Visibility enforcement
- Namespace validation
- Audit logging

These validation points become the foundation for identifying business rules and designing security tests.

---

# Researcher's Notes

## Observation 1

Every workflow contains explicit validation stages before modifying project state.

## Observation 2

Project creation establishes the initial security boundary for all child resources.

## Observation 3

Most workflows eventually modify shared project state, making them candidates for authorization testing, race condition analysis, and business logic review.

---

# Key Takeaways

- GitLab Projects are governed by multiple interconnected workflows.
- Every workflow contains business decisions and validation logic.
- Workflows are the foundation for deriving business rules and security tests.
- Each workflow should be analyzed independently before evaluating interactions between workflows.
