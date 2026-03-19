# Layer 2: Quality Metrics

[← Back to Overview](http://github.com/pivotworks/ai-engineering-metrics/blob/main/README.md)

**Purpose:** Measure whether the work is actually good. This is where AI-generated problems surface.

---

## Why Quality Metrics Matter

These metrics require more infrastructure to track but are much harder to game. They catch what output metrics miss: code that shipped fast but shouldn't have, work that creates more work, and the hidden costs of speed.

---

## Metrics at a Glance

| Metric | Target | Key Signal |
|:-------|:-------|:-----------|
| [Code Churn Rate](#code-churn-rate) | <10% | Shipping fast but creating rework |
| [Rework Ratio](#rework-ratio) | <15% | Hidden costs of AI-generated code |
| [Time-to-Rework](#time-to-rework) | >30 days | Review process not catching issues |
| [Defect Escape Rate](#defect-escape-rate) | Trending ↓ | Tests not catching what matters |
| [Defect Attribution](#defect-attribution) | Baseline first | AI ROI analysis foundation |

---

## Code Churn Rate

Lines reverted or modified within 14-21 days.

**Why it matters:** GitClear research projects code churn will double by 2026 due to AI-generated code. High churn means you're shipping faster but creating rework.

| | |
|:--|:--|
| **Formula** | `(lines modified within window / total lines committed) * 100` |
| **Target** | Below 10% for mature codebases. Above 15% indicates systemic issues. |
| **How to track** | Git analysis comparing commits to subsequent modifications. [GitClear](https://gitclear.com) provides this out of the box. |

---

## Rework Ratio

Percentage of effort spent fixing previous work.

**Why it matters:** AI can inflate output while creating hidden rework costs. If you ship twice as much but spend 40% of your time fixing it, you're not ahead.

| | |
|:--|:--|
| **Formula** | `(story points on rework tickets / total story points) * 100` |
| **Target** | Below 15% of total effort. Spikes above 25% indicate quality problems upstream. |
| **How to track** | Tag tickets/PRs as "rework," "fix," "bugfix," or link to original implementation. |

---

## Time-to-Rework

How long code survives before requiring intervention.

**Why it matters:** Short time-to-rework means the review process isn't catching issues. The code looked fine, passed review, then broke quickly.

| | |
|:--|:--|
| **Formula** | `median(first_fix_timestamp - merge_timestamp)` for commits requiring fixes |
| **Target** | Greater than 30 days = acceptable. Under 7 days = significant problems. |
| **How to track** | Track time delta between initial merge commit and first fix commit touching the same files/functions. |

---

## Defect Escape Rate

Bugs found in production vs. caught during development.

**Why it matters:** If production defect rate is rising while test coverage looks good, your tests aren't catching what matters.

| | |
|:--|:--|
| **Formula** | `(production defects / total defects) * 100` |
| **Target** | Trending down over time. Absolute numbers depend on your context. |
| **How to track** | Defect tracking with stage attribution. Tag where defects were found: unit test, integration test, QA, staging, production. |

---

## Defect Attribution

Which defects trace to AI-generated vs. human-written code.

**Why it matters:** Without this, you can't evaluate whether AI is helping or creating hidden costs. This is the baseline for any AI ROI analysis.

| | |
|:--|:--|
| **Implementation** | Add `[ai-assisted]` or `[ai-generated]` tags to commits. Build reporting that segments defect rates by tag. |
| **How to track** | Tag AI-generated code at commit time. Add metadata or commit message conventions. Then link defects to originating commits. |

---

## Usage Guidelines

- Compare AI-generated versus human-generated code quality once you have attribution
- Identify patterns: certain types of AI-generated work that consistently need rework
- Set thresholds that trigger process changes

> **⚠️ Warning sign:** Quality metrics flat while output metrics spike means you're creating future problems at an accelerated rate.

---

## Navigation

[← Layer 1: Output](layer-1-output.md) · [Layer 3: Process →](layer-3-process.md)
