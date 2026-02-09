# Guardrail Rollout Sequencing

Guardrails fail when they are introduced as **policy enforcement first**.
They succeed when introduced as **learning systems that gradually earn enforcement**.

This playbook describes a **sequenced, low-risk rollout model** for CI/CD guardrails.

---

## Core Rule

> **Never enforce what you cannot explain, observe, or debug.**

If teams cannot understand *why* a guardrail exists or *how* it behaves,
enforcement will create resistance and workarounds.

---

## Phase 0 — Baseline Visibility (No Enforcement)

**Goal:** Understand reality before changing behavior

Actions:
- Collect signals silently
- Observe current practices
- Identify variance across teams
- Validate signal quality

Examples:
- Capture test execution results
- Record deployment frequency
- Observe IaC policy violations (without blocking)

Guardrail posture:
- **Read-only**
- No failures
- No required changes

---

## Phase 1 — Advisory Guardrails

**Goal:** Build trust and shared understanding

Actions:
- Surface warnings in CI
- Provide actionable messages
- Document intent and rationale
- Offer examples of “good” outcomes

Examples:
- “This change bypasses feature flags”
- “This deployment lacks rollback metadata”
- “This IaC change violates policy X (non-blocking)”

Guardrail posture:
- Soft signals
- No blocking
- Clear ownership paths

---

## Phase 2 — Selective Enforcement

**Goal:** Prevent high-confidence failures

Actions:
- Enforce only deterministic rules
- Start with narrow scope
- Apply enforcement to higher-risk environments first

Examples:
- Block deploys missing rollback strategy in staging
- Fail builds with critical security misconfigurations
- Require feature flags for user-facing changes

Guardrail posture:
- Targeted enforcement
- Clear escape hatches
- Fast feedback loops

---

## Phase 3 — Policy-Driven Enforcement

**Goal:** Scale consistency without manual oversight

Actions:
- Externalize rules into policy definitions
- Standardize enforcement across pipelines
- Remove ad-hoc approvals

Examples:
- Policy-as-code for IaC
- Standard deployment contracts
- Centralized workflow templates

Guardrail posture:
- Automated
- Predictable
- Low operational overhead

---

## Phase 4 — Runtime Guardrails

**Goal:** Protect users without slowing delivery

Actions:
- Shift protection to runtime
- Integrate health signals and exposure controls
- Enable automated rollback or kill switches

Examples:
- Progressive delivery limits
- Error-rate based exposure halting
- Feature flag rollbacks

Guardrail posture:
- Always-on
- Environment-aware
- Independent of CI latency

---

## Environment Mapping

| Phase | Dev | CI | Staging | Prod |
|------|-----|----|---------|------|
| Baseline | ✔ | ✔ | ✔ | ✔ |
| Advisory | ✔ | ✔ | ✔ | ✔ |
| Selective Enforcement | | ✔ | ✔ | |
| Policy Enforcement | | ✔ | ✔ | ✔ |
| Runtime Guardrails | | | | ✔ |

---

## What NOT to Do

- Skip advisory phase
- Enforce in dev environments
- Require approvals instead of automation
- Introduce multiple guardrails at once
- Roll out without rollback paths

---

## Signals That You’re Ready to Advance a Phase

You can move forward when:
- Teams understand the “why”
- Signal quality is trusted
- Violations are rare and explainable
- Exceptions are minimal and justified

---

## Leadership Responsibilities

Leaders must:
- Fund enablement before enforcement
- Resist “just block it” instincts
- Treat guardrails as system capabilities
- Measure success by **reduced incidents**, not **increased blocks**

---

## Summary

Successful guardrails:
- Start as guidance
- Earn enforcement
- Move protection to runtime
- Disappear into delivery flow

Guardrails should feel like **safety rails**, not **roadblocks**.

