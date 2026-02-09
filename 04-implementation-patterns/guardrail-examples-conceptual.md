# Guardrail Examples (Conceptual)

This section provides **concrete examples** of how different guardrail policy types
are applied in real delivery systems.

These examples are **technology-agnostic** and focus on:
- Intent
- Enforcement progression
- Decision ownership

For the conceptual taxonomy behind these examples, see:
→ [Policy Types Deep Dive](../../02-guardrail-model/policy-types.md)

---

## Example 1: Infrastructure-as-Code (IaC) Guardrails

**Policy Type:** Infrastructure Safety  
**Primary Risk:** Irreversible or unsafe infrastructure changes

### Early Maturity
- Terraform plans are generated automatically
- Drift is detected and reported
- No enforcement; teams learn what “unsafe” looks like

**Outcome:** Visibility without disruption

---

### Growing Maturity
- Certain destructive changes (e.g., deleting stateful resources) require justification
- Guardrail blocks only *high-risk* operations
- Overrides are logged, not approved

**Outcome:** Safer defaults without slowing delivery

---

### High Maturity
- Production infrastructure changes require:
  - Approved change windows *or*
  - Progressive rollout patterns
- Guardrails are environment-aware (dev ≠ prod)

**Outcome:** Risk is controlled without central approvals

---

## Example 2: Build Provenance & Supply Chain Guardrails

**Policy Type:** Provenance & Integrity  
**Primary Risk:** Untrusted or tampered artifacts

### Early Maturity
- Build metadata is captured (who, what, when)
- Provenance is visible but not enforced

**Outcome:** Transparency without friction

---

### Growing Maturity
- Deployments warn when provenance is missing
- Non-compliant artifacts are allowed with audit trails

**Outcome:** Teams learn expectations before enforcement

---

### High Maturity
- Production deploys require verified provenance
- Non-compliant artifacts are blocked automatically
- Overrides require post-incident review, not pre-approval

**Outcome:** Supply-chain security without gatekeeping

---

## Example 3: Feature Flags & Release-on-Demand Guardrails

**Policy Type:** Release Safety  
**Primary Risk:** Unsafe customer exposure and blast radius

### Early Maturity
- Feature flags are encouraged but optional
- No guardrails; learning phase

**Outcome:** Adoption without mandate

---

### Growing Maturity
- Production releases require:
  - Flags for high-risk features
  - Ability to disable without redeploy
- Guardrails warn when flags are missing

**Outcome:** Safer releases with team autonomy

---

### High Maturity
- Progressive delivery is required for:
  - Customer-facing changes
  - Schema-impacting releases
- Guardrails enforce:
  - Percentage rollout
  - Blast-radius limits
  - Automatic rollback triggers

**Outcome:** Release confidence at scale

---

## Example 4: Branch Protection as a Guardrail (Not Approval)

**Policy Type:** Change Integrity  
**Primary Risk:** Bypassing quality and security checks

### Anti-Pattern
- Manual approvals required for every merge
- Central reviewers become bottlenecks

---

### Guardrail-Based Approach
- Required checks are enforced automatically
- No human approval required if checks pass
- Overrides are logged and reviewed asynchronously

**Outcome:** Quality enforcement without slowing flow

---

## Key Pattern Across All Examples

Across all policy types:

- Guardrails **progress over time**
- Enforcement is **context-aware**
- Humans are removed from the critical path
- Overrides are **audited, not approved**

Guardrails protect the system — they do not police teams.

---

## What Comes Next

These conceptual examples will later be mapped to:
- Reusable workflows
- Policy-as-code patterns
- Environment-specific enforcement

Without changing the underlying intent.

