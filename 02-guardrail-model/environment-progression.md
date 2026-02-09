# Environment-Based Guardrail Progression

Guardrails should **progress deliberately across environments**, increasing enforcement
as confidence, signal quality, and system maturity improve.

This avoids the two most common failure modes:
- Over-enforcement too early (delivery paralysis)
- Under-enforcement too late (risk exposure)

---

## Core Principle

> **Guardrails should be strictest where risk is highest and learning cost is lowest.**

This usually means:
- Advisory guardrails in lower environments
- Enforced guardrails in higher environments
- Runtime controls everywhere

---

## Why Environments Matter

Different environments exist to support **different kinds of learning**:

| Environment | Primary Purpose |
|------------|-----------------|
| Dev | Fast feedback, experimentation |
| CI | Consistency, repeatability |
| Test / QA | Integration confidence |
| Staging | Production-like validation |
| Production | Customer safety & reliability |

Guardrails should respect these purposes.

---

## Progressive Enforcement by Environment

### Development (Local / Dev)

**Goal:** Learn fast, avoid friction

Typical guardrails:
- Advisory linting and checks
- Warnings for missing metadata
- Optional feature flag usage

Not appropriate here:
- Hard policy failures
- Security gate approvals
- Mandatory rollout constraints

Reason:
> Early friction discourages adoption and experimentation.

---

### Continuous Integration (CI)

**Goal:** Prevent obvious defects from propagating

Typical guardrails:
- Required tests passing
- Basic security scanning (informational or soft-fail)
- Build reproducibility checks
- Artifact provenance capture

Enforcement style:
- Fail builds only on **clear, deterministic issues**
- Avoid flaky or slow checks

---

### Test / Integration Environments

**Goal:** Validate system behavior

Typical guardrails:
- Dependency compatibility checks
- Contract verification
- Infrastructure policy validation (IaC)
- Feature flag presence for risky changes (soft enforcement)

This is where **guardrails begin to shape behavior**.

---

### Staging / Pre-Production

**Goal:** Reduce production risk

Typical guardrails:
- Required rollout strategies declared
- Feature flags required for user-impacting changes
- Security findings with severity-based enforcement
- Promotion blocked without rollback capability

Key shift:
> Guardrails now protect *customers*, not just pipelines.

---

### Production

**Goal:** Protect users and the business

Typical guardrails:
- Enforced progressive delivery
- Mandatory runtime disablement mechanisms
- Policy-driven exposure limits
- Automated rollback or exposure halt on signal breach

Important:
- Enforcement happens **at runtime**, not only at deploy time
- Manual approvals should be rare or eliminated

---

## Maturity Progression Over Time

Guardrails should evolve as the organization matures.

### Early Maturity
- Advisory checks
- Manual interpretation
- Focus on learning

### Intermediate Maturity
- Selective enforcement
- Policy-driven rules
- Consistent patterns across teams

### Advanced Maturity
- Automated enforcement
- Runtime signal integration
- Minimal human gating

---

## Example: Feature Flag Enforcement Progression

| Environment | Expectation |
|------------|-------------|
| Dev | Optional |
| CI | Recommended |
| Staging | Required for risky changes |
| Prod | Required with runtime controls |

---

## Example: Infrastructure-as-Code (IaC) Progression

| Environment | Enforcement |
|------------|-------------|
| Dev | Policy warnings |
| CI | Soft-fail on violations |
| Staging | Hard-fail on critical violations |
| Prod | Strict policy enforcement |

---

## Anti-Patterns to Avoid

- Same enforcement everywhere
- Production-only guardrails
- Approval-heavy controls replacing automation
- Introducing enforcement before signal quality is trusted

---

## How Leaders Should Use This Model

- Ask **where enforcement belongs**, not “why teams failed”
- Fund enablement before tightening controls
- Treat guardrails as evolving system capabilities

Guardrails succeed when they **disappear into the flow of delivery**.

