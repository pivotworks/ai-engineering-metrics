# Layer 3: Process Metrics

[← Back to Overview](../)

**Purpose:** Measure whether humans are actually engaged or just rubber-stamping. These are leading indicators that predict quality problems before they surface in production.

---

## Why Process Metrics Matter

Process metrics are your early warning system. They show problems forming before they hit production. When Layer 2 shows quality dropping, Layer 3 tells you why.

---

## Metrics at a Glance

| Metric | Target | Key Signal |
|:-------|:-------|:-----------|
| [Review Depth](#review-depth) | ≥1 comment/PR | Humans disengaging from oversight |
| [AI Override Rate](#ai-override-rate) | 20-40% | Rubber-stamping vs. healthy skepticism |
| [Guardrail Freshness](#guardrail-freshness) | <30 days | AI following outdated instructions |
| [Guardrail Coverage](#guardrail-coverage) | Audit quarterly | System not learning from mistakes |
| [Time-to-First-Review](#time-to-first-review) | <4 hours | Review bottleneck forming |
| [Review Queue Depth](#review-queue-depth) | Stable/declining | Pressure to rubber-stamp building |

---

## Review Depth

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

## AI Override Rate

How often engineers reject or modify AI suggestions.

**Why it matters:** Engineers should be evaluating AI output, not accepting it blindly. Override rate is a proxy for human judgment remaining in the loop.

| | |
|:--|:--|
| **Target** | 20-40% = healthy engagement. <10% = rubber-stamping. >60% = AI misconfigured for your codebase. |
| **How to track** | IDE telemetry (Copilot/Cursor) or commit analysis comparing AI suggestions to final code. Some tools provide this natively. |

---

## Guardrail Freshness

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

## Guardrail Coverage

Whether repeated mistakes are being captured as guardrails.

**Why it matters:** If the same types of mistakes keep happening, the guardrails aren't learning. The system isn't compounding.

| | |
|:--|:--|
| **Implementation** | Add "guardrail candidate" as an incident retro field. Track which candidates get implemented. |
| **How to track** | Manual audit. Review incident retros and ask: "Should this have been a guardrail? Is it one now?" |

---

## Time-to-First-Review

How long PRs wait before someone looks.

**Why it matters:** Long review queues create pressure to skip review or approve quickly. This metric predicts review depth problems.

| | |
|:--|:--|
| **Target** | <4 hours for standard PRs. <1 hour for critical paths. |
| **How to track** | GitHub/GitLab APIs. Delta between PR open time and first review action. |

---

## Review Queue Depth

PRs waiting for review at any given time.

**Why it matters:** AI increases PR volume. If review capacity doesn't scale, queues grow, and pressure to rubber-stamp increases.

| | |
|:--|:--|
| **Target** | Team-dependent, but growing queue is always a warning sign. |
| **How to track** | Snapshot counts from GitHub/GitLab API, tracked over time. |

---

## Diagnostic Guide

| Symptom | Check | Likely Cause |
|:--------|:------|:-------------|
| Quality dropping | Review depth | Reviews getting shallower |
| Same mistakes repeating | Guardrail freshness/coverage | Stale or missing guardrails |
| Override rate dropping | Quality metrics | Rubber-stamping if quality also down |

> **⚠️ Warning sign:** Review depth down + override rate down + guardrails stale = quality collapse incoming.

---

## Navigation

[← Layer 2: Quality](layer-2-quality.md) · [Layer 4: Outcome →](layer-4-outcome.md)
