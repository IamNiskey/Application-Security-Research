# Actors

## Introduction

An actor is any entity that interacts with a GitLab Project. Actors can be human users, automated systems, or external integrations. Each actor has a defined set of responsibilities, permissions, and interactions with project resources.

Understanding the actors involved in a GitLab Project is essential because almost every business rule and authorization decision is evaluated in the context of an actor attempting to perform an action.

---

# Human Actors

## Anonymous User

Description

A user who is not authenticated to GitLab.

Responsibilities

- Browse publicly accessible projects.
- View public repositories.
- View public issues.
- View public merge requests.

Restrictions

- Cannot modify project resources.
- Cannot create issues in private projects.
- Cannot access private project data.
- Cannot manage project settings.

---

## Authenticated User

Description

A user who has successfully authenticated to GitLab but is not necessarily a member of the project.

Responsibilities

- View projects according to visibility rules.
- Request access to projects (when permitted).
- Interact with resources they are authorized to access.

Restrictions

- Cannot perform member-only actions without appropriate permissions.

---

## Project Member

Description

A user who has been granted membership in a project either directly or indirectly through a group.

Project members receive permissions based on their assigned role.

Membership Types

- Direct Member
- Inherited Member
- Shared Member
- Inherited Shared Member

---

## Guest

Primary Responsibilities

- View project information.
- Participate in discussions.
- Create and comment on issues where permitted.

Restrictions

- Cannot push code.
- Cannot modify repositories.
- Cannot manage project configuration.

---

## Planner

Primary Responsibilities

- Plan and organize work.
- Create and manage issues.
- Manage milestones and iterations.

Restrictions

- Cannot push code.

---

## Reporter

Primary Responsibilities

- View source code.
- Create issues.
- Review project information.
- Generate reports.

Restrictions

- Cannot push code.
- Cannot manage project settings.

---

## Security Manager

Primary Responsibilities

- Review security findings.
- Manage vulnerability information.
- Manage compliance-related resources.

Restrictions

- Does not receive full project administration permissions.

---

## Developer

Primary Responsibilities

- Push code.
- Create branches.
- Create merge requests.
- Run CI/CD pipelines.
- Contribute to software development.

Restrictions

- Cannot perform many administrative project operations.

---

## Maintainer

Primary Responsibilities

- Manage project configuration.
- Manage members.
- Approve access.
- Configure CI/CD.
- Administer repositories.
- Manage releases.

Maintainers are responsible for the operational management of the project.

---

## Owner

Description

The highest project authority where applicable. In GitLab, the Owner role is primarily associated with groups. For projects in a personal namespace, the namespace owner effectively has owner-level permissions, while group-owned projects derive owner authority from the parent group.

Primary Responsibilities

- Full administrative control.
- Manage project ownership.
- Configure security settings.
- Delete or transfer projects where permitted.

---

# System Actors

## GitLab CI/CD

Role

Automates project workflows.

Responsibilities

- Execute pipelines.
- Build software.
- Deploy applications.
- Execute automated testing.

---

## GitLab Background Jobs

Responsibilities

- Process asynchronous tasks.
- Send notifications.
- Execute scheduled maintenance.
- Process imports and exports.

---

## External Integrations

Examples

- GitHub
- Slack
- Jira
- Kubernetes
- Webhooks
- Third-party CI/CD systems

Responsibilities

- Exchange information with the project.
- Trigger automated workflows.
- Synchronize external systems.

---

# Actor Hierarchy

```text
Anonymous User
        │
Authenticated User
        │
Project Member
        │
 ┌──────┼──────────────────────────────────────────┐
 │      │        │         │         │             │
Guest Planner Reporter Security Developer Maintainer
                                Manager
```

Project ownership and administrative authority may be provided through the owning namespace depending on how the project is managed.

---

# Security Perspective

Every security-sensitive operation within a GitLab Project is initiated by an actor.

The application evaluates:

- Who is performing the action?
- What role do they possess?
- How did they obtain that role?
- Is the action permitted?
- Does the resource belong to the current project?
- Are additional authorization conditions satisfied?

Because actor identity determines authorization decisions throughout GitLab, understanding actor capabilities is fundamental to analyzing business logic, authorization controls, and privilege boundaries.

---

# Researcher's Notes

## Observation 1

Project membership is not limited to direct invitations. Members can inherit access through groups or shared relationships, meaning authorization decisions depend not only on a user's role but also on the source of that role.

## Observation 2

Different actors interact with the same resources under different permission models. This creates opportunities to verify that authorization is consistently enforced across all roles.

## Observation 3

Automated actors, such as CI/CD pipelines and background jobs, execute privileged operations on behalf of users. Their permissions and trust boundaries should be analyzed alongside human actors.

---

# Key Takeaways

- Every action within a GitLab Project is performed by a defined actor.
- Project permissions are determined by roles and membership type.
- Human users, automation, and external integrations all participate in project workflows.
- Understanding actor capabilities is essential before modeling workflows or testing authorization.
