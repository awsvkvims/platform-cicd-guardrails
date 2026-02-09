# Delivery Lifecycle & Guardrail Injection Points

## Purpose

This document explains **where CI/CD guardrails attach within the delivery lifecycle**,  
what kinds of controls belong at each stage, and how signals flow without disrupting teams.

The goal is **system-level safety and consistency**, not slowing delivery or introducing manual gates.

---

## The Delivery Lifecycle (Conceptual)

Modern software delivery typically flows through the following stages:

1. Code Creation
2. Pull Request / Review
3. Merge
4. Build & Package
5. Artifact Promotion
6. Deployment
7. Runtime & Operations

Guardrails can be injected at multiple points — but **not all guardrails belong everywhere**.

---

## Guardrail Design Principle

> **Earlier stages provide signals; later stages enforce decisions.**

This preserves:
- Developer flow
- Fast feedback
- Progressive enforcement
- Trust in the system

---

## Injection Points by Lifecycle Stage

---

### 1. Code Creation (Local Development)

**What happens here**
- Developers write code
- Run tests locally
- Experiment freely

**Guardrails here**
- ❌ None enforced
- ✅ Optional local feedback (linters, test hints)

**Why**
- Local development must remain fast and autonomous
- Enforcement here creates friction and workarounds

**Signals emitted**
- None collected centrally

---

### 2. Pull Request Creation

**What happens here**
- Code becomes visible
- Intent is declared
- Collaboration begins

**Guardrails here**
- Soft guardrails only
  - Static analysis warnings
  - Security scan annotations
  - Policy hints

**Enforcement**
- ❌ No hard blocking (early maturity)
- ⚠️ Advisory comments

**Signals emitted**
- Lint results
- Test outcomes
- Security findings
- Policy evaluations

**Why**
- PRs are the best place for learning
- Blocking here too early leads to bypassing

---

### 3. Merge

**What happens here**
- Code becomes shared truth
- Risk increases

**Guardrails here**
- Conditional enforcement
  - Required checks
  - Policy thresholds
  - Exception paths

**Enforcement**
- ✅ Allowed with guardrails
- ❌ Block only on high-risk violations

**Signals emitted**
- Merge outcomes
- Exception usage
- Policy compliance trends

---

### 4. Build & Package

**What happens here**
- Artifacts are created
- Supply chain risk emerges

**Guardrails here**
- Strong enforcement
  - Reproducible builds
  - SBOM generation
  - Dependency checks

**Enforcement**
- ✅ Build must pass
- ❌ Non-compliant artifacts are rejected

**Signals emitted**
- Build success/failure
- Dependency risk
- Artifact metadata

---

### 5. Artifact Promotion

**What happens here**
- Artifacts move across environments
- Risk increases with exposure

**Guardrails here**
- Policy-driven promotion
  - Environment-specific thresholds
  - Time-based controls
  - Approval automation

**Enforcement**
- ✅ Automated allow/deny
- ❌ No manual approvals as default

**Signals emitted**
- Promotion latency
- Exception frequency
- Policy drift

---

### 6. Deployment

**What happens here**
- Artifacts reach users
- Blast radius matters

**Guardrails here**
- Deployment safety checks
  - Readiness
  - Progressive rollout controls
  - Health gating

**Enforcement**
- ✅ Block unsafe deployments
- 🔁 Automated rollback triggers

**Signals emitted**
- Deployment success
- Rollback events
- Error budgets

### Deployment & Promotion

At this stage, guardrails ensure that deployments are **safe by default**.

Typical enforcement:
- Rollout strategy declared (e.g., progressive, canary)
- Kill-switch capability present for risky changes
- Separation of deploy and release validated

Guardrails should verify **capability**, not configuration detail.

---

### 7. Runtime & Operations

**What happens here**
- Systems operate continuously
- Drift and incidents occur

**Guardrails here**
- Drift detection
- Runtime policy enforcement
- Incident-based controls

**Enforcement**
- ✅ Alerting and automated remediation
- ❌ No retroactive punishment

**Signals emitted**
- Incident trends
- Drift frequency
- Recovery metrics

---
### Runtime & Operations

Runtime guardrails control **actual user exposure**.

Examples:
- Progressive rollout gated by health metrics
- Automatic exposure halt on SLO breach
- Immediate disablement without redeploy

This is where Release on Demand is enforced.

Key principle:
> Runtime guardrails protect customers when prediction fails.

---

## What Does NOT Belong Anywhere

The following patterns are **explicit anti-patterns**:

- Manual approval gates as default
- Individual developer metrics
- Team ranking
- One-size-fits-all thresholds
- Enforcement without feedback

---

## Signal Flow Summary

1. Signals are emitted early
2. Signals are aggregated centrally
3. Enforcement increases with risk
4. Exceptions are tracked, not punished
5. Leaders act on trends, not individuals

---

## How This Enables Scale

This model:
- Preserves developer autonomy
- Enables platform consistency
- Supports regulatory needs
- Scales across teams and environments

Guardrails become **invisible safety rails**, not speed bumps.

---

## Relationship to Other Artifacts

- Enforcement progression → `02-guardrail-model/`
- Reusable workflows → `04-implementation-patterns/reusable-workflows.md`
- Environment tightening → (next section)

