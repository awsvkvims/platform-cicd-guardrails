# Guardrails, Not Approvals

## Principle

**Safety should be encoded in systems, not enforced through human approvals.**

Approvals introduce queues, variability, and dependency on individual judgment.
Guardrails provide consistent, scalable safety without slowing delivery.

This principle replaces *centralized control* with *distributed safety*.

---

## The Problem with Approvals

Approval-based controls typically:
- Create bottlenecks and queues
- Shift accountability away from teams
- Scale poorly as the number of teams grows
- Incentivize bypass behavior (“rubber-stamping”)

Most importantly, approvals provide **late feedback** — often after work is complete.

---

## What Guardrails Are

Guardrails are **automated, policy-backed constraints** embedded directly into CI/CD workflows.

They:
- Run automatically
- Apply consistently
- Provide fast feedback
- Do not require human intervention for normal operation

Examples:
- Blocking deployment if critical security controls fail
- Warning on policy drift without stopping delivery
- Automatically enforcing artifact provenance

---

## Guardrails vs Approvals

| Dimension            | Approvals                         | Guardrails                          |
|----------------------|-----------------------------------|-------------------------------------|
| Feedback timing      | Late                              | Early                               |
| Scalability          | Poor                              | High                                |
| Consistency          | Variable                          | Deterministic                       |
| Human dependency     | Required                          | Optional (exception-based)          |
| Delivery impact      | Slows flow                        | Preserves flow                      |
| Accountability       | Centralized                       | Team-owned                          |

---

## Automation Before Escalation

A key corollary of this principle:

> **If a control requires a human to run routinely, it does not scale.**

Human review should be reserved for:
- Exceptions
- Novel risk
- Incident response
- Policy evolution

Not for:
- Every deployment
- Every pipeline
- Every change

---

## What This Principle Enables

- Faster, safer deployments
- Reduced operational toil
- Clear ownership boundaries
- Trust-based delivery models

It creates the foundation for **progressive enforcement**, where controls can warn, gate, or block based on risk.

---

## Related Principles

- **Progressive Enforcement** — not all risks require blocking
- **Fast Feedback Over Perfect Control**
- **Teams Own Delivery, Platforms Own Safety**

