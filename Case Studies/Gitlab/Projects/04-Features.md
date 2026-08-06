# Features

## Introduction

GitLab Projects provide a comprehensive set of features that support the planning, development, security, deployment, and maintenance of software.

Rather than acting solely as a Git repository, a Project serves as a platform that integrates multiple capabilities into a single collaboration environment. Each feature contributes to one or more business objectives and introduces its own workflows, business rules, authorization requirements, and security considerations.

Understanding these features is essential because each one represents a distinct attack surface that should be analyzed independently.

---

# Core Features

## Repository Management

Description

The repository stores the project's source code and Git history. It provides version control through commits, branches, tags, and merge operations.

Primary Capabilities

- Store source code
- Manage branches
- Track commits
- Manage tags
- Clone repositories

Business Value

Provides version control and source code management.

---

## Issue Management

Description

Issues allow teams to plan, prioritize, assign, and track work throughout the software development lifecycle.

Primary Capabilities

- Create issues
- Assign issues
- Label issues
- Comment
- Close and reopen issues

Business Value

Supports project planning and work tracking.

---

## Merge Requests

Description

Merge Requests enable code review before changes are merged into the target branch.

Primary Capabilities

- Submit code for review
- Discuss code changes
- Approve changes
- Merge branches

Business Value

Improves code quality and collaboration.

---

## CI/CD Pipelines

Description

Projects integrate with GitLab CI/CD to automate building, testing, and deployment.

Primary Capabilities

- Execute pipelines
- Run automated tests
- Deploy applications
- Generate build artifacts

Business Value

Automates software delivery.

---

## Project Members

Description

Projects allow users to collaborate using role-based access control.

Primary Capabilities

- Invite members
- Assign roles
- Remove members
- Manage permissions

Business Value

Supports secure collaboration.

---

## Wiki

Description

Projects provide an integrated Wiki for documentation.

Primary Capabilities

- Create documentation
- Edit documentation
- Organize project knowledge

Business Value

Centralizes project documentation.

---

## Releases

Description

Projects manage software releases and version history.

Primary Capabilities

- Publish releases
- Attach release assets
- Track release history

Business Value

Supports software distribution.

---

## Packages

Description

Projects provide package registries for storing build artifacts and dependencies.

Primary Capabilities

- Publish packages
- Download packages
- Manage package versions

Business Value

Supports software distribution and dependency management.

---

## Project Settings

Description

Projects expose administrative settings that configure project behavior.

Primary Capabilities

- Configure visibility
- Configure integrations
- Configure CI/CD
- Configure repository settings
- Configure security settings

Business Value

Controls how the Project operates.

---

# Feature Relationships

```
GitLab Project

├── Repository

├── Issues

├── Merge Requests

├── Members

├── CI/CD

├── Wiki

├── Packages

├── Releases

└── Settings
```

Each feature introduces its own workflows, business rules, authorization model, and security requirements while remaining within the Project boundary.

---

# Security Perspective

From an application security perspective, every feature should be considered an independent attack surface.

Each feature contains:

- Business workflows
- Authorization decisions
- State transitions
- User interactions
- System interactions
- Trust boundaries

Rather than testing an entire Project as one feature, security assessments should analyze each feature independently before evaluating how they interact.

---

# Researcher's Notes

## Observation 1

Projects are containers for multiple independent capabilities rather than a single feature. Each capability should be analyzed separately during security testing.

---

## Observation 2

Many workflows span multiple features. For example, adding a Project Member changes authorization, which can affect access to repositories, merge requests, issues, pipelines, and settings.

---

## Observation 3

Because features interact with one another, business logic flaws may arise at the boundaries between features rather than within an individual feature.

---

# Key Takeaways

- A GitLab Project is composed of multiple independent features.
- Each feature provides distinct business capabilities.
- Every feature introduces its own workflows and business rules.
- Features should be treated as individual attack surfaces during security testing.
- Understanding feature relationships is essential before modeling workflows.
