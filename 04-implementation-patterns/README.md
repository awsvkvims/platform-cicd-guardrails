# Implementation Patterns

This section describes **how guardrails are implemented in real CI/CD systems**
without prescribing tools, vendors, or pipelines.

The goal is to show:
- Where guardrails live
- How they are injected safely
- How enforcement increases over time

---

## Recommended Starting Point

If you are new to this repository, start here:

1. **Reusable Workflows**  
   → [`reusable-workflows.md`](reusable-workflows.md)  
   How platforms encode guardrails once and reuse them everywhere

2. **Guardrail Injection Points**  
   → [`guardrail-injection-points.md`](guardrail-injection-points.md)  
   Where guardrails sit across the delivery lifecycle

3. **Guardrail Examples**  
   → [`guardrail-examples.md`](guardrail-examples.md)  
   Concrete examples of policy types and enforcement patterns

These patterns scale from:
- Advisory → Soft enforcement → Hard enforcement
- Dev → Staging → Production
