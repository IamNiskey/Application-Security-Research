# Reporting and Documentation

## Introduction

Security research is only valuable if its results can be understood, reproduced, and reused.

Reporting and documentation transform observations, experiments, and vulnerabilities into durable knowledge that benefits future research, improves security testing, and enables others to verify conclusions.

The objective is not merely to document vulnerabilities, but to document understanding.

---

# Documentation Pipeline

```text
Research
        │
        ▼
Evidence Collection
        │
        ▼
Validation
        │
        ▼
Root Cause Analysis
        │
        ▼
Security Findings
        │
        ▼
Recommendations
        │
        ▼
Reusable Knowledge
```

Every stage should produce artifacts that can be independently reviewed.

---

# Step 1 — Document the Target

Capture basic information about the application.

Include

- Application name
- Feature under analysis
- Research scope
- Version (if known)
- Research date
- Documentation references

Deliverable

Target profile.

---

# Step 2 — Record Observations

During research, record observations even if they do not immediately appear to be vulnerabilities.

Examples

- Unexpected responses
- Hidden workflows
- New objects
- State transitions
- Authorization behavior
- Timing differences
- Error messages

Deliverable

Research log.

---

# Step 3 — Preserve Evidence

Every important conclusion should be supported by evidence.

Examples

- HTTP requests
- HTTP responses
- Screenshots
- API responses
- Logs
- Timeline diagrams
- State diagrams

Evidence should allow another researcher to reproduce the observation.

Deliverable

Evidence repository.

---

# Step 4 — Validate Findings

Before documenting a vulnerability, verify that it is:

- Reproducible
- Consistent
- Not a false positive
- Supported by evidence

If possible, reproduce the finding using multiple approaches.

Deliverable

Validated findings.

---

# Step 5 — Perform Root Cause Analysis

Do not stop after identifying the vulnerability.

Determine:

- Which business rule failed?
- Which invariant was violated?
- Which trust boundary failed?
- Which workflow permitted the issue?
- Which architectural assumption was incorrect?

Deliverable

Root cause analysis.

---

# Step 6 — Write the Finding

Every finding should include:

## Title

A concise description of the issue.

## Summary

A short explanation of the vulnerability.

## Business Impact

Describe the effect on the business or users.

## Technical Description

Explain how the vulnerability occurs.

## Preconditions

List any required permissions, states, or conditions.

## Reproduction Steps

Provide clear, repeatable instructions.

## Evidence

Include requests, responses, screenshots, and observations.

## Root Cause

Identify the architectural or business logic failure.

## Recommendations

Provide practical remediation guidance.

Deliverable

Complete finding report.

---

# Step 7 — Document the Research

Even when no vulnerabilities are discovered, preserve the research.

Include

- Architecture
- Workflows
- Business Rules
- Invariants
- State Machines
- Trust Boundaries
- Attack Surface
- Test Cases
- Lessons Learned

Negative results remain valuable because they reduce duplicate effort in future research.

Deliverable

Case study.

---

# Step 8 — Build Reusable Knowledge

Convert completed research into reusable assets.

Examples

- Methodologies
- Checklists
- Testing patterns
- Decision trees
- Workflow diagrams
- State models
- Trust boundary maps
- Case studies

Each project should strengthen future research.

Deliverable

Knowledge library.

---

# Documentation Quality Checklist

Before publishing, verify:

- Scope is clearly defined.
- Evidence supports every conclusion.
- Findings are reproducible.
- Root causes are identified.
- Recommendations are actionable.
- Diagrams are accurate.
- References are included.
- Terminology is consistent.

---

# Security Perspective

High-quality documentation should answer:

- What was tested?
- Why was it tested?
- How was it tested?
- What assumptions were evaluated?
- What evidence supports the conclusions?
- What business impact exists?
- How should the issue be remediated?

If these questions cannot be answered, the research is incomplete.

---

# Researcher's Notes

## Observation 1

The quality of research is measured not only by discovered vulnerabilities but also by the clarity and reproducibility of the documentation.

## Observation 2

A well-documented negative result is often more valuable than an undocumented positive result.

## Observation 3

Reusable documentation compounds in value over time, allowing future assessments to begin with architectural understanding instead of starting from scratch.

---

# Publication Checklist

Before publishing a case study or report:

- Verify all findings.
- Remove sensitive information.
- Confirm screenshots are appropriately sanitized.
- Cite official documentation where applicable.
- Ensure diagrams match the final architecture.
- Review grammar and formatting.
- Verify all references remain accessible.

---

# Key Takeaways

- Documentation is a core part of application security research.
- Every finding should be supported by reproducible evidence.
- Root cause analysis provides more value than describing symptoms.
- Reusable knowledge transforms individual assessments into a long-term research asset.
- High-quality reporting benefits researchers, developers, and future investigations alike.
