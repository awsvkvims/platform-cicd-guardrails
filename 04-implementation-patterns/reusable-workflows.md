# Reusable Workflows

## Purpose

Reusable workflows are the **primary implementation mechanism** for platform CI/CD guardrails
in modern delivery platforms.

They allow guardrails to be:
- **Centrally defined**
- **Consistently applied**
- **Easily evolved**
- **Consumed voluntarily by teams**

without creating centralized pipelines or approval bottlenecks.

This document explains **why reusable workflows matter**, **what problems they solve**, and **how they should be used conceptually** — not how to implement them in a specific tool.

---

## The Problem Reusable Workflows Solve

Most organizations attempting CI/CD standardization fall into one of these traps:

- Copy-pasted pipeline templates that drift over time
- Central pipelines owned by a platform team
- Mandatory approvals that slow delivery
- “Golden paths” that teams work around instead of with

These approaches fail because they:
- Centralize ownership
- Create bottlenecks
- Scale poorly
- Erode trust

Reusable workflows address this by shifting standardization from **pipelines** to **capabilities**.

---

## What Reusable Workflows Are

Reusable workflows are **composable building blocks** that encapsulate:

- Guardrails
- Checks
- Signals
- Conventions

They are:
- Defined once
- Versioned
- Referenced by teams
- Executed in team-owned pipelines

Teams **own their pipelines**.  
Platforms **own the guardrails**.

---

## What Reusable Workflows Are Not

Reusable workflows are **not**:

- Central pipelines
- Approval gates
- Full CI/CD definitions
- One-size-fits-all templates

They should never:
- Dictate team workflow structure
- Encode business logic
- Assume a specific application architecture

Their job is to **enforce standards**, not control delivery.

---

## Why Reusable Workflows Enable Guardrails (Not Gatekeeping)

Reusable workflows enable guardrails because they:

- Run automatically
- Are applied consistently
- Do not require human approval
- Produce machine-readable signals
- Can evolve independently of team pipelines

This allows enforcement to be:
- Progressive
- Environment-aware
- Transparent

Guardrails become **part of the system**, not an external checkpoint.

---

## Ownership Model

Clear ownership boundaries are essential.

### Platform / Enablement Teams Own:
- Reusable workflow definitions
- Enforcement logic
- Signal emission
- Versioning and evolution

### Product / Delivery Teams Own:
- Pipeline composition
- Workflow sequencing
- Release decisions
- Local optimizations

This separation prevents:
- Platform teams becoming delivery bottlenecks
- Teams bypassing standards
- Endless coordination loops

---

## Progressive Adoption Model

Reusable workflows support **progressive enforcement** naturally.

Common progression:
1. Optional usage
2. Observability-only execution
3. Warning on violation
4. Blocking in higher environments

Because workflows are reusable and versioned, this progression:
- Does not require pipeline rewrites
- Does not break teams unexpectedly
- Can be communicated clearly

---

## Reusable Workflows as a Contract

A reusable workflow is a **contract**, not a control mechanism.

The contract defines:
- What is being checked
- What signals are emitted
- What happens on violation

It does **not** define:
- How teams structure their pipelines
- How teams deploy
- How teams release

Contracts build trust.  
Hidden enforcement destroys it.

---

## Relationship to Other Guardrail Mechanisms

Reusable workflows typically work alongside:
- Branch protection rules
- Infrastructure guardrails
- Policy engines
- Runtime controls

They are **one layer** in a multi-layer guardrail system.

See also:
- [Enforcement Levels](../02-guardrail-model/enforcement-levels.md)
- [Progressive Enforcement](../02-guardrail-model/progressing-enforcement.md)

---

## Design Principles for Reusable Workflows

Effective reusable workflows follow these principles:

- Small and focused
- Single responsibility
- Explicit inputs and outputs
- Observable behavior
- Versioned evolution

If a workflow is hard to explain in one paragraph, it is too complex.

---

## What Comes Next

This document establishes **why reusable workflows exist**.

Next, we define:
- **Where** guardrails attach in the delivery lifecycle
- **How** signals flow from workflows to dashboards
- **How** enforcement escalates safely

→ Next: **Guardrail Injection Points**
