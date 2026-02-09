# Guardrail Examples in CI/CD Pipelines

## Purpose

This document shows concrete CI/CD examples of guardrails in action.

Each example demonstrates:
- Where the guardrail runs
- What risk it addresses
- How it evolves with maturity
- How it replaces approvals without slowing teams

Examples are intentionally tool-agnostic and simplified.

---

## Example 1: Feature Flag Guardrail (Release-on-Demand)

### Risk Addressed
High-risk code changes deployed directly to users without rollback control.

### Early Maturity (Advisory)

```yaml
- name: Check for feature flags
  run: |
    if grep -R "new_checkout_flow" src/; then
      echo "WARNING: High-risk path detected without feature flag"
    fi
```

Outcome:
- Pipeline passes
- Signal is logged
- Teams learn expectations

---

### Growing Maturity (Soft Enforcement)

```yaml
- name: Validate feature flags
  run: |
    if grep -R "new_checkout_flow" src/ &&        ! grep -R "FEATURE_FLAG_CHECKOUT" src/; then
      echo "ERROR: Feature flag required for high-risk path"
      exit 1
    fi
```

Outcome:
- Production deploys blocked
- Non-prod remains open
- No approvals required

---

### Advanced Maturity (Policy-Based)

```yaml
- name: Enforce rollout strategy
  run: |
    jq -e '.rollout.strategy == "progressive"' release.json
```

Outcome:
- Rollout strategy enforced automatically
- Leadership intent encoded as policy

---

## Example 2: Infrastructure-as-Code Guardrail

### Risk Addressed
Manual or unsafe infrastructure changes in production.

### Early Maturity (Visibility)

```yaml
- name: Detect IaC changes
  run: terraform plan -out=tfplan
```

Outcome:
- Drift becomes visible
- No blocking

---

### Growing Maturity (Risk-Aware Blocking)

```yaml
- name: Block destructive changes
  run: |
    terraform show -json tfplan | jq '.resource_changes[]
      | select(.change.actions | index("delete"))' && exit 1
```

Outcome:
- High-risk changes blocked
- Low-risk changes proceed

---

### Advanced Maturity (Auto-Promotion)

```yaml
- name: Auto-apply safe changes
  if: env.ENVIRONMENT != 'prod'
  run: terraform apply -auto-approve tfplan
```

Outcome:
- Safety encoded in pipeline
- Approvals eliminated

---

## Example 3: Provenance & Artifact Guardrails

### Risk Addressed
Untrusted or untraceable artifacts reaching production.

### Early Maturity (Recording)

```yaml
- name: Record build metadata
  run: |
    echo "commit=$GITHUB_SHA" >> provenance.txt
```

Outcome:
- Traceability exists
- No enforcement

---

### Growing Maturity (Verification)

```yaml
- name: Verify artifact source
  run: |
    test "$(cat provenance.txt | grep commit)" || exit 1
```

Outcome:
- Foreign artifacts blocked
- Supply chain hardened

---

### Advanced Maturity (Policy Enforcement)

```yaml
- name: Enforce signed artifacts
  run: cosign verify artifact:latest
```

Outcome:
- Trust becomes provable
- Compliance automated

---

## Why This Matters

These examples show that:
- Guardrails scale better than approvals
- Safety can be enforced without slowing delivery
- Maturity is incremental, not disruptive

Guardrails work best when:
- Applied late, not early
- Based on risk, not rules
- Owned by platforms, not teams

---

## Related Reading

- Guardrail model  
  `02-guardrail-model/enforcement-levels.md`

- Delivery lifecycle injection points  
  `04-implementation-patterns/delivery-lifecycle-injection-points.md`

- Leadership framing  
  `07-leadership-conversations/how-i-explain-this-in-10-min.md`
