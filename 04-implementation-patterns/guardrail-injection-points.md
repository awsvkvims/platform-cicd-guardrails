# Guardrail Injection Points

## Purpose

Guardrails are most effective when they are applied at the **right points in the delivery lifecycle**.

This document defines the major **injection points** where guardrails should attach, what each point protects, and what good enforcement looks like at each point.

The goal is to:
- Provide **fast feedback** early
- Apply **stricter enforcement** only where risk demands it
- Avoid central bottlenecks and late-stage surprises

---

## The Delivery Lifecycle (Where Guardrails Attach)

A typical software delivery lifecycle looks like:

1. Developer workflow (local)
2. Pull request / merge process
3. Continuous integration (build/test/analyze)
4. Artifact publication (registry / repo)
5. Deployment (environment promotion)
6. Runtime operation (post-deploy)
7. Feedback loops (metrics, incidents, learning)

Guardrails can attach at each stage — but they should not all **enforce** at each stage.

---

## Injection Point 1: Developer Workflow (Local)

**What it protects**
- Developer feedback speed
- Prevents obvious mistakes early

**Typical guardrails**
- Formatting and linting
- Pre-commit hooks
- Dependency checks (lightweight)

**Recommended enforcement**
- Local-only (non-blocking)
- Advisory by default

**One-line reason**
Local guardrails improve flow, but must not become fragile or mandatory bottlenecks.

---

## Injection Point 2: Pull Request & Merge

**What it protects**
- Shared codebase integrity
- Team coordination safety

**Typical guardrails**
- Branch protections (no direct pushes to main)
- Required reviews (risk-based)
- Required status checks (CI must pass)
- CODEOWNERS for sensitive areas

**Recommended enforcement**
- Gate/Block for mainline branches
- Warn/Observe on feature branches

**One-line reason**
Merge is the first irreversible “shared state” change — it’s the right place for governance that doesn’t slow inner-loop work.

---

## Injection Point 3: CI Pipeline (Build/Test/Scan)

**What it protects**
- Build integrity
- Test quality
- Early detection of security and policy violations

**Typical guardrails**
- Unit/integration test execution
- SAST, dependency scanning
- IaC checks (lint/validate)
- Policy evaluation (lightweight)

**Recommended enforcement**
- Warn in dev
- Gate/Block in staging/prod depending on risk

**One-line reason**
CI is where automated controls can provide fast, consistent feedback without requiring human intervention.

---

## Injection Point 4: Artifact Publication (Registry/Repo)

**What it protects**
- Supply chain integrity
- Artifact immutability and traceability

**Typical guardrails**
- Artifact signing / provenance
- Immutable tags or digest pinning
- SBOM generation and publishing
- Registry write restrictions

**Recommended enforcement**
- Block publication if provenance is missing (mature state)
- Start with observe/warn to baseline

**One-line reason**
If the artifact is unsafe or untraceable, everything downstream becomes higher risk and harder to audit.

---

## Injection Point 5: Deployment & Environment Promotion

**What it protects**
- Production stability
- Blast radius control
- Risk-based release governance

**Typical guardrails**
- Environment approvals (rare, risk-based)
- Change windows (only when truly required)
- Progressive delivery controls (canary/blue-green)
- Policy gates (e.g., “no critical vulns in prod”)

**Recommended enforcement**
- Dev: observe/warn
- Staging: warn/gate
- Prod: gate/block for high-risk controls

**One-line reason**
This is where guardrails should be strictest — because the blast radius is real.

---

## Injection Point 6: Runtime (Post-Deploy)

**What it protects**
- User experience
- Reliability and security posture over time

**Typical guardrails**
- Health checks, SLOs, error budgets
- Runtime security monitoring
- Drift detection (IaC vs actual)
- Alerting and automated rollback triggers

**Recommended enforcement**
- Not “block” (too late) — instead:
  - Alert, rollback, degrade gracefully, open incidents

**One-line reason**
Runtime guardrails are about detection and response, not prevention.

---

## Injection Point 7: Signal & Feedback Loops

**What it protects**
- Learning, improvement, and trust
- Preventing “silent failure” of guardrail programs

**Typical guardrails**
- Trend reporting (warnings, exceptions, bypass frequency)
- Platform friction signals (time-to-fix, false positives)
- Adoption signals (who is using paved roads)

**Recommended enforcement**
- No enforcement — these are signals for decision-making

**One-line reason**
Guardrails only improve systems if their outcomes feed back into platform investment and policy evolution.

---

## How Reusable Workflows Fit In

Reusable workflows are typically used at:

- PR checks (branch protections + checks)
- CI checks (build/test/scan)
- Artifact publication (signing/SBOM)
- Deployment (policy gates and release controls)

They enable guardrails to be:
- Standardized
- Versioned
- Updated safely
- Adopted without copy/paste

See: [Reusable Workflows](reusable-workflows.md)

---

## Common Failure Modes (Anti-Patterns)

1. **Blocking too early**
   - Teams fight the guardrail program
   - Adoption collapses

2. **No signals / no feedback**
   - Controls become stale
   - False positives accumulate
   - Teams bypass silently

3. **Central pipelines**
   - Platform becomes a bottleneck
   - Teams lose autonomy

4. **Approvals as default**
   - Flow slows
   - Rubber-stamping replaces safety

---

## Practical Starting Point (Recommended)

Start with these three injections first:

1. PR checks (branch protection + required CI)
2. CI checks (tests + scanning as warnings)
3. Environment promotion (risk-based gates only in prod)

Then add:
- supply chain controls
- runtime controls
- feedback dashboards

---

## Next

Now that we know **where guardrails attach**, we can define:

- how signals are emitted consistently
- how enforcement is configured by environment
- how teams consume guardrails as capabilities

→ Next: **Signals, Exceptions, and Feedback**

