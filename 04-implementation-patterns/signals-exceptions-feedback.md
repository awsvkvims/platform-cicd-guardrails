# Signals, Exceptions, and Feedback

## Purpose

This document defines how **CI/CD guardrails communicate, adapt, and improve over time**.

Effective guardrails do not simply block or allow changes.
They:
- Emit **signals** that describe system health
- Allow **controlled exceptions** when necessary
- Create **feedback loops** that drive platform and policy improvement

Without these mechanisms, guardrails become brittle gates.
With them, guardrails become enablement systems.

---

## Core Concept: Signals ≠ Enforcement

A foundational design principle:

> **Signals inform decisions. Enforcement applies constraints.**

These must remain **decoupled**.

### Signals
- Describe *what is happening*
- Are observable, queryable, and trendable
- Exist even when no enforcement is applied

Examples:
- Test coverage change over time
- Frequency of security exceptions
- Percentage of deployments requiring manual override
- Drift between desired and actual infrastructure state

### Enforcement
- Applies rules at defined control points
- Is intentionally progressive
- Can be relaxed, scoped, or overridden with intent

Signals exist **before**, **during**, and **after** enforcement.

---

## Signal Types in CI/CD Guardrails

### 1. Compliance Signals
Indicate whether a change meets defined expectations.

Examples:
- Required checks present or missing
- Policy evaluations passed or failed
- Artifact provenance verified or unknown

Used by:
- Platform teams
- Security
- Audit stakeholders

---

### 2. Friction Signals
Reveal where guardrails slow or block delivery.

Examples:
- Time waiting on approvals
- Frequency of bypass requests
- Re-runs caused by unclear rules
- Failed checks due to flaky tests

Used by:
- Enablement teams
- Platform owners

These signals guide **guardrail improvement**, not punishment.

---

### 3. Risk Signals
Describe exposure and impact, not compliance posture.

Examples:
- Severity distribution of bypassed checks
- Age of unresolved policy exceptions
- Scope of changes made under override

Used by:
- Leadership
- Risk and security partners

---

## Exception Patterns (Bypass Without Chaos)

Exceptions are **first-class citizens** in a healthy guardrail system.

If exceptions are hidden or discouraged, teams will route around guardrails entirely.

### Principles for Exceptions

Exceptions must be:
- **Explicit** — never silent
- **Scoped** — limited in impact
- **Time-bound** — expire automatically
- **Observable** — generate signals

---

### Common Exception Mechanisms

#### 1. Time-Bound Overrides
Allow a rule to be bypassed for a fixed duration.

Example:
- “Skip vulnerability gate for 48 hours while patch is validated”

Signal emitted:
- Override duration
- Affected scope
- Reason category

---

#### 2. Scoped Exceptions
Limit bypass to:
- A single repository
- A specific environment
- A defined change type

Example:
- “Allow direct deploy to staging for migration repo only”

---

#### 3. Risk-Acknowledged Overrides
Require acknowledgment, not approval.

Example:
- Checkbox or annotation:
  > “I acknowledge this bypass increases risk in X way”

This shifts behavior from compliance theater to informed decision-making.

---

## What Exceptions Are NOT

Exceptions must never:
- Be permanent
- Be invisible
- Be justified by seniority alone
- Become the default path

If they do, the guardrail has failed.

---

## Feedback Loops: How Guardrails Improve

Signals and exceptions feed structured feedback loops.

### Feedback Loop 1: Platform Improvement
High bypass frequency → invest in:
- Faster tests
- Better tooling
- Clearer rules

---

### Feedback Loop 2: Policy Calibration
Consistent low-risk overrides → adjust:
- Thresholds
- Enforcement level
- Scope of the rule

---

### Feedback Loop 3: Organizational Learning
Repeated exceptions → ask:
- Is this policy aligned with how teams actually work?
- Is the cost of enforcement higher than the risk it mitigates?

---

## Guardrail Anti-Patterns to Avoid

❌ Silent bypasses  
❌ Permanent exceptions  
❌ Manual approval as default  
❌ Single “compliance score”  
❌ Enforcement without signal visibility  

These destroy trust and create shadow delivery paths.

---

## Relationship to Other Patterns

This model connects directly to:
- **Reusable Workflows** — where signals are emitted
- **Enforcement Levels** — where enforcement is applied
- **Rollout Playbooks** — where feedback drives evolution

Signals, exceptions, and feedback are what turn guardrails
from **rules** into **systems**.

---

## Key Takeaway

> **Strong guardrails constrain risk.  
> Great guardrails teach the system how to improve.**

