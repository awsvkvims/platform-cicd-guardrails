# Policy Types Deep Dive

## Purpose

This document describes the **core classes of guardrail policies** enforced in modern
CI/CD systems and how they map to delivery risk, maturity, and organizational intent.

Each policy type:
- Targets a different failure mode
- Applies at different points in the delivery lifecycle
- Progresses from advisory to enforced over time

This is a **conceptual model**, not a tool catalog.

---

## Policy Type 1: Feature Flag & Release-on-Demand Guardrails

### Why This Policy Exists

Traditional deployments couple:
- code deployment
- feature exposure
- customer impact

This coupling increases:
- blast radius
- rollback risk
- decision pressure

Feature flag guardrails decouple **deployment from release**.

---

### What These Guardrails Protect Against

- Irreversible production changes
- High-risk paths without rollback
- Late-stage approval bottlenecks
- Emergency hotfixes

---

### Common Guardrail Checks

| Guardrail | Intent |
|---------|--------|
| Kill switch declared | Ensure rapid rollback |
| Flag ownership defined | Accountability without approval |
| Rollout strategy declared | Prevent “all-at-once” releases |
| Flag expiry required | Prevent permanent toggles |
| Environment defaults enforced | Prevent accidental exposure |

---

### Enforcement Progression

**Early maturity**
- Warn if flags are missing
- Log rollout metadata

**Growing maturity**
- Block prod deploys for high-risk paths without flags
- Require explicit rollout strategy

**Advanced maturity**
- Enforce progressive rollout by default
- Require experiment metrics for exposure changes

---

### Key Principle

> Feature flags are **safety mechanisms**, not permission systems.

---

## Policy Type 2: Infrastructure-as-Code (IaC) Guardrails

### Why This Policy Exists

Manual or inconsistent infrastructure changes:
- bypass review
- drift from intent
- fail silently

IaC guardrails ensure infrastructure changes are:
- intentional
- reviewable
- reversible

---

### What These Guardrails Protect Against

- Manual console changes
- Environment drift
- Unsafe production modifications
- Non-reproducible infrastructure

---

### Common Guardrail Checks

| Guardrail | Intent |
|---------|--------|
| IaC-only changes enforced | Prevent console drift |
| Environment scope validation | Prevent cross-env impact |
| Destructive change detection | Flag high-risk ops |
| Plan diff visibility | Improve decision-making |
| Approval replacement | Replace manual approvals with policy |

---

### Enforcement Progression

**Early maturity**
- Detect and report drift
- Warn on destructive changes

**Growing maturity**
- Block prod changes without reviewed plans
- Require explicit acknowledgment of risk

**Advanced maturity**
- Auto-apply low-risk changes
- Enforce immutable infra patterns

---

### Key Principle

> Guardrails replace approvals by making intent explicit and verifiable.

---

## Policy Type 3: Provenance & Supply Chain Guardrails

### Why This Policy Exists

Modern delivery pipelines assemble software from:
- source code
- dependencies
- build systems
- artifacts

Without provenance:
- trust is implicit
- investigation is slow
- compliance becomes manual

---

### What These Guardrails Protect Against

- Unknown artifact origins
- Untrusted build systems
- Tampered dependencies
- Audit gaps

---

### Common Guardrail Checks

| Guardrail | Intent |
|---------|--------|
| Artifact built by trusted pipeline | Prevent foreign artifacts |
| Commit-to-artifact traceability | Enable root cause analysis |
| Dependency source validation | Reduce supply chain risk |
| Signature verification | Detect tampering |
| Environment promotion rules | Prevent artifact swapping |

---

### Enforcement Progression

**Early maturity**
- Record provenance metadata
- Log build → deploy links

**Growing maturity**
- Block deployments of unsigned artifacts
- Require traceable source

**Advanced maturity**
- Enforce policy-based promotion
- Automate compliance evidence

---

### Key Principle

> Provenance turns “trust us” into “prove it”.

---

## How Policy Types Work Together

These policies are **complementary**, not independent.

| Policy Type | Primary Risk Reduced |
|-----------|----------------------|
| Feature Flags | Customer impact |
| IaC | Infrastructure stability |
| Provenance | Supply chain integrity |

Together, they enable:
- faster delivery
- safer change
- lower cognitive load

---

## Relationship to Other Sections

- Guardrail enforcement levels  
  → `02-guardrail-model/enforcement-levels.md`

- Injection points in delivery lifecycle  
  → `04-implementation-patterns/delivery-lifecycle-injection-points.md`

- Reusable workflow patterns  
  → `04-implementation-patterns/reusable-workflows.md`

---

## Key Takeaway

Guardrails are most effective when they:
- focus on *risk*, not rules
- evolve with maturity
- remove the need for human approvals

The goal is **safer speed**, not stricter control.

