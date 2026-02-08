# Enforcement Levels

## Purpose

This document defines **how guardrails are enforced over time**, from advisory feedback
to non-bypassable controls.

It helps the organization answer:

- What is mandatory today?
- What is recommended but optional?
- How do we evolve controls without breaking delivery?

This avoids two common failures:
- **All controls optional** → inconsistent compliance and audit risk
- **All controls mandatory immediately** → teams bypass, fork, or stall delivery

---

## The 4 Enforcement Levels

### Level 0 — Visibility Only (Observe)
**Meaning:** The system measures or detects, but does not inform or block.

Examples:
- Record deployment events
- Capture scan results but don’t report them
- Collect evidence silently for later analysis

Use when:
- You need baseline data
- You suspect controls will be noisy
- You want to quantify impact before acting

---

### Level 1 — Advisory (Inform)
**Meaning:** The system reports issues and provides guidance, but does not block.

Examples:
- “Vulnerability found — here’s the remediation link”
- “No tests detected — recommended minimum is X”
- “Artifact not signed — this will become required”

Use when:
- Teams need time to adopt new practices
- Controls need tuning
- You want learning before enforcement

---

### Level 2 — Soft Gate (Warn + Escalate)
**Meaning:** The system does not block immediately, but requires acknowledgment or creates a tracked exception.

Examples:
- Allow deploy, but:
  - open an exception ticket automatically
  - require a risk acknowledgment in PR
  - alert enablement/security when thresholds exceeded

Use when:
- Risk is real but not catastrophic
- You need enforceable accountability without stoppage
- You want exception data for leadership decisions

---

### Level 3 — Hard Gate (Block)
**Meaning:** The system blocks promotion/deploy until the guardrail passes.

Examples:
- Block if:
  - critical vulnerabilities exceed threshold
  - required test suite fails
  - artifact lacks provenance/signature
  - required approvals (rare) are missing for high-risk paths

Use when:
- The control is proven, low-noise, and non-negotiable
- You have remediation paths documented
- Teams trust the guardrail is fair and deterministic

---

## Key Rule: Don’t Hard-Gate Without a Remediation Path

Hard gates must provide:
- Clear failure reason
- Direct remediation guidance
- Links to docs/playbooks
- A defined exception path (rare, auditable)

If developers cannot fix it quickly, the gate becomes a bottleneck and will be bypassed.

---

## How Controls Move Between Levels

A typical progression:

1. Level 0 (observe) → baseline data, tune thresholds
2. Level 1 (advisory) → education + adoption
3. Level 2 (soft gate) → exceptions generate investment signals
4. Level 3 (hard gate) → stable enforcement at scale

Not all controls must reach Level 3.

---

## Examples of Controls and Their Typical Levels

| Control | Typical start | Typical end |
|--------|---------------|-------------|
| Unit tests executed | L1 | L3 |
| Dependency vulnerability scanning | L1 | L2/L3 |
| SAST scanning | L0/L1 | L2 |
| Artifact signing/provenance | L1 | L3 |
| Manual approval | L0 | L0/L1 (avoid) |

---

## Relationship to Dashboards

Enforcement levels create measurable signals for leaders:

- High volume of soft-gate exceptions → system constraint or missing enablement
- Rising hard-gate failures → training gap or tech debt
- Low failure + high throughput → healthy guardrail design

These signals should never be used to rank teams.
They exist to guide platform and enablement investment.

