# Progressive Enforcement

## Principle

**Not all risks require the same level of enforcement.**

Effective guardrails apply controls proportionally, based on risk, maturity, and context.

This principle prevents organizations from choosing between:
- Speed *or* safety  
- Autonomy *or* control  

You can have both — if enforcement is progressive.

---

## The Problem with Binary Controls

Binary enforcement models (“allow” vs “block”) lead to:
- Over-blocking low-risk changes
- Friction that teams work around
- Pressure to weaken controls entirely

When everything blocks, nothing is trusted.

---

## Progressive Enforcement Model

Controls should exist on a **spectrum**, not a switch.

Typical enforcement levels:

1. **Observe**
   - Signal is collected
   - No impact on delivery
   - Used for learning and baselining

2. **Warn**
   - Feedback is visible in CI/CD
   - Delivery continues
   - Teams are informed, not stopped

3. **Gate**
   - Explicit acknowledgement required
   - Used sparingly for elevated risk

4. **Block**
   - Deployment is prevented
   - Reserved for critical, well-understood risks

---

## Why This Matters

Progressive enforcement:
- Preserves flow while improving safety
- Allows controls to mature safely
- Builds trust with engineering teams
- Enables incremental rollout of guardrails

It also makes guardrails **evolvable**, rather than brittle.

---

## Enforcement Is a Policy Decision

Enforcement level is not a technical concern alone.

It reflects:
- Risk tolerance
- Regulatory environment
- Platform maturity
- Team capability

This is why enforcement logic belongs in **platform guardrails**, not team pipelines.

---

## How This Connects to CI/CD Guardrails

Progressive enforcement allows:
- The same control to warn today and block later
- Different enforcement levels for different environments
- Safe experimentation with new controls

This principle directly informs the **Guardrail Model** and **Implementation Patterns**.

---

## Related Principles

- **Guardrails, Not Approvals**
- **Automation Before Escalation**
- **Fast Feedback Over Perfect Control**

