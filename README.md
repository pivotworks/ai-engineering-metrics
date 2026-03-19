# The Metrics Stack for AI-Augmented Teams

> A four-layer framework for measuring what actually matters

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

If you're still measuring engineering productivity with PR count, lines of code, or even DORA metrics alone, you're measuring a world that no longer exists.

AI-augmented teams need a new metrics stack. Not because the old metrics are wrong, but because they're incomplete. They measure output. They're blind to quality, context, and the hidden costs AI creates.

---

## The Four Layers

A complete metrics stack has four layers. Most teams only have one or two.

| Layer | What It Measures | Signal Type | |
|:------|:-----------------|:------------|:--|
| **Layer 1: Output** | Volume of work produced | Lagging, easily gamed | [→ Metrics](docs/layer-1-output.md) |
| **Layer 2: Quality** | Whether the work is good | Lagging, harder to game | [→ Metrics](docs/layer-2-quality.md) |
| **Layer 3: Process** | Whether the system is healthy | Leading, diagnostic | [→ Metrics](docs/layer-3-process.md) |
| **Layer 4: Outcome** | Whether it matters to the business | Lagging, ground truth | [→ Metrics](docs/layer-4-outcome.md) |

**Key insight:** Output without quality is noise. Quality without outcome is vanity. Process metrics without the other layers are just activity tracking. You need all four layers to understand what's actually happening.

<img width="1408" height="768" alt="modern_AIAugmented_metrics_layers" src="https://github.com/user-attachments/assets/15d0dcd8-b7be-4fa3-9d0f-f29a6ddff988" />

---

## How the Layers Connect

The stack is diagnostic. When something breaks, you trace through the layers to find the cause.

```
Customer bugs spiking (L4)
         │
         ▼
Defect escape rate up (L2) ──► Code churn up (L2)
         │
         ▼
Review depth down (L3) ──► AI override rate down (L3)
         │
         ▼
    DIAGNOSIS: Rubber-stamping AI output
         │
         ▼
    FIX: Restore review process rigor
```

---

## Diagnostic Patterns

<details>
<summary><strong>Pattern 1:</strong> Customer Bugs Spiking</summary>

&nbsp;

| Layer | Signal |
|:------|:-------|
| L4 | Customer-reported bugs up 30% |
| L2 | Defect escape rate up, code churn up |
| L3 | Review depth down, AI override rate down |

**Diagnosis:** Engineers are rubber-stamping AI output. The review process has become a checkbox.

**Fix:** Set minimum review time thresholds. Require substantive comments. Slow down.

</details>

<details>
<summary><strong>Pattern 2:</strong> Output Up, Outcomes Flat</summary>

&nbsp;

| Layer | Signal |
|:------|:-------|
| L1 | PRs up 50%, deployments up 40% |
| L4 | Feature adoption flat, customer bugs unchanged |
| L2 | Rework ratio up 25% |

**Diagnosis:** You're shipping more but creating rework. Net productivity might be negative.

**Fix:** Slow PR velocity. Invest in quality gates. Track rework attribution.

</details>

<details>
<summary><strong>Pattern 3:</strong> Quality Looks Good, Incidents Rising</summary>

&nbsp;

| Layer | Signal |
|:------|:-------|
| L2 | Churn down, rework ratio stable |
| L4 | Incident frequency up 40% |
| L3 | Guardrail freshness: no updates in 90 days |

**Diagnosis:** Guardrails aren't covering new failure modes. AI is making mistakes in areas the guardrails don't address.

**Fix:** Audit guardrails against recent incidents. Add rules for new failure patterns.

</details>

<details>
<summary><strong>Pattern 4:</strong> Review Bottleneck Emerging</summary>

&nbsp;

| Layer | Signal |
|:------|:-------|
| L1 | PR volume up 60% |
| L3 | Time-to-first-review up from 2hr to 8hr, queue growing |
| L3 (predicted) | Review depth about to drop |

**Diagnosis:** AI-accelerated output is overwhelming review capacity. Quality problems coming.

**Fix:** Add review capacity. Consider automated pre-review checks. Set PR size limits.

</details>

---

## Implementation Roadmap

### Phase 1: Baseline — Week 1-2

Get signal with minimal tooling investment. No new tools required.

- [ ] **Code churn tracking** — Git access + [GitClear](https://gitclear.com) or custom scripts
- [ ] **Defect escape rate** — Defect tracker with stage tagging
- [ ] **Customer-reported bugs** — Support ticket system

### Phase 2: Process Visibility — Month 1

Understand why quality metrics move.

- [ ] **Review depth tracking** — GitHub/GitLab API access
- [ ] **Guardrail freshness** — Simple git log script
- [ ] **AI attribution tagging** — Commit convention `[ai-assisted]`

### Phase 3: Full Stack — Month 2-3

Complete visibility across all layers.

- [ ] **Rework ratio** — Ticket hygiene discipline
- [ ] **AI override rate** — IDE telemetry or code analysis
- [ ] **Time-to-rework** — Link fixes to original commits
- [ ] **Full outcome metrics** — Product analytics integration
- [ ] **Connected dashboards** — Engineering analytics platform
- [ ] **Thresholds and alerts** — Custom configuration

### Phase 4: Calibration — Ongoing

| Quarterly | Monthly |
|:----------|:--------|
| Review thresholds | Attribution accuracy check |
| Guardrail audit | Metrics review |
| Outcome correlation analysis | |

---

## What This Doesn't Solve

Metrics don't create clarity. They create the conditions for clarity if someone is willing to do the work of interpretation.

| Metric Signal | Could Mean... | Or Could Mean... |
|:--------------|:--------------|:-----------------|
| Defect escape rate up | Worse code | Better detection |
| Review depth down | Rubber-stamping | Cleaner PRs that need less feedback |
| Override rate dropping | Trust in AI | Disengagement from oversight |

**AI can:**
- Surface correlations
- Flag anomalies
- Generate hypotheses

**AI cannot:**
- Decide what matters to this team in this context
- Evaluate tradeoffs against business constraints
- Be accountable for decisions

The metrics stack gives you the data. The clarity still comes from humans who understand the context and are accountable for the decisions.

---

## The Alternative

The alternative is what most teams have now:

- PR counts on a dashboard
- Maybe DORA metrics
- A vague sense that things are either fine or not fine

AI-augmented teams shipping 2x the output with no visibility into quality, process, or outcomes. Metrics that look great while technical debt compounds. Review processes that become checkboxes. Guardrails that rot.

**Start here:**
1. Code churn
2. Defect escape rate
3. Connect to outcomes

The metrics won't tell you what to do. But they'll tell you where to look.

---

## Contributing

This framework is evolving. If you've implemented these metrics and have insights to share:

1. Open an issue describing your experience
2. Submit a PR with improvements or additions
3. Share case studies of what worked (or didn't)

Particularly interested in:
- Tooling recommendations for specific metrics
- Threshold calibration data from real teams
- Additional diagnostic patterns
- Edge cases and failure modes

---

## Related Reading

- [The Guardrail Maintenance Problem](./docs/guardrail-maintenance-problem.md) — Why AI instruction files rot like Confluence pages

---

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You're free to share and adapt with attribution.

---

## Author

**Michaela Glaze**  
Fractional CTO and founder of [PivotWorks Consulting](https://pivotworks.io), specializing in execution risk prevention and delivery stabilization for post-PMF B2B SaaS companies.

- [LinkedIn](https://linkedin.com/in/michaelaglaze)
- [Substack: Invisible Failure](https://invisiblefailure.substack.com)

---

*If this framework helped your team, consider giving the repo a ⭐*
