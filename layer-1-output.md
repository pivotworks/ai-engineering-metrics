# Layer 1: Output Metrics

[← Back to Overview](../)

**Purpose:** Measure volume of work. Use for context, not evaluation.

---

## Why Output Metrics Are Dangerous Alone

These metrics are easy to collect and easy to game. AI has made them trivially inflatable. The creator of Claude Code pushes 50 to 100 PRs per week using parallel AI agents. That's not a criticism of his productivity. It's a signal that PR count no longer means what it used to mean.

---

## Metrics

| Metric | What It Measures | How to Track | Limitations |
|:-------|:-----------------|:-------------|:------------|
| **PR count / merge frequency** | How much code is shipping | Native in GitHub/GitLab | Inflated by AI, gameable by splitting work |
| **Deployment frequency** | How often you release to production | CI/CD pipeline logs, DORA tooling | More deployments only good if deployments are good |
| **Commit frequency** | Activity signal | Git log analysis | Tells you nothing about value |
| **Lines of code** | Volume of code changes | Git diff analysis, GitClear | Best work often reduces LOC |

---

## Usage Guidelines

- ✅ Track at team level, not individual
- ✅ Use trend lines, not absolutes
- ✅ Treat as context for other metrics
- ❌ Don't use for standalone evaluation
- ❌ Don't evaluate engineers based on PR count

> **⚠️ Warning sign:** If Layer 1 metrics are your primary dashboard, you're measuring activity, not productivity.

---

## Navigation

[Layer 2: Quality →](layer-2-quality.md)
