# Provenance & Supply Chain Guardrails

## Purpose

Provenance and supply chain guardrails ensure that **only trusted, traceable, and verifiable artifacts** are allowed to move through the delivery pipeline — especially into production.

These guardrails answer a critical question:

> “Do we know *what* we are running, *where it came from*, and *how it was produced*?”

They are foundational for security, compliance, and operational trust.

---

## What These Guardrails Protect Against

Supply chain guardrails reduce risk from:

- Untrusted or tampered build artifacts
- Images built outside approved pipelines
- Dependency substitution attacks
- “Works on my machine” deployments
- Unknown build-time behavior

They protect the **integrity of delivery**, not just runtime behavior.

---

## Provenance Before Tooling

This is **not** about choosing a specific tool (SLSA, Sigstore, Cosign, etc.).

At a conceptual level, provenance guardrails enforce:

- Artifacts are built in known environments
- Builds are repeatable and auditable
- Artifact lineage is verifiable
- Promotion follows trust, not rebuilds

Trust is earned through **process**, not assumed.

---

## Core Guardrail Concepts

### 1. Artifact Identity

Every deployable artifact should have:
- A unique, immutable identifier
- A cryptographic digest
- A known build origin

Tags are convenience.
Digests are truth.

---

### 2. Build Trust Boundaries

Only artifacts produced by:
- Approved pipelines
- Trusted build systems
- Controlled environments

are allowed to proceed.

This prevents:
- Local builds
- Ad-hoc uploads
- Manual image pushes

---

### 3. Promotion, Not Rebuild

Artifacts should be:
- Built once
- Promoted across environments
- Never rebuilt for staging or production

Why:
- Rebuilds break traceability
- Promotion preserves intent
- Drift is eliminated

---

### 4. Verification at Entry Points

Artifact verification typically occurs at:
- Image pull time
- Deployment admission
- Promotion steps

Verification may check:
- Signatures
- Provenance metadata
- Policy compliance

Failures stop the pipeline, not production traffic.

---

## Enforcement Progression by Maturity

### Early Stage (Awareness)

- Artifact metadata collected
- No blocking enforcement
- Violations surfaced as warnings

Used when:
- Pipelines are inconsistent
- Teams are learning artifact discipline

---

### Intermediate Stage (Selective Enforcement)

- Only pipeline-built artifacts allowed in staging
- Signature verification enabled
- Promotion paths enforced

Used when:
- Delivery is standardized
- Risk tolerance is moderate

---

### Advanced Stage (Strict Trust)

- All production artifacts must be verified
- Unverified artifacts are rejected automatically
- Policy-as-code gates promotion

Used when:
- Regulatory, security, or safety risk is high
- Supply chain integrity is critical

---

## Environment-Based Enforcement

- **Dev**
  - Local builds allowed
  - Provenance captured but not enforced

- **Staging**
  - Only pipeline artifacts allowed
  - Verification encouraged or required

- **Production**
  - Strict verification
  - Promotion-only deployment
  - No rebuilds permitted

This avoids slowing experimentation while protecting production.

---

## Decision Ownership Model

- **Teams**
  - Own code and dependencies
  - Trigger builds
  - Consume trusted artifacts

- **Platform / Security**
  - Define trust policies
  - Operate verification systems
  - Enforce promotion rules

- **Leadership**
  - Sets acceptable risk
  - Funds automation
  - Avoids exception-driven governance

No one approves artifacts manually.

Systems enforce trust.

---

## Anti-Patterns to Avoid

- “Just push this one image”
- Rebuilding for each environment
- Trusting tags instead of digests
- Manual overrides without audit trails
- Using security tools only at runtime

Supply chain risk must be addressed **before deployment**.

---

## Relationship to Other Guardrails

Provenance guardrails connect directly to:

- **Reusable workflows**  
  Build, sign, and publish artifacts consistently

- **IaC guardrails**  
  Ensure infrastructure pulls only trusted artifacts

- **Feature flag & release guardrails**  
  Separate artifact trust from exposure control

- **Enablement dashboards**  
  Surface:
  - unverified artifact attempts
  - promotion violations
  - build source drift

---

## Why This Matters

Strong provenance guardrails:

- Reduce blast radius of compromise
- Enable faster incident response
- Improve auditability
- Increase trust in automation

They allow organizations to say:

> “If it’s running, we know exactly why we trust it.”

