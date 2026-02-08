# Reuse Model: Implement Once, Consume Everywhere

## Purpose

This document explains how CI/CD guardrails should be **built as reusable components**
so that teams consume them declaratively instead of duplicating logic.

The goal is to make guardrails:
- Consistent
- Easy to adopt
- Easy to evolve
- Hard to bypass (when required)
- Low cognitive load for teams

---

## The Reuse Problem We Are Solving

Without a reuse model, organizations end up with:
- Copy-pasted pipeline YAML across repositories
- Divergent enforcement (different teams implement controls differently)
- Inconsistent audit evidence
- “Works on Team A’s pipeline but not Team B’s”
- Slow, risky rollouts of new controls

A reuse model avoids this by separating:
- **Control logic (platform-owned)**
from
- **Service pipeline intent (team-owned)**

---

## Roles and Responsibilities

### Platform / Enablement Own

- Guardrail implementation code
- Shared workflow templates
- Policy evaluation logic
- Versioning and change management
- Documentation and remediation guidance

### Teams Own

- When to run controls in their workflow (within constraints)
- What they deploy and how they test (within standards)
- Service-specific build and test details
- Local troubleshooting and fixes when guardrails fail

Key rule:
> Teams should call guardrails. They should not implement guardrails.

---

## Reuse Building Blocks (Conceptual)

A reusable model usually includes:

### 1. A “Paved Road” Template
A recommended starting workflow that includes the common controls.

- Best for: new services
- Reduces initial setup time
- Provides safe defaults

### 2. Composable Guardrail Units
Small, reusable control blocks that teams can include without duplication.

Examples:
- “Run unit tests”
- “Run dependency scan”
- “Sign artifact”
- “Promote artifact”

### 3. Central Policy Evaluation
Rules live centrally and are referenced at runtime, rather than copied into each repo.

Examples:
- Enforcement by environment
- Risk-tier strictness
- Allowed exception paths

### 4. Evidence Standardization
Guardrails emit evidence in a consistent structure so audits and reporting are automated.

---

## How This Looks in GitHub Actions (Conceptually)

In GitHub Actions, reuse is typically implemented with:

- **Reusable workflows**: called by other workflows
- **Composite actions**: packaged steps with inputs/outputs
- **Organization/repo templates**: recommended starting points
- **Branch protection rules**: ensure required checks exist
- **Environments**: allow gated deployments with audit trails

Important:
This offering is not “GitHub Actions best practices.”
GitHub Actions is one example of a reuse mechanism.

---

## Versioning Strategy for Guardrails

Guardrails must be versioned like products.

Recommended approach:
- Use semantic versions for guardrail packages
- Maintain backward compatibility for minor updates
- Use major versions for breaking changes

Why:
- Teams can adopt improvements on their timeline
- Platform teams can roll forward safely
- Changes remain auditable

---

## Rollout Safety: Avoid Breaking Everyone at Once

Guardrail changes should be rolled out progressively:

1. Add control at advisory level
2. Tune thresholds based on observed outcomes
3. Make it soft-gated for exceptions and learning
4. Only hard-gate once:
   - false positives are low
   - remediation paths exist
   - teams trust the enforcement

This keeps guardrails trusted and prevents mass bypass behavior.

---

## What “Good” Looks Like

A healthy reuse model has these properties:

- Teams write minimal pipeline YAML
- Most guardrail logic lives centrally
- Controls are consistent across repos
- Updating controls does not require editing 100+ repos
- Exceptions are rare and auditable
- Teams trust guardrails as deterministic and fair

---

## Relationship to Other Documents

- Guardrail categories (what we enforce)  
  → [Guardrail Categories](../02-guardrail-model/guardrail-categories.md)

- Enforcement maturity model (how strict)  
  → [Enforcement Levels](../02-guardrail-model/enforcement-levels.md)

- System overview (architecture layers)  
  → [Reference Architecture](system-overview.md)

