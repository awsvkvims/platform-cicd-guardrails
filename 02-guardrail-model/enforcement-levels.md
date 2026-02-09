# Guardrail Enforcement Levels

## Purpose

This document defines a **shared enforcement model** for CI/CD guardrails.

It allows organizations to:
- Apply safety controls without slowing delivery
- Scale governance across many teams
- Adjust enforcement based on risk and maturity

The goal is **consistent enforcement logic**, not uniform rigidity.

---

## Guardrails vs Enforcement

A **guardrail** is *what* is being checked.  
**Enforcement level** defines *what happens* when the guardrail is triggered.

Example:
- Guardrail: “Container images must be scanned”
- Enforcement level: Observe → Warn → Gate → Block

---

## The Enforcement Spectrum

### Level 0: Observe

**What happens**
- Signal is collected
- No feedback in the pipeline

**When to use**
- Introducing new controls
- Establishing baselines
- Building trust

**Example**
- Collect vulnerability data without surfacing it in CI

---

### Level 1: Warn

**What happens**
- Guardrail emits visible feedback
- Pipeline continues

**When to use**
- Early adoption
- Non-critical risk
- Behavioral nudges

**Example**
- Warning when test coverage drops below trend

---

### Level 2: Gate

**What happens**
- Explicit acknowledgement required
- Human-in-the-loop exception

**When to use**
- Elevated but contextual risk
- Transitional phases

**Example**
- Manual approval when deploying with known high-risk dependency

---

### Level 3: Block

**What happens**
- Pipeline fails
- Deployment prevented

**When to use**
- Critical, well-understood risk
- Regulatory or safety boundaries

**Example**
- Blocking deploy when artifact provenance is missing

---

## Environment-Based Enforcement

The same guardrail may have **different enforcement levels** by environment.

| Environment | Typical Enforcement |
|------------|---------------------|
| Dev        | Observe / Warn      |
| Staging    | Warn / Gate         |
| Production | Gate / Block        |

This preserves flow while maintaining safety where it matters most.

---

## Maturity-Based Progression

Enforcement should **progress over time**, not start at maximum strictness.

Typical progression:
1. Observe → establish baseline
2. Warn → socialize expectations
3. Gate → handle exceptions
4. Block → codify non-negotiables

This reduces resistance and increases adoption.

---
---

## Example Enforcement Progressions

This section provides **concrete examples** of how guardrail enforcement
can evolve over time and across environments as organizational maturity increases.

The intent is to show that:
- Guardrails are introduced **gradually**
- Enforcement tightens **as confidence grows**
- Different contexts justify different levels of strictness

---

## Example 1: Vulnerability Scanning Maturity Progression

### Phase 1: Early Adoption (Low Maturity)

**Goal:** Establish visibility without friction

| Environment | Enforcement |
|------------|-------------|
| Dev        | Observe     |
| Staging    | Observe     |
| Production | Warn        |

Behavior:
- Vulnerabilities are scanned and logged
- No pipeline failures
- Teams learn *what exists*, not *what to fix immediately*

---

### Phase 2: Growing Confidence (Medium Maturity)

**Goal:** Encourage remediation without blocking flow

| Environment | Enforcement |
|------------|-------------|
| Dev        | Warn        |
| Staging    | Warn        |
| Production | Gate        |

Behavior:
- Developers see warnings early
- Production deploys require explicit acknowledgement for high-risk issues
- Exceptions are visible and reviewable

---

### Phase 3: Established Practice (High Maturity)

**Goal:** Codify non-negotiable risk boundaries

| Environment | Enforcement |
|------------|-------------|
| Dev        | Warn        |
| Staging    | Gate        |
| Production | Block       |

Behavior:
- Teams expect and plan for security requirements
- Only clearly defined, critical issues block deploys
- Policy is predictable and trusted

---

## Example 2: Test Coverage Guardrail Across Environments

### Guardrail
> “Changes should not significantly reduce effective test coverage.”

### Enforcement Strategy

| Environment | Enforcement | Rationale |
|------------|-------------|-----------|
| Dev        | Warn        | Fast feedback without slowing iteration |
| Staging    | Gate        | Explicit decision before promotion |
| Production | Block       | Prevent silent quality regression |

Important nuance:
- This guardrail should be **trend-based**, not threshold-based
- The goal is detecting degradation, not hitting arbitrary numbers

---

## Example 3: Artifact Provenance (Supply Chain Security)

### Early Phase

| Environment | Enforcement |
|------------|-------------|
| Dev        | Observe     |
| Staging    | Warn        |
| Production | Gate        |

Purpose:
- Teach teams what provenance means
- Identify tooling gaps
- Avoid blocking delivery prematurely

