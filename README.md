# The Metrics Stack for AI-Augmented Teams

> A four-layer framework for measuring what actually matters


If you're still measuring engineering productivity with PR count, lines of code, or even DORA metrics alone, you're measuring a world that no longer exists.

AI-augmented teams need a new metrics stack. Not because the old metrics are wrong, but because they're incomplete. They measure output. They're blind to quality, context, and the hidden costs AI creates.

---

## The Four Layers

| Layer | What It Measures | Signal Type | |
|:------|:-----------------|:------------|:--|
| **[Layer 1: Output](docs/layer-1-output.md)** | Volume of work produced | Lagging, easily gamed | PR count, LOC, deployments |
| **[Layer 2: Quality](docs/layer-2-quality.md)** | Whether the work is good | Lagging, harder to game | Churn, rework, defects |
| **[Layer 3: Process](docs/layer-3-process.md)** | Whether the system is healthy | Leading, diagnostic | Review depth, override rate |
| **[Layer 4: Outcome](docs/layer-4-outcome.md)** | Whether it matters to the business | Lagging, ground truth | Customer bugs, adoption |

**Key insight:** Output without quality is noise. Quality without outcome is vanity. Process metrics without the other layers are just activity tracking. You need all four layers to understand what's actually happening.

<img width="1408" height="768" alt="modern_AIAugmented_metrics_layers" src="https://github.com/user-attachments/assets/15d0dcd8-b7be-4fa3-9d0f-f29a6ddff988" />

---

## Using This Framework

| Section | What You'll Learn |
|:--------|:------------------|
| [How the Layers Connect](docs/how-layers-connect.md) | Trace problems from outcomes back to root causes |
| [Diagnostic Patterns](docs/diagnostic-patterns.md) | Common failure modes and how to fix them |
| [Implementation Roadmap](docs/implementation-roadmap.md) | Phased rollout from week 1 to ongoing calibration |
| [What This Doesn't Solve](docs/what-this-doesnt-solve.md) | Limitations and the role of human judgment |

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

- [The Guardrail Maintenance Problem]([docs/guardrail-maintenance-problem.md](https://invisiblefailure.substack.com/p/the-ai-guardrail-maintenance-problem)) — Why AI instruction files rot like Confluence pages

---

## Author

**Michaela Glaze**  
Fractional CTO and founder of [PivotWorks Consulting](https://pivotworks.io), specializing in execution risk prevention and delivery stabilization for post-PMF B2B SaaS companies.

- [LinkedIn](https://linkedin.com/in/michaelaglaze)
- [Substack: Invisible Failure](https://invisiblefailure.substack.com)

---

*If this framework helped your team, consider giving the repo a ⭐*
