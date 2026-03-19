# Diagnostic Patterns

[← Back to Overview](http://github.com/pivotworks/ai-engineering-metrics/blob/main/README.md)

Common failure modes and how to fix them.

---

## Pattern 1: Customer Bugs Spiking

| Layer | Signal |
|:------|:-------|
| L4 | Customer-reported bugs up 30% |
| L2 | Defect escape rate up, code churn up |
| L3 | Review depth down, AI override rate down |

**Diagnosis:** Engineers are rubber-stamping AI output. The review process has become a checkbox.

**Fix:** Set minimum review time thresholds. Require substantive comments. Slow down.

---

## Pattern 2: Output Up, Outcomes Flat

| Layer | Signal |
|:------|:-------|
| L1 | PRs up 50%, deployments up 40% |
| L4 | Feature adoption flat, customer bugs unchanged |
| L2 | Rework ratio up 25% |

**Diagnosis:** You're shipping more but creating rework. Net productivity might be negative.

**Fix:** Slow PR velocity. Invest in quality gates. Track rework attribution.

---

## Pattern 3: Quality Looks Good, Incidents Rising

| Layer | Signal |
|:------|:-------|
| L2 | Churn down, rework ratio stable |
| L4 | Incident frequency up 40% |
| L3 | Guardrail freshness: no updates in 90 days |

**Diagnosis:** Guardrails aren't covering new failure modes. AI is making mistakes in areas the guardrails don't address.

**Fix:** Audit guardrails against recent incidents. Add rules for new failure patterns.

---

## Pattern 4: Review Bottleneck Emerging

| Layer | Signal |
|:------|:-------|
| L1 | PR volume up 60% |
| L3 | Time-to-first-review up from 2hr to 8hr, queue growing |
| L3 (predicted) | Review depth about to drop |

**Diagnosis:** AI-accelerated output is overwhelming review capacity. Quality problems coming.

**Fix:** Add review capacity. Consider automated pre-review checks. Set PR size limits.

---

## Quick Reference

| Symptom | First Check | Second Check |
|:--------|:------------|:-------------|
| Customer bugs up | L2 defect escape rate | L3 review depth |
| Incidents up | L3 guardrail freshness | L2 code churn |
| Rework up | L3 AI override rate | L2 time-to-rework |
| Review queue growing | L1 PR volume | L3 review capacity |

---

## Navigation

[← How the Layers Connect](how-layers-connect.md) · [Implementation Roadmap →](implementation-roadmap.md)