---

### Mature Phase

| Environment | Enforcement |
|------------|-------------|
| Dev        | Warn        |
| Staging    | Gate        |
| Production | Block       |

At this stage:
- Tooling is standardized
- Teams understand requirements
- Enforcement reflects real risk tolerance

---

## Example 4: Progressive Enforcement Over Time (Same Environment)

Even within a single environment, enforcement may evolve.

### Production Environment — Year 1 → Year 2

| Timeframe | Enforcement |
|----------|-------------|
| Year 1   | Gate        |
| Year 2   | Block       |

What changed:
- Teams gained experience
- Exceptions declined
- Confidence in signals increased

Enforcement tightened **because readiness increased**, not because policy changed.

---

---

## Example 5: Infrastructure as Code (IaC) Guardrails

### Guardrail
> “All infrastructure changes must be defined and reviewed as code.”

This guardrail reduces configuration drift, improves auditability, and enables safer change management.

---

### Phase 1: Introduction (Low Maturity)

**Goal:** Encourage adoption without blocking teams

| Environment | Enforcement |
|------------|-------------|
| Dev        | Observe     |
| Staging    | Warn        |
| Production | Gate        |

Behavior:
- IaC usage is detected and reported
- Manual changes are logged but not blocked
- Teams learn tooling and workflows without pressure

---

### Phase 2: Standardization (Medium Maturity)

**Goal:** Make IaC the default path

| Environment | Enforcement |
|------------|-------------|
| Dev        | Warn        |
| Staging    | Gate        |
| Production | Block       |

Behavior:
- Staging and production require IaC-based changes
- Exceptions require explicit justification
- Drift detection becomes actionable

---

### Phase 3: Operating Discipline (High Maturity)

**Goal:** Eliminate unmanaged infrastructure risk

| Environment | Enforcement |
|------------|-------------|
| Dev        | Warn        |
| Staging    | Block       |
| Production | Block       |

Behavior:
- All environments are IaC-managed
- Manual changes are prohibited
- Infrastructure changes are predictable, reviewable, and auditable

---

## Example 6: Branch Protection & Merge Controls

### Guardrail
> “Critical branches must meet minimum safety conditions before merge.”

This guardrail protects shared codebases without preventing experimentation.

---

### Phase 1: Visibility & Learning

**Goal:** Make expectations visible

| Branch Type | Enforcement |
|------------|-------------|
| Feature    | Observe     |
| Main       | Warn        |

Signals:
- Missing reviews
- Skipped CI
- Force pushes

Behavior:
- Teams see what *would* have been blocked
- No hard failures

---

### Phase 2: Shared Responsibility

**Goal:** Prevent accidental risk

| Branch Type | Enforcement |
|------------|-------------|
| Feature    | Warn        |
| Main       | Gate        |

Behavior:
- Main branch requires:
  - CI completion
  - At least one reviewer
- Overrides are allowed but visible

---

### Phase 3: High-Trust Enforcement

**Goal:** Codify non-negotiable safety practices

| Branch Type | Enforcement |
|------------|-------------|
| Feature    | Warn        |
| Main       | Block       |

Behavior:
- No direct pushes to main
- Required reviews and CI enforced
- Exceptions handled via explicit process, not silent bypass

---

## Pattern to Notice

Across IaC and branch protection:

- Early phases focus on **learning and visibility**
- Middle phases introduce **intentional friction**
- Mature phases rely on **predictable enforcement**

> Strong guardrails feel restrictive only when introduced before enablement.

---

## Key Takeaways

- Enforcement should **follow maturity**, not precede it
- Early visibility builds trust
- Predictable progression reduces resistance
- Strict enforcement works only after enablement is in place

> Guardrails succeed when teams say  
> *“This is fair, predictable, and helps us.”*
---

## Ownership Model

| Responsibility        | Owner            |
|-----------------------|------------------|
| Guardrail definition  | Platform / Enablement |
| Enforcement level     | Architecture / Risk |
| Exception handling    | Product / Delivery |
| Execution             | CI/CD systems |

This separation prevents policy drift and shadow governance.

---

## Guardrails Are Not Targets

A critical reminder:

> **Enforcement levels are safety mechanisms, not performance goals.**

They should:
- Protect systems
- Enable teams
- Reduce risk

They should never:
- Rank teams
- Punish individuals
- Replace judgment

---

## Related Documents

- **Principles**
  - [Guardrails, Not Approvals](../01-principles/guardrails-vs-approvals.md)
  - [Progressive Enforcement](../01-principles/progressive-enforcement.md)

- **Implementation**
  - [Reusable Workflows](../04-implementation-patterns/reusable-workflows.md)

