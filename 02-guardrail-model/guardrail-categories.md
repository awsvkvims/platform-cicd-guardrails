# Guardrail Categories

## Purpose

This document defines the **types of controls** enforced by the CI/CD guardrail platform.

It helps answer:
- What decisions are automated vs guided?
- What risks are controlled at build vs deploy time?
- What guardrails belong in pipelines vs platforms?

These categories are **technology-agnostic** and apply across tools and clouds.

---

## Category 1 — Code & Build Integrity

**Goal:** Ensure what is built is deterministic, traceable, and reproducible.

Typical controls:
- Build reproducibility
- Dependency lockfiles
- Build environment consistency
- Artifact immutability

Typical enforcement:
- Start at Level 1 (advisory)
- Mature to Level 3 (hard gate)

Failure risk:
- Non-reproducible builds
- Undetected dependency drift
- Supply chain ambiguity

---

## Category 2 — Test & Quality Guardrails

**Goal:** Prevent changes that degrade system behavior or reliability.

Typical controls:
- Unit / integration test execution
- Coverage thresholds (used carefully)
- Contract tests
- Smoke tests before promotion

Typical enforcement:
- Level 1 → Level 3 (when tests are stable)

Anti-pattern to avoid:
- Gating on vanity coverage numbers
- Blocking without actionable failure output

---

## Category 3 — Security & Risk Controls

**Goal:** Detect and reduce risk early without stopping delivery unnecessarily.

Typical controls:
- Dependency vulnerability scanning
- SAST / IaC scanning
- Secrets detection
- Container image scanning

Typical enforcement:
- Level 0–1 initially
- Level 2 for most cases
- Level 3 only for high-confidence, high-severity risks

Key rule:
Security guardrails must optimize for **risk reduction**, not compliance theater.

---

## Category 4 — Artifact Provenance & Trust

**Goal:** Ensure deployed artifacts are authentic, traceable, and approved.

Typical controls:
- Artifact signing
- Provenance (SLSA-style)
- Promotion-only deploys
- Registry trust policies

Typical enforcement:
- Level 1 initially
- Level 3 once adoption is stable

Why this matters:
This category enables:
- Secure promotion across environments
- Auditability
- Supply chain defense

---

## Category 5 — Deployment & Promotion Controls

**Goal:** Control how changes move between environments.

Typical controls:
- Environment promotion rules
- Progressive delivery gates
- Rollback readiness checks
- Change windows (used sparingly)

Typical enforcement:
- Level 1–2 preferred
- Level 3 only for production-critical paths

Avoid:
- Manual approvals as default
- Environment-specific logic duplication

---

## Category 6 — Configuration & Policy Compliance

**Goal:** Ensure runtime environments meet baseline expectations.

Typical controls:
- Required environment variables
- Resource limits
- Runtime security policies
- Policy-as-code checks

Typical enforcement:
- Level 2–3 when deterministic
- Exceptions tracked and reviewed

---

## Category 7 — Observability & Feedback Hooks

**Goal:** Ensure systems emit signals for learning and recovery.

Typical controls:
- Health checks defined
- Deployment event emission
- Error budget tracking hooks
- Rollback signals available

Typical enforcement:
- Level 0–1 initially
- Level 2 once teams rely on signals

---

## Guardrails vs Approvals (Reminder)

Guardrails:
- Are automated
- Are consistent
- Are auditable
- Improve with time

Approvals:
- Are manual
- Are inconsistent
- Do not scale
- Hide system problems

Default to **guardrails**, not approvals.

---

## Relationship to Enforcement Levels

Each guardrail category:
- Maps to one or more enforcement levels
- Evolves independently
- Produces signals for enablement and leadership dashboards

Not all categories need to reach hard gating to be valuable.

