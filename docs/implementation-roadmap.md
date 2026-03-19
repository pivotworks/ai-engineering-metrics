# Implementation Roadmap

[← Back to Overview](http://github.com/pivotworks/ai-engineering-metrics/blob/main/README.md)

Phased rollout from minimal investment to full visibility.

---

## Phase 1: Baseline — Week 1-2

Get signal with minimal tooling investment. No new tools required.

- [ ] **Code churn tracking** — Git access + [GitClear](https://gitclear.com) or custom scripts
- [ ] **Defect escape rate** — Defect tracker with stage tagging
- [ ] **Customer-reported bugs** — Support ticket system

**Why start here:** These three metrics give you quality signal (L2) connected to outcomes (L4) with tools you already have.

---

## Phase 2: Process Visibility — Month 1

Understand why quality metrics move.

- [ ] **Review depth tracking** — GitHub/GitLab API access
- [ ] **Guardrail freshness** — Simple git log script
- [ ] **AI attribution tagging** — Commit convention `[ai-assisted]`

**Why this matters:** Now you can trace quality problems back to process breakdowns.

---

## Phase 3: Full Stack — Month 2-3

Complete visibility across all layers.

- [ ] **Rework ratio** — Ticket hygiene discipline
- [ ] **AI override rate** — IDE telemetry or code analysis
- [ ] **Time-to-rework** — Link fixes to original commits
- [ ] **Full outcome metrics** — Product analytics integration
- [ ] **Connected dashboards** — Engineering analytics platform
- [ ] **Thresholds and alerts** — Custom configuration

**What changes:** You can now predict problems before they hit production and measure AI ROI directly.

---

## Phase 4: Calibration — Ongoing

| Quarterly | Monthly |
|:----------|:--------|
| Review thresholds | Attribution accuracy check |
| Guardrail audit | Metrics review |
| Outcome correlation analysis | |

**Why calibration matters:** Thresholds that work today won't work in six months. Teams change. Codebases change. AI tools change.

---

## Common Mistakes

| Mistake | Why It Fails | Instead |
|:--------|:-------------|:--------|
| Start with L1 (output) | Easy to measure, impossible to act on | Start with L2 + L4 connection |
| Skip L3 (process) | Can't diagnose why quality is dropping | Add process metrics in Phase 2 |
| Set thresholds once | Context changes, thresholds become noise | Quarterly calibration |
| Track everything at once | Analysis paralysis, no action | Phase implementation |

---

## Navigation

[← Diagnostic Patterns](diagnostic-patterns.md) · [What This Doesn't Solve →](what-this-doesnt-solve.md)
