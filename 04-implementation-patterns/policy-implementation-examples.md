# Policy-as-Code Implementation Examples  
*(GitHub Actions & Jenkins)*

## Purpose

This document shows **how policy-as-code guardrails are implemented in real CI/CD systems**
without coupling the model to a single tool.

The goal is to demonstrate:
- Where guardrails live
- How they are evaluated
- How enforcement progresses
- How the same policy intent applies across tools

This is **not a tool comparison**.
It is a mapping from **guardrail intent → implementation pattern**.

---

## Shared Mental Model (Applies to All Tools)

Regardless of CI/CD system, guardrails follow the same shape:

1. **Input collection**
   - environment
   - artifact metadata
   - change context
2. **Policy evaluation**
   - deterministic logic
   - explainable outcome
3. **Enforcement decision**
   - allow / warn / block
4. **Evidence emission**
   - logs
   - structured output
   - audit trail

Only *where* this runs differs.

---

## GitHub Actions — Guardrail Patterns

### 1. Reusable Workflow as Guardrail Boundary

**Pattern**
- Guardrails live in centrally owned reusable workflows
- Product teams call them via `uses:`

**Why**
- Central ownership
- Versioned guardrails
- Consistent behavior across repos

**Example injection points**
- PR validation workflow
- Promotion workflow
- Deployment workflow

**Typical responsibilities**
- Validate deployment contracts
- Evaluate policy-as-code
- Emit structured decision output

---

### 2. Advisory → Enforced Progression

**Early stage**
- Guardrail runs
- Outputs warnings
- Does not fail the pipeline

**Later stage**
- Same guardrail
- Fails job based on environment or risk class

**Key insight**
> Enforcement level changes, not the policy logic.

---

### 3. Feature Flag & Release-on-Demand Guardrails

GitHub Actions commonly enforce:
- presence of kill-switch metadata
- rollout strategy declaration
- environment-based defaults

**Example controls**
- Block prod deploy if no rollback mechanism declared
- Require feature flags for high-risk paths
- Enforce flag expiry metadata

---

### 4. Evidence & Audit

GitHub Actions provide:
- immutable logs
- step outputs
- job summaries

These become:
- deployment evidence
- audit artifacts
- investigation inputs

---

## Jenkins — Guardrail Patterns

### 1. Shared Libraries as Guardrail Boundary

**Pattern**
- Guardrails implemented in Jenkins shared libraries
- Teams call standardized steps

**Why**
- Central governance
- Reuse across pipelines
- Controlled evolution

**Common injection points**
- Pre-merge pipelines
- Promotion pipelines
- Deployment stages

---

### 2. Policy Evaluation as Pipeline Stage

Policies are often evaluated as:
- explicit pipeline stages
- gated transitions between stages

**Example**
- “Evaluate Promotion Policy”
- “Validate Deployment Eligibility”

---

### 3. Progressive Enforcement

Jenkins pipelines often:
- mark builds unstable first
- later transition to failed builds

This supports:
- learning
- trust-building
- gradual adoption

---

### 4. Evidence & Audit

Jenkins provides:
- build logs
- archived artifacts
- metadata annotations

These serve the same purpose as in GitHub Actions:
- traceability
- auditability
- incident investigation

---

## What Is the Same Across Tools

| Concern | GitHub Actions | Jenkins |
|------|---------------|---------|
| Guardrail ownership | Central | Central |
| Policy logic | Code | Code |
| Enforcement progression | Config-driven | Stage-driven |
| Evidence | Logs + outputs | Logs + artifacts |
| Promotion awareness | Yes | Yes |

**Tool choice does not change guardrail design principles.**

---

## What This Enables

- Teams experience guardrails as **supportive**
- Leaders gain **consistent signals**
- Enablement teams avoid bespoke pipelines
- Compliance becomes a byproduct, not a bottleneck

---

## What This Intentionally Avoids

- Tool evangelism
- One-size-fits-all pipelines
- Embedding policy logic directly into application repos
- Hardcoded approvals

---

## Relationship to Other Docs

- Guardrail contracts  
  → `04-implementation-patterns/guardrail-contracts.md`

- Injection points  
  → `04-implementation-patterns/delivery-lifecycle-injection-points.md`

- Enforcement progression  
  → `02-guardrail-model/environment-progression.md`

---

## Key Takeaway

Guardrails are **architecture decisions**, not pipeline syntax.

CI/CD tools are **execution engines** — the guardrail model stays the same.

