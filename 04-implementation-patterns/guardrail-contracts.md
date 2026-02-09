# Guardrail Contracts: Signals, Exceptions, and Evidence

## Purpose

Guardrails succeed when they behave like reliable platform capabilities:
- predictable inputs
- predictable outputs
- explainable failures
- traceable exceptions

This document defines the **contract** that guardrail workflows should follow so that:
- teams can debug quickly,
- platform teams can evolve guardrails safely,
- security/audit stakeholders can trust evidence without adding manual gates.

---

## The Contract (High-Level)

Every guardrail should provide:

1. **Signals**  
   What the guardrail observed and concluded

2. **Exceptions**  
   How a rule can be bypassed intentionally and safely

3. **Evidence**  
   The artifacts/logs that prove what happened (for audit and learning)

---

## 1) Signals

Signals are the guardrail outputs that answer:

> “What did the system observe, and what does it mean?”

Signals must be:
- **human-readable** (for teams)
- **machine-readable** (for reporting/automation)
- **stable over time** (avoid frequent renaming)

### Signal Severity Levels

Use a small consistent set:

- **PASS** — compliant
- **WARN** — non-compliant but allowed (early maturity or low risk)
- **FAIL** — non-compliant and blocked (high risk / higher env)
- **INFO** — contextual, not evaluative

### Required Signal Fields

Each emitted signal should include:

- **guardrail_id**: stable identifier (e.g., `artifact.provenance`, `iac.tags`, `release.flags`)
- **severity**: PASS/WARN/FAIL/INFO
- **summary**: one-line outcome
- **details**: short explanation (what failed and why)
- **environment**: dev/staging/prod (or equivalent)
- **decision_context**: PR / build / promote / deploy / runtime
- **remediation_hint**: what to do next
- **links**: pointer to internal docs/playbooks

### Example Signal (Conceptual)

- guardrail_id: `release.flags.required`
- severity: `FAIL`
- summary: `Missing feature flag for user-impacting change`
- details: `Changes to /checkout path require a runtime disablement mechanism.`
- environment: `staging`
- decision_context: `promote`
- remediation_hint: `Add a feature flag defaulting OFF and declare rollout strategy.`
- links: `04-implementation-patterns/release-on-demand.md` (future)

---

## 2) Exceptions

Exceptions are not a loophole — they are a **designed control**.

> “We allow bypass, but we do not allow invisibility.”

### Exception Requirements (Non-Negotiable)

Every exception must be:

- **Explicit** (declared, not implied)
- **Scoped** (to a specific rule, env, repo, or timeframe)
- **Time-bound** (expires automatically)
- **Traceable** (who/what/why captured)
- **Observable** (emits signals)

### Exception Capture Fields

- **exception_id** (unique)
- **guardrail_id** (what is being bypassed)
- **scope** (repo/service/env/commit range)
- **reason_category** (e.g., incident, migration, flaky-check, vendor-outage)
- **reason_text** (short human explanation)
- **owner** (person/team accountable)
- **expires_at** (required)
- **created_at**
- **approval_mode** (acknowledgement vs approval)

### Preferred Exception Types

#### A) Acknowledgement-based (preferred)
User acknowledges increased risk; no manual approver required.

Use when:
- risk is understood
- mitigation exists
- speed matters

#### B) Approval-based (rare)
Requires explicit approval.

Use when:
- regulatory policy demands it
- risk is extreme
- blast radius is large

Manual approvals should be **exceptional**, not default workflow design.

---

## 3) Evidence

Evidence is what proves guardrails ran and what they concluded.

> “Audit should be a byproduct of delivery, not an additional workflow.”

### Evidence Sources

Depending on stage, evidence may include:
- CI job logs (checks + decisions)
- Policy evaluation outputs
- Signed artifact metadata
- SBOM / provenance attestation
- Deployment records (who/what/when)
- Runtime rollback/flag disable events

### Evidence Characteristics

Evidence should be:
- immutable where possible
- retained long enough for audit needs
- easy to retrieve by commit SHA / artifact digest

### Evidence Index (Recommended)

Organizations often standardize an evidence “index” keyed by:
- commit SHA
- artifact digest
- environment
- timestamp

This enables traceability without approvals.

---

## Progressive Enforcement (Contract Compatibility)

This contract supports progressive enforcement because the same guardrail can emit:

- INFO/WARN in dev
- WARN/FAIL in staging
- FAIL in prod

…without changing the guardrail’s identity or semantics.

Only the enforcement threshold changes.

---

## Anti-Patterns

Avoid:
- silent bypass
- exceptions with no expiry
- “contact platform team” as remediation hint
- changing guardrail IDs frequently
- coupling evidence to manual approvals

---

## Relationship to Other Docs

- Injection points: `04-implementation-patterns/delivery-lifecycle-injection-points.md`
- Signals/exceptions feedback model: `04-implementation-patterns/signals-exceptions-feedback.md`
- Environment progression: `02-guardrail-model/environment-progression.md`
- Rollout sequencing: `06-rollout-playbooks/guardrail-rollout-sequencing.md`

---

## Key Takeaway

Guardrails scale when they behave like platform products:
- predictable
- explainable
- traceable
- progressively enforceable

