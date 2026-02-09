# Guardrail Injection Points (Overview)

This document provides a **conceptual overview** of *where* guardrails can be applied
across the software delivery lifecycle.

It intentionally avoids implementation detail and instead points to the
canonical lifecycle model.

---

## What Are Injection Points?

**Injection points** are moments in the delivery lifecycle where guardrails can:

- Evaluate risk
- Enforce policy
- Provide feedback
- Prevent unsafe promotion

They exist to **shape system behavior**, not to block teams unnecessarily.

Guardrails should:
- Activate early where possible
- Tighten progressively
- Prefer automation over approval

---

## Canonical Lifecycle View

The full lifecycle model — including *what happens at each stage* and *why guardrails belong there* — is defined in:

➡️ **[Delivery Lifecycle Injection Points](delivery-lifecycle-injection-points.md)**

That document is the **single source of truth**.

---

## Common Injection Categories (High Level)

Guardrails typically appear in these phases:

1. **Code Creation**
   - Static analysis
   - Branch protection
   - Commit hygiene

2. **Build & Validation**
   - Test coverage expectations
   - Dependency checks
   - Artifact integrity

3. **Artifact Promotion**
   - Provenance verification
   - Policy gates (automated)

4. **Deployment**
   - Environment-specific enforcement
   - Progressive rollout readiness

5. **Runtime & Operations**
   - Feature flag constraints
   - Kill-switch guarantees
   - SLO-driven rollback

6. **Signals & Feedback**
   - Drift detection
   - Guardrail effectiveness metrics

---

## Why This Document Exists

This file exists to:
- Provide a fast mental model
- Orient readers new to guardrails
- Point to deeper architectural guidance

It is **not** intended for design decisions or implementation planning.

For detail, always refer to:

➡️ **[Delivery Lifecycle Injection Points](delivery-lifecycle-injection-points.md)**

---

## Design Reminder

> Guardrails are most effective when they are:
> - Predictable
> - Progressive
> - Visible
> - Difficult to bypass, but easy to comply with

