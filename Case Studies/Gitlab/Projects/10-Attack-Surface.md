# Attack Surface

## Introduction

The attack surface of a GitLab Project consists of every feature, workflow, interface, and trust boundary through which an actor can read, modify, or influence Project resources.

Rather than identifying only URLs or API endpoints, this research models the attack surface in terms of business capabilities. Each capability represents a potential entry point for authorization testing, business logic analysis, race condition testing, and workflow validation.

---

# Attack Surface Overview

```text
                    GitLab Project
                           │
     ┌────────────┬────────────┬────────────┬────────────┐
     │            │            │            │
 Repository    Members     Settings      CI/CD
     │            │            │            │
     ├────────────┼────────────┼────────────┤
                  │
           Business Workflows
                  │
     ┌────────────┼────────────┬────────────┐
     │            │            │
 Visibility   Namespace   Integrations
```

Every component above exposes one or more workflows that should be evaluated independently.

---

# Attack Surface Categories

## AS-001 Project Creation

Business Capability

Create a new Project.

Primary Security Questions

- Who can create Projects?
- Can namespace restrictions be bypassed?
- Can project names or paths conflict?
- Are quotas enforced correctly?

---

## AS-002 Project Configuration

Business Capability

Modify Project settings.

Examples

- Visibility
- General settings
- Repository settings
- Feature toggles
- CI/CD settings

Primary Security Questions

- Who may modify settings?
- Are configuration changes properly authorized?
- Can restricted settings be modified indirectly?

---

## AS-003 Repository Management

Business Capability

Manage source code.

Examples

- Push
- Pull
- Branches
- Tags
- Commits

Primary Security Questions

- Can repository permissions be bypassed?
- Are protected branches enforced?
- Can cross-project access occur?

---

## AS-004 Membership Management

Business Capability

Manage Project members and roles.

Primary Security Questions

- Who may invite members?
- Who may change roles?
- Can inherited permissions be abused?
- Can membership changes race with authorization checks?

---

## AS-005 Project Visibility

Business Capability

Control Project accessibility.

Visibility Levels

- Public
- Internal
- Private

Primary Security Questions

- Can visibility restrictions be bypassed?
- Can confidential data become exposed?
- Do cached resources respect visibility changes?

---

## AS-006 Namespace Operations

Business Capability

Associate the Project with its owning namespace.

Primary Security Questions

- Can Projects move between namespaces without authorization?
- Are ownership relationships preserved?
- Are inherited permissions updated correctly?

---

## AS-007 Project Lifecycle

Business Capability

Manage operational state.

Examples

- Archive
- Restore
- Delete
- Recover

Primary Security Questions

- Are state transitions validated?
- Can archived Projects still be modified?
- Can deletion workflows be bypassed?

---

## AS-008 CI/CD

Business Capability

Execute automated workflows.

Examples

- Pipelines
- Jobs
- Variables
- Artifacts

Primary Security Questions

- Can unauthorized users trigger pipelines?
- Are secrets adequately protected?
- Can pipeline execution bypass Project permissions?

---

## AS-009 External Integrations

Business Capability

Communicate with external systems.

Examples

- Webhooks
- Slack
- Jira
- Kubernetes

Primary Security Questions

- Are integrations authenticated?
- Is inbound data trusted appropriately?
- Can external systems perform unauthorized actions?

---

## AS-010 API Access

Business Capability

Interact with Projects through the GitLab API.

Primary Security Questions

- Are API and UI authorization rules consistent?
- Are object identifiers validated?
- Can users access Projects outside their authorization scope?

---

# Shared Attack Surfaces

Several workflows interact with the same Project state.

Examples include:

- Membership and visibility
- Namespace and ownership
- Settings and CI/CD
- Repository and merge requests

These shared areas are strong candidates for business logic flaws and race condition testing because multiple workflows operate on the same underlying resources.

---

# Security Perspective

Every attack surface should be evaluated from multiple perspectives:

- Authentication
- Authorization
- Input validation
- Workflow integrity
- State transitions
- Trust boundaries
- Shared state consistency

Testing should focus on whether the application consistently enforces its business rules across all interfaces.

---

# Researcher's Notes

## Observation 1

The Project attack surface extends beyond repositories and includes every workflow that can modify Project state or expose Project information.

## Observation 2

Many attack surfaces overlap. A single action, such as changing Project visibility, can affect repositories, issues, merge requests, packages, and CI/CD behavior.

## Observation 3

The highest-risk areas are often workflows that modify shared Project state, particularly membership, ownership, visibility, namespace association, and lifecycle operations.

---

# Key Takeaways

- Attack surfaces should be modeled as business capabilities rather than individual endpoints.
- Every Project feature introduces one or more attack surfaces.
- Shared Project state increases the likelihood of business logic flaws and race conditions.
- A structured attack surface model provides a foundation for systematic security testing.
