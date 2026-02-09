# Infrastructure as Code (IaC) Guardrails

## Purpose

Infrastructure as Code guardrails ensure that **environment changes are intentional, reviewable, reversible, and safe** — without relying on manual approvals or heroics.

These guardrails:
- Prevent configuration drift
- Reduce production risk
- Enable safe self-service
- Shift infrastructure control from people to systems

They form the backbone of scalable platform operations.

---

## What These Guardrails Protect

IaC guardrails protect against:

- Manual, undocumented changes in shared environments
- Configuration drift between environments
- Irreversible infrastructure changes
- Privileged access bypassing delivery workflows
- Late discovery of security or cost risks

They help organizations answer:

> “Can we change infrastructure confidently without slowing teams down?”

---

## Guardrail Intent (Before Tooling)

IaC guardrails are **not about Terraform vs CloudFormation vs Pulumi**.

They are about enforcing **change discipline** and **environment integrity**.

At a conceptual level, they enforce:

- Declarative infrastructure
- Version-controlled changes
- Automated validation before apply
- Auditable change history
- Predictable rollback paths

---

## Common Policy Rules (Conceptual)

Typical IaC guardrail rules include:

- Infrastructure changes must be made via code
- Production changes must come from a trusted pipeline
- Direct console changes are disallowed or monitored
- Destructive changes require explicit intent
- Environment parity must be maintained

These are behavioral contracts, not tooling constraints.

---

## Enforcement Progression by Maturity

### Early Stage (Visibility First)

- IaC recommended but not enforced
- Drift detection enabled
- Warnings surfaced in pipelines or dashboards

Used when:
- Teams are learning IaC
- Legacy environments exist

---

### Intermediate Stage (Controlled)

- Infrastructure changes must go through pipelines
- Drift detection triggers alerts
- Production changes require code review
- Manual changes logged and escalated

Used when:
- Platform maturity is growing
- Risk tolerance is decreasing

---

### Advanced Stage (Strict)

- All infrastructure changes must be IaC-driven
- Console access heavily restricted or removed
- Drift triggers automatic remediation or rollback
- Policy-as-code validates plans before apply

Used when:
- Environments are business-critical
- Compliance and reliability are high priority

---

## Environment-Based Enforcement

IaC guardrails tighten across environments:

- **Dev**
  - Rapid experimentation allowed
  - Fewer restrictions
  - Drift tolerated temporarily

- **Staging**
  - Change validation enforced
  - Parity with production expected

- **Production**
  - Strict pipeline-only changes
  - Drift prevention enforced
  - Rollback paths required

This progression prevents friction while protecting critical systems.

---

## Decision Ownership Model

IaC guardrails intentionally separate concerns:

- **Teams**
  - Define required infrastructure
  - Propose changes via code
  - Own service behavior

- **Platform Teams**
  - Own pipelines and validation
  - Define allowed patterns
  - Prevent unsafe changes

- **Leadership**
  - Sets risk tolerance
  - Funds automation
  - Avoids approving individual changes

Ownership is clear, but responsibility is shared.

---

## Anti-Patterns to Avoid

These patterns undermine IaC guardrails:

- “Break-glass” access as a normal workflow
- Emergency console changes without reconciliation
- Treating IaC as documentation instead of control
- Excessive approval steps replacing automation
- Environment-specific snowflakes

Guardrails should reduce toil, not increase it.

---

## Relationship to Other Guardrails

IaC guardrails connect directly to:

- **Reusable workflows**  
  Enforce validation, plan review, and apply rules

- **Delivery lifecycle injection points**  
  Typically enforced at:
  - plan generation
  - pre-apply validation
  - production apply

- **Enablement dashboards**  
  Surface:
  - drift frequency
  - failed applies
  - rollback activity

---

## Why This Matters

Organizations with strong IaC guardrails:

- Recover faster from incidents
- Scale platforms safely
- Reduce dependency on individuals
- Enable teams without sacrificing control

IaC guardrails are not about locking things down.

They are about **making the safest path the default path**.

