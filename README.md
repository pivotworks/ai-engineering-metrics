# The Metrics Stack for AI-Augmented Teams

> A four-layer framework for measuring what actually matters

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

If you're still measuring engineering productivity with PR count, lines of code, or even DORA metrics alone, you're measuring a world that no longer exists.

AI-augmented teams need a new metrics stack. Not because the old metrics are wrong, but because they're incomplete. They measure output. They're blind to quality, context, and the hidden costs AI creates.

---

## Table of Contents

- [The Four Layers](#the-four-layers)
- [Layer 1: Output Metrics](#layer-1-output-metrics)
- [Layer 2: Quality Metrics](#layer-2-quality-metrics)
- [Layer 3: Process Metrics](#layer-3-process-metrics)
- [Layer 4: Outcome Metrics](#layer-4-outcome-metrics)
- [How the Layers Connect](#how-the-layers-connect)
- [Diagnostic Patterns](#diagnostic-patterns)
- [Implementation Roadmap](#implementation-roadmap)
- [What This Doesn't Solve](#what-this-doesnt-solve)
- [Contributing](#contributing)

---

## The Four Layers

A complete metrics stack has four layers. Most teams only have one or two.

| Layer | What It Measures | Signal Type |
|:------|:-----------------|:------------|
| **Layer 1: Output** | Volume of work produced | Lagging, easily gamed |
| **Layer 2: Quality** | Whether the work is good | Lagging, harder to game |
| **Layer 3: Process** | Whether the system is healthy | Leading, diagnostic |
| **Layer 4: Outcome** | Whether it matters to the business | Lagging, ground truth |

**Key insight:** Output without quality is noise. Quality without outcome is vanity. Process metrics without the other layers are just activity tracking. You need all four layers to understand what's actually happening.

<img width="1408" height="768" alt="modern_AIAugmented_metrics_layers" src="https://github.com/user-attachments/assets/15d0dcd8-b7be-4fa3-9d0f-f29a6ddff988" />

---

## Layer 1: Output Metrics

**Purpose:** Measure volume of work. Use for context, not evaluation.

These metrics are easy to collect and easy to game. AI has made them trivially inflatable. The creator of Claude Code pushes 50 to 100 PRs per week using parallel AI agents. That's not a criticism of his productivity. It's a signal that PR count no longer means what it used to mean.

| Metric | What It Measures | How to Track | Limitations |
|:-------|:-----------------|:-------------|:------------|
| **PR count / merge frequency** | How much code is shipping | Native in GitHub/GitLab | Inflated by AI, gameable by splitting work |
| **Deployment frequency** | How often you release to production | CI/CD pipeline logs, DORA tooling | More deployments only good if deployments are good |
| **Commit frequency** | Activity signal | Git log analysis | Tells you nothing about value |
| **Lines of code** | Volume of code changes | Git diff analysis, GitClear | Best work often reduces LOC |

### Usage Guidelines

- ✅ Track at team level, not individual
- ✅ Use trend lines, not absolutes
- ✅ Treat as context for other metrics
- ❌ Don't use for standalone evaluation
- ❌ Don't evaluate engineers based on PR count

> **⚠️ Warning sign:** If Layer 1 metrics are your primary dashboard, you're measuring activity, not productivity.

---

## Layer 2: Quality Metrics

**Purpose:** Measure whether the work is actually good. This is where AI-generated problems surface.

These metrics require more infrastructure to track but are much harder to game. They catch what output metrics miss: code that shipped fast but shouldn't have, work that creates more work, and the hidden costs of speed.

### Metrics at a Glance

| Metric | Target | Key Signal |
|:-------|:-------|:-----------|
| [Code Churn Rate](#code-churn-rate) | <10% | Shipping fast but creating rework |
| [Rework Ratio](#rework-ratio) | <15% | Hidden costs of AI-generated code |
| [Time-to-Rework](#time-to-rework) | >30 days | Review process not catching issues |
| [Defect Escape Rate](#defect-escape-rate) | Trending ↓ | Tests not catching what matters |
| [Defect Attribution](#defect-attribution) | Baseline first | AI ROI analysis foundation |

---

#### Code Churn Rate

Lines reverted or modified within 14-21 days.

**Why it matters:** GitClear research projects code churn will double by 2026 due to AI-generated code. High churn means you're shipping faster but creating rework.

| | |
|:--|:--|
| **Formula** | `(lines modified within window / total lines committed) * 100` |
| **Target** | Below 10% for mature codebases. Above 15% indicates systemic issues. |
| **How to track** | Git analysis comparing commits to subsequent modifications. [GitClear](https://gitclear.com) provides this out of the box. |

---

#### Rework Ratio

Percentage of effort spent fixing previous work.

**Why it matters:** AI can inflate output while creating hidden rework costs. If you ship twice as much but spend 40% of your time fixing it, you're not ahead.

| | |
|:--|:--|
| **Formula** | `(story points on rework tickets / total story points) * 100` |
| **Target** | Below 15% of total effort. Spikes above 25% indicate quality problems upstream. |
| **How to track** | Tag tickets/PRs as "rework," "fix," "bugfix," or link to original implementation. |

---

#### Time-to-Rework

How long code survives before requiring intervention.

**Why it matters:** Short time-to-rework means the review process isn't catching issues. The code looked fine, passed review, then broke quickly.

| | |
|:--|:--|
| **Formula** | `median(first_fix_timestamp - merge_timestamp)` for commits requiring fixes |
| **Target** | Greater than 30 days = acceptable. Under 7 days = significant problems. |
| **How to track** | Track time delta between initial merge commit and first fix commit touching the same files/functions. |

---

#### Defect Escape Rate

Bugs found in production vs. caught during development.

**Why it matters:** If production defect rate is rising while test coverage looks good, your tests aren't catching what matters.

| | |
|:--|:--|
| **Formula** | `(production defects / total defects) * 100` |
| **Target** | Trending down over time. Absolute numbers depend on your context. |
| **How to track** | Defect tracking with stage attribution. Tag where defects were found: unit test, integration test, QA, staging, production. |

---

#### Defect Attribution

Which defects trace to AI-generated vs. human-written code.

**Why it matters:** Without this, you can't evaluate whether AI is helping or creating hidden costs. This is the baseline for any AI ROI analysis.

| | |
|:--|:--|
| **Implementation** | Add `[ai-assisted]` or `[ai-generated]` tags to commits. Build reporting that segments defect rates by tag. |
| **How to track** | Tag AI-generated code at commit time. Add metadata or commit message conventions. Then link defects to originating commits. |

---

### Layer 2 Usage Guidelines

- Compare AI-generated versus human-generated code quality once you have attribution
- Identify patterns: certain types of AI-generated work that consistently need rework
- Set thresholds that trigger process changes

> **⚠️ Warning sign:** Quality metrics flat while output metrics spike means you're creating future problems at an accelerated rate.

---

## Layer 3: Process Metrics

**Purpose:** Measure whether humans are actually engaged or just rubber-stamping. These are leading indicators that predict quality problems before they surface in production.

### Metrics at a Glance

| Metric | Target | Key Signal |
|:-------|:-------|:-----------|
| [Review Depth](#review-depth) | ≥1 comment/PR | Humans disengaging from oversight |
| [AI Override Rate](#ai-override-rate) | 20-40% | Rubber-stamping vs. healthy skepticism |
| [Guardrail Freshness](#guardrail-freshness) | <30 days | AI following outdated instructions |
| [Guardrail Coverage](#guardrail-coverage) | Audit quarterly | System not learning from mistakes |
| [Time-to-First-Review](#time-to-first-review) | <4 hours | Review bottleneck forming |
| [Review Queue Depth](#review-queue-depth) | Stable/declining | Pressure to rubber-stamp building |

---

#### Review Depth

Substantive engagement vs. rubber-stamping.

**Why it matters:** If review depth drops while output rises, humans are disengaging from oversight. The review becomes a checkbox, not a quality gate.

| | |
|:--|:--|
| **Target** | Average ≥1 substantive comment per PR. >30% PRs approved without comments = warning sign. |
| **How to track** | GitHub/GitLab APIs: comments per PR, changes requested, review time. |

**Signals to track:**
- Comments per PR (excluding bot comments)
- Percentage of PRs with changes requested
- Time spent in review (from first review request to approval)
- Percentage of PRs approved without comments

---

#### AI Override Rate

How often engineers reject or modify AI suggestions.

**Why it matters:** Engineers should be evaluating AI output, not accepting it blindly. Override rate is a proxy for human judgment remaining in the loop.

| | |
|:--|:--|
| **Target** | 20-40% = healthy engagement. <10% = rubber-stamping. >60% = AI misconfigured for your codebase. |
| **How to track** | IDE telemetry (Copilot/Cursor) or commit analysis comparing AI suggestions to final code. Some tools provide this natively. |

---

#### Guardrail Freshness

When AI instruction files were last meaningfully updated.

**Why it matters:** Stale guardrails mean AI is following outdated instructions. The codebase evolves, the guardrails should evolve with it.

| | |
|:--|:--|
| **Target** | Meaningful updates within the last 30 days for active codebases. |
| **How to track** | Git log on guardrail files (CLAUDE.md, .cursorrules, etc.). Filter out formatting-only changes. |

**Quick check:**
```bash
git log -1 --format="%ar" -- CLAUDE.md .cursorrules
```

---

#### Guardrail Coverage

Whether repeated mistakes are being captured as guardrails.

**Why it matters:** If the same types of mistakes keep happening, the guardrails aren't learning. The system isn't compounding.

| | |
|:--|:--|
| **Implementation** | Add "guardrail candidate" as an incident retro field. Track which candidates get implemented. |
| **How to track** | Manual audit. Review incident retros and ask: "Should this have been a guardrail? Is it one now?" |

---

#### Time-to-First-Review

How long PRs wait before someone looks.

**Why it matters:** Long review queues create pressure to skip review or approve quickly. This metric predicts review depth problems.

| | |
|:--|:--|
| **Target** | <4 hours for standard PRs. <1 hour for critical paths. |
| **How to track** | GitHub/GitLab APIs. Delta between PR open time and first review action. |

---

#### Review Queue Depth

PRs waiting for review at any given time.

**Why it matters:** AI increases PR volume. If review capacity doesn't scale, queues grow, and pressure to rubber-stamp increases.

| | |
|:--|:--|
| **Target** | Team-dependent, but growing queue is always a warning sign. |
| **How to track** | Snapshot counts from GitHub/GitLab API, tracked over time. |

---

### Layer 3 Diagnostic Guide

| Symptom | Check | Likely Cause |
|:--------|:------|:-------------|
| Quality dropping | Review depth | Reviews getting shallower |
| Same mistakes repeating | Guardrail freshness/coverage | Stale or missing guardrails |
| Override rate dropping | Quality metrics | Rubber-stamping if quality also down |

> **⚠️ Warning sign:** Review depth down + override rate down + guardrails stale = quality collapse incoming.

---

## Layer 4: Outcome Metrics

**Purpose:** Connect engineering work to business results. This is ground truth. Everything else is proxy.

| Metric | What It Measures | How to Track | Target |
|:-------|:-----------------|:-------------|:-------|
| **Customer-reported bugs** | Quality as experienced by users | Support tickets tagged as bugs | Trending down |
| **Incident frequency** | Production stability | PagerDuty, Opsgenie | Stable or declining |
| **MTTR ([Mean Time to Repair](https://limble.com/learn/mean-time-to-repair))** | How quickly you fix production problems | Incident timestamps | <1hr critical, <4hr standard |
| **Feature adoption** | Whether shipped work gets used | Product analytics (Amplitude, Mixpanel) | Meets adoption targets |
| **Time-to-value** | End-to-end from idea to customer value | Ticket lifecycle tracking | Trending down |

### Usage Guidelines

Validate that improvements in Layers 1-3 actually translate to outcomes.

> **⚠️ Warning sign:** Layers 1-3 look great, Layer 4 is flat or declining. You're optimizing the wrong things.

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

# Implementation Roadmap

## Phase 1: Baseline (Week 1-2)

**Objective:** Get signal with minimal tooling investment.

| Implement | Layer | Tooling Required |
|:----------|:------|:-----------------|
| ☐ Code churn tracking | L2 | Git access, GitClear or custom scripts |
| ☐ Defect escape rate | L2 | Defect tracker with stage tagging |
| ☐ Customer-reported bugs | L4 | Support ticket system |

## Phase 2: Process Visibility (Month 1)

**Objective:** Understand why quality metrics move.

| Implement | Layer | Tooling Required |
|:----------|:------|:-----------------|
| ☐ Review depth tracking | L3 | GitHub/GitLab API access |
| ☐ Guardrail freshness | L3 | Simple git log script |
| ☐ AI attribution tagging | L2 | Commit convention `[ai-assisted]` |

## Phase 3: Full Stack (Month 2-3)

**Objective:** Complete visibility across all layers.

| Implement | Layer | Tooling Required |
|:----------|:------|:-----------------|
| ☐ Rework ratio with tagging | L2 | Ticket hygiene discipline |
| ☐ AI override rate | L3 | IDE telemetry or code analysis |
| ☐ Time-to-rework | L2 | Linking fixes to original commits |
| ☐ Full outcome metrics | L4 | Product analytics integration |
| ☐ Connected dashboards | All | Engineering analytics platform |
| ☐ Thresholds and alerts | All | Custom configuration |

## Phase 4: Calibration (Ongoing)

| Activity | Cadence |
|:---------|:--------|
| Review thresholds | Quarterly |
| Guardrail audit | Quarterly |
| Outcome correlation analysis | Quarterly |
| Attribution accuracy check | Monthly |
| Metrics review | Monthly |

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
