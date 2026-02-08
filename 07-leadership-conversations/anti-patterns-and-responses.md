# Anti-Patterns and Guardrail Responses

## Purpose

This document captures common enterprise anti-patterns that appear when organizations try to scale CI/CD safely.

For each anti-pattern, it provides:
- What typically happens
- Why it fails at scale
- The guardrail-based alternative
- A leadership-safe way to explain it

---

## Anti-Pattern 1: “Just Require Approvals”

### What Happens
Leadership introduces required approvals for deployments or PR merges as a primary risk control.

### Why It Fails
- Approvals do not scale with volume
- Reviewers become bottlenecks
- Approval quality degrades under load
- Teams route around the process (hotfixes, exceptions, shadow pipelines)
- It shifts accountability from systems to individuals

### Guardrail Alternative
Use **automated, deterministic gates**:
- Tests must pass
- Scans must meet policy thresholds
- Artifacts must be signed/proven
- Deployments must emit evidence

Reserve human approvals for:
- rare emergency exceptions
- truly high-risk changes (limited scope, auditable)

### How I Explain It
Approvals answer: “Do I trust you?”  
Guardrails answer: “Is this change safe?”

At scale, we need systems that verify safety, not humans that guess trust.

---

## Anti-Pattern 2: Copy-Paste Pipelines

### What Happens
Teams duplicate pipeline YAML from other repos and modify it until it works.

### Why It Fails
- Enforcement diverges quickly
- Controls are missing in some repos
- Updates require changing dozens of pipelines
- Audits become manual evidence hunts

### Guardrail Alternative
Implement controls once as reusable components:
- reusable workflows / templates
- shared policy evaluation
- standard evidence outputs

### How I Explain It
If the org has 200 repos, we should not have 200 versions of “how we do security scans.”

---

## Anti-Pattern 3: “Security Owns the Pipeline”

### What Happens
Security teams control or centrally operate CI/CD gates to ensure compliance.

### Why It Fails
- Security becomes the release bottleneck
- Security engineers end up doing operational work
- Ownership conflicts increase (who fixes pipeline failures?)
- Teams stop trusting security as a partner

### Guardrail Alternative
Security defines intent and risk thresholds.  
Platform implements enforcement in guardrails.  
Teams remediate failures.

### How I Explain It
Security should define *what must be true*.  
The platform should make it true by default.

---

## Anti-Pattern 4: Hard Gates Too Early

### What Happens
Controls are made blocking before they are stable, tuned, or understood.

### Why It Fails
- False positives create distrust
- Delivery stops
- Teams bypass the platform
- Controls are disabled under pressure

### Guardrail Alternative
Progress enforcement intentionally:
- Observe → Advisory → Soft gate → Hard gate

### How I Explain It
A guardrail must earn trust before it earns authority.

---

## Anti-Pattern 5: Exceptions Become the Default

### What Happens
Teams frequently bypass controls via manual exceptions, and exceptions accumulate without review.

### Why It Fails
- Risk becomes invisible
- “Compliance” becomes performative
- Audit exposure increases
- Leaders can’t tell what’s actually enforced

### Guardrail Alternative
Make exceptions:
- rare
- time-bound
- auditable
- visible as signals for investment

### How I Explain It
Exceptions are not failures — they are signals that the system needs improvement.
But if exceptions are common, the guardrail isn’t working.

---

## Anti-Pattern 6: Metrics Used as Judgment

### What Happens
Guardrail failure counts are used to rank teams or evaluate performance.

### Why It Fails
- Teams hide failures
- People optimize appearances, not safety
- Trust collapses
- Signal quality drops

### Guardrail Alternative
Use guardrail signals to:
- identify systemic constraints
- prioritize enablement investment
- reduce risk over time

### How I Explain It
If guardrail failures are used for judgment, teams will stop letting the system be honest.

